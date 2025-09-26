# Configuring AWS Cognito

## Prerequisites

- A cognito **user pool** already created in your AWS account.
- The `FederationMetadata.xml` file generated from **Active Directory** or **Azure Entra ID**.

## Configure Cognito Pool

### Add a SAML Identity Provider

1. In your user pool, in the right side menu go to **Authorization > Social and external providers**.
2. Press the button **Add identity provider** and select SAML.
3. For commodity reasons, set the provider name as `chat-ad-provider`. Leave the rest of the configurations as default.
4. Under **Metadata document** press the button **Choose file** and upload the `FederationMetadata.xml` from **Active Directory** or **Entra ID**.
5. Click on the yellow button **Add identity provider**.

---

### Configure Attribute Mapping

1. Once your **IdP** was created, go to its configuration and press **Attribute Mapping > Edit**
2. Specify exactly the following attributes:
   - **email** - E-Mail Address
   - **name** - Name
   - **username** - Name ID
3. Click on **Save changes**.
4. Also, in your identity provider don't forget to donwload the **signing certificate** and the **metadata.xml** from Cognito.
5. Click on **View signing certificate**, a window will open, there press on **Download as .crt**. After the download, click on **Close**.
6. Now go to **Metadata document** section and press on the **metadata.xml** download link.

---

### Integrate with an App Client

1. In your user pool, in the right side menu go to **Applications > App clients**.
2. Select your app client and press **App client information > Edit**.
3. Ensure that **only** the following values are selected:
   - ALLOW_USER_AUTH
   - ALLOW_USER_PASSWORD_AUTH
   - ALLOW_CUSTOM_AUTH
   - ALLOW_REFRESH_TOKEN_AUTH
4. Click on **Save changes**
5. Now in your app client select the **Login pages** tab and press the **Edit** button.
6. In **Allowed callbacks URLs** add the callback page for your application (e.g., <https://chatbot.com/callback>)
7. In **Identity providers** select the identity provider you created (`chat-ad-provider`).
8. In **OpenID Connect scopes** ensure that **Email, OpenID** and **Profile** are selected.
9. Click on **Save changes**.

---

### Key Cognito Information

This section outlines the essential data you'll need from your Amazon Cognito user pool to configure a SAML 2.0 identity provider (IdP) in Active Directory or Entra ID.

1. In cognito userpool go to **Overview** and copy the **User Pool ID**.
2. In cognito userpool go to **Branding > Domain** and copy the **Domain**.
3. Using the information you gathered above, you'll need to construct three key endpoints:
   - **URN Service Provider:** `urn:amazon:cognito:sp:USERPOOL_ID`
   - **Assertion Consumer Service (ACS):** `URSERPOOL_DOMAIN/saml2/idpresponse`
   - **Metadata URL:** `URSERPOOL_DOMAIN/saml2/idp/metadata`
   - **Signing Certificate File** the `chat-userpool.crt` file you downloaded from the **IdP**.
   - **Metadata File** the `metadata.xml` file you downloaded from the **IdP**.

Based on your requirements, you can now proceed with the instructions for configuring either **Active Directory Federation Services (AD FS)** or **Azure Entra ID**.

## Integrate with Active Directory FS

### Creating a Relying Party Trust

1. In windows server open **Server Manager > Tools > AD FS Management**.
2. In the right sidebar, go to **AD FS > Relying Party Trusts**.
3. **Right-click** and select **Add Relying Party Trust**, keep the **Claims Aware** setting and hit **Start**.
4. On **Select Data Source** choose the **Import data about the relying party from a file**, click on **browse** and choose the location of `metada.xml` file. Hit **Next** button.
5. For the **Display Name** set a name for the Relying Party Trust (e.g., CognitoSAMLApp).
6. Continue with the creation wizard and click on **Finish**.

---

### Configuring the Relying Party Trust

1. **Right-click** on the recently created relying party trust and select **Properties**.
2. Navigate to the **Identifiers** tab. In the **Relying Party Identifier** field, paste the **URN Service Provider** URL and click **Add**.
3. **Remove** the rest of the identifiers that are not recognized or are not from Cognito.
4. Go to the **Signature** tab, click **Add**, and select the `chat-userpool.crt` file. **Remove** any other signatures that are not recognized or are not from Cognito.
5. Switch to the **Encryption** tab and click **Remove**.
6. Select the **Endpoints** tab. Locate the SAML Assertion Consumer Endpoint with index 0 and click **Edit**.
7. In the **Edit Endpoint** window, change the **Binding** to `POST`. In the **Trusted URL** field, paste the **ACS** URL you constructed using your Cognito domain. Click **OK** to save the changes.
8. Close the **Properties** window.

---

### Relying Party Trust Claims

1. **Right-click** on the created relying party trust and select **Edit Claim Issuance Policy**.
2. **Remove** any claim that are not recognized or are not from Cognito.
3. Click on **Add Rule**, all rules will use the **Send LDAP Attributes...** for the **Claim rule template**.
4. Now you'll need to add **three rules**, one by one with the following specifications. **Don't add the claims in a single rule**:
   1. **Rule name:** email
      - **LDAP Attribute:** E-Mail-Addresses
      - **Outgoing Claim:** E-Mail Address
   2. **Rule name:** name
      - **LDAP Attribute:** Display-Name
      - **Outgoing Claim:** Name
   3. **Rule name:** username
      - **LDAP Attribute:** SAM-Account-Name
      - **Outgoing Claim:** Name ID
5. Click on **Ok** and close the window.

---

### Restart the Service

1. On Windows Server, open **Powershell** as **Administrator**.
2. On the shell, paste the command `Restart-Service adfssrv`.
3. Wait until it restarts, you can check it's status by using the command `Get-Service adfssrv`.
4. The **AD FS** integration with **Congito** should be working now.

## Integrate with Azure Entra ID
