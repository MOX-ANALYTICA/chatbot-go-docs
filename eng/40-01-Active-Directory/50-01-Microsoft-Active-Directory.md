# Microsoft Active Directory (Windows Server 2022)

1. Open **Server Manager > Manage > Add Roles and Features**.
2. **Installation Type:** select **Role-based feature installation**.
3. **Server Selection:** choose the server from the server pool where you want to install AD DS and click Next.
4. **Server Roles:** check the following services:
    - Active Directory Domain Services
    - Active Directory Federation Services
    - Active Directory Certificate Services
       - Certification Authority
       - Certification Authority Web Enrollment
5. A new window will pop up asking to add required features. Click **Add Features** and then **Next**.
6. **Confirm Installation:** review your selections and click Install. The installation will begin and may take a few minutes. Once it's complete, click Close.
7. Now, in the **Server Manager** you'll see a yellow flag, now we'll need to configure each installed feature. Follow the rest of the guide in order.

## Active Directory Domain Services

### Change Adapter IPv4 DNS

If you're in a local environment, running on an EC2 instance do the following before starting to configure the AD.

1. On the **Windows search bar** search for **Network Status**.
2. Once the window is opened, click on **Change adapter options**.
3. Right-click on **Ethernet 3 > Properties** and select **Internet Protocol Version 4 (TCP/IPv4) > Properties**.
4. Update the **Preferred DNS server** to the **Private IP address** of the EC2 Instance.
5. Click on **Ok** and close the windows.

### Promoting the Server to a Domain Controller

1. **Promote to Domain Controller:** Click the yellow flag and select Promote this server to a domain controller. This opens the Active Directory Domain Services Configuration Wizard.
2. **Deployment Configuration:** Select Deployment Configuration: Select **Add a new forest**. In the **Root domain name** field, enter the name for your new domain (e.g., **yourdomain.local**).
3. **Domain Controller Options:**
   - Set a Directory Services Restore Mode (DSRM) password. This is important for recovering the domain controller in case of an issue.
   - Keep the DNS Server and Global Catalog options checked, as this is your first domain controller in the new forest.
   - Click Next.
4. **Additional Options:** The NetBIOS domain name will be automatically populated. You can change it if you wish, but for testing, the default is fine. Click **Next**.
5. **Review Options and Install:** Review the summary of your choices. Once you are satisfied, click Next to run the prerequisite check. After the check passes, click **Install**. The server will restart automatically to complete the promotion.

### Creating the AD Users

1. Open **Server Manager > Tools > Active Directory Users and Computers**.
2. Now, in the console tree on the left, right-click on the domain name you created.
3. Select **New > User** and fill the user details for **First name**, **Last name** and **User logon name**.
4. Create two users one for testing and one for the **AD FS management** (eg. <testuser@yourdomain.local>, <svc-adfs@yourdomain.local>)
5. Set a password for both, and optionally tick the checkbox for **Password never expires**.
6. Click **Apply** and **Ok**.

> **Important**
> Now that an AD is configured, you'll need to specify that your Administrator password never expires. This way you won't lose access to your Windows Server in the future.
> In the **Users and Computers** menu navigate to **Users**, right-click **Administratior** and change the password policy in **Properties > Account**.

## Active Directory SSL Certificate

We'll need a valid **SSL certificate** to later configure the **AD FS**. We have two options: **internal certificate authority** or **self-signed certificate**. For the most robust solution we recommend the first option, but you're free to choose.

---

### Self-signed certificate

1. Open PowerShell as an administrator on your AD FS server.
2. Run the `New-SelfSignedCertificate` cmdlet to create a new certificate. The key is to include the correct DNS name for your federation service, for example, `sts.yourtestdomain.local`.

   ```bash
   New-SelfSignedCertificate -DnsName "sts.youdomain.local" -CertStoreLocation "Cert:\LocalMachine\My" -NotAfter (Get-Date).AddYears(3)
   ```

   - `New-SelfSignedCertificate`: The command to create the certificate.

   - `DnsName "sts.yourdomain.local"`: Sets the DNS name. This must match the federation service name you configured in ADFS.

   - `CertStoreLocation "Cert:\LocalMachine\My"`: Specifies where the certificate should be stored.

   - `NotAfter (Get-Date).AddYears(3)`: Sets the expiration date three years from now.

3. After the command runs, it will output the certificate's thumbprint. You can then use this certificate when configuring ADFS.

---

### Using Internal Certificate Authority (CA)

#### Configuring the CA

1. In **Server Manager**, go to the **Certification Authority** role service to configure.
2. Choose **Enterprise CA** as the setup type to integrate it with your AD.
3. Select **Root CA** since this is the frst and only CA in your test environment.
4. Choose the **create new private key**.
5. On the **Cryptography for CA** page, accept the default settings unless you have specific requirements.
6. Give your CA a name. For instance, `admox-CA`.
7. Set the validity period for the CA certificate (e.g., 5 years).
8. Review the settings and click **Configure**.

---

#### Create the DNS Record

For a client to find your AD FS service, you must create a DNS record that maps the federation service name to your server's static private IP address.

1. Open **Server Manager > Tools > DNS**.
2. Navigate to your domain's **Forward Lookup Zone** (e.g., `yourdomain.local`).
3. Right-click on the zone and select **New Host (A or AAAA)**.
4. In the "Name" field, enter the prefix you chose (e.g., `sts`). The FQDN (Fully Qualified Domain Name) will be created automatically.
5. In the "IP address" field, enter the **static private IP address** of your AD FS server.
6. Click **Add Host** and then **OK**.

---

#### Generate the Certificate Template

Now that you have a name and a DNS record for it, you can create and enroll the certificate using the AD CS certificate template you made earlier.

1. Press the **Windows key + R**, type `mmc` in the Run box, and press Enter. This will open **MMC** (Microsoft Management Console).
2. Go to **File > Add/Remove Snap-in**.
3. In the "Add or Remove Snap-ins" window, find and select **Certificate Templates** from the "Available snap-ins" list on the left side.
4. Click **Add >**, then click **OK**.
5. The **Certificate Templates** console will appear in your MMC window, select it and a list of certificates will appear.
6. Right-click the **Web Server** template and select **Duplicate Template**.
7. On the **General** tab, give your new template a name like `ADFS-Certificate-Template`, also set the **Vality period** (e.g. 3 years).
8. On the **Subject Name** tab, ensure **Supply in the request** is selected. This allows you to specify the DNS name later.
9. On the **Security** tab, select your **Administrator**'s computer account and give it **Read** and **Enroll** permissions.
10. Back in the main **Certification Authority** console, right-click **Certificate Templates > New > Certificate Template to Issue**. Select your new `ADFS-Certificate-Template`.

---

#### Enroll the Certificate

1. Press the **Windows key + R**, type `certlm.msc`.
2. Navigate to **Personal > Certificates**.
3. Right-click on the "Certificates" folder and select **All Tasks > Request New Certificate...**
4. In the wizard, click **Next** twice to get to the "Request Certificates" page.
5. You should now see the `ADFS-Certificate-Template` you created. Click the link that says **"More information is required to enroll for this certificate. Click here to configure settings."**
6. In the **Subject name** section, from the **Type** dropdown, select **Common name**.
7. In the **Value** box, enter the federation service name you chose (e.g., `sts.yourdomain.local`).
8. Click **Add**.
9. Now, from the **Type** dropdown, select **DNS**.
10. In the **Value** box, enter the same federation service name (`sts.yourdomain.local`).
11. Click **Add**, then click **OK**.
12. Click **Enroll** to complete the request.

The certificate will be created and stored in your computer's personal certificate store, ready to be selected when you run the AD FS configuration wizard. This process ensures the certificate's subject name matches the federation service name you'll use, preventing errors during configuration.

## Active Directory Federation Service

### ADFS Configuration

1. Now follow the configuration wizard for **ADFS**.
2. Now you'll be able to select the domain you configured (`sts.yourdomain.local`).
3. The **Specify Service Account** select **use an existing domain user account**, select the user you created for the **ADFS** (`svc-adfs`) and specify the password you configured.
4. Follow the remaining steps to finish the AD FS configuration. The wizard will then perform a prerequisite check and complete the installation.
5. At the end of the installation, the **ADFS** will show warnings about the service. All of these warnings are informational in your specific test scenario. The most important step now is to restart the server to complete the AD FS configuration

### Generating the Federation Metadata XML file

This is the `.xml` file you need for Cognito. AD FS automatically generates this file at a specific URL.

1. On your ADFS server, open a web browser.
2. Navigate to the following URL, replacing yourtestdomain.local with your actual federation service name:

   ```xml
   https://sts.yourtestdomain.local/FederationMetadata/2007-06/FederationMetadata.xml
   ```

3. Your browser may show a certificate warning. For a test environment, you can safely ignore this and proceed.
4. Save the XML file to your computer. This is the file you will upload to AWS Cognito.
