# Azure Entra ID Configuration

## Create the SAML Business App

1. Brose to **Browse to Entra ID > Enterprise apps > New application.**.
2. Click **Create your own application**. Name it (e.g., **CognitoSAMLProvider**)
3. Select **Integrate any other application you don't find in the gallery (Non-gallery)**
4. Click **Create**

## Configure SAML SSO

1. In your new enterprise application, go to **Single sign-on** (left sidebar)
2. Select **SAML** as the single sign-on method
3. In **Basic SAML Configuration**, click **Edit** and configure:
   - **Identifier (Entity ID):** `urn:amazon:cognito:sp:USERPOOL_ID`
   - **Reply URL (Assertion Consumer Service URL):** `URSERPOOL_DOMAIN/saml2/idpresponse`
   - **Sign on URL (optional):** Leave empty
   - Click **Save**

## Configure Attributes & Claims

1. Still in the SAML configuration, go to **Attributes & Claims** section, click **Edit**
2. On **Required claims** modify the following, click on each of them and set:
   - **Source attribute:** `user.userprincipalname` (or `user.mail` if you prefer email)
   - **Name ID format:** `Email address` or `Unspecified`
3. **Verify the default claims exist** (Azure creates these automatically):

   | Claim Name (Full URI)                                                | Source Attribute | Notes         |
   | -------------------------------------------------------------------- | ---------------- | ------------- |
   | `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress` | user.mail        | Default claim |
   | `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`         | user.displayname | Default claim |

4. **(Optional) Add additional claims only if needed**:

   | Claim Name  | Source Attribute |
   | ----------- | ---------------- |
   | given_name  | user.givenname   |
   | family_name | user.surname     |

## Download Federation Metadata

1. In the **SAML Certificates** section
2. Download the **Federation Metadata XML** file
3. Save it (you'll upload this to Cognito)

## Authorize users in Entra ID to access

1. Go to **Users and groups** (left sidebar)
2. Click **Add user/group**
3. Select the users or groups who should have access
4. Click **Assign**

**OR** allow all users in your tenant:

1. Go to **Entra ID Management Center Applications > Enterprise apps**
2. Search the application you created named **CognitoSAMLProvider**
3. On the leftside bar select the option **Properties**
4. In the **Is assignment required?** field select **No**
