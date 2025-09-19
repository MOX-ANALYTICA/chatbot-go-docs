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

### Configure Attribute Mapping

1. Once your IdP was created, go to its configuration and press **Attribute Mapping > Edit**
2. Specify exactly the following attributes:
   - **email** - E-Mail Address
   - **name** - Name
   - **username** - Name ID
3. Click on **Save changes**.
4. Also, in your identity provider don't forget to **donwload the metadata from Cognito**.
5. Go to **Metadata document** section and press on the **metadata.xml** download link.

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

## Integrate with Active Directory FS


## Integrate with Entra ID
