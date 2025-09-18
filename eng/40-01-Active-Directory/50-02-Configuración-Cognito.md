Phase 4: Configuring AWS Cognito

    Create a User Pool: If you haven't already, create a user pool in the Amazon Cognito console.

    Add a SAML Identity Provider:

        In your user pool, go to Federation > Identity providers.

        Select SAML.

        Give your provider a name (e.g., ADFS).

        Under Metadata document, choose Upload metadata document and upload the .xml file you downloaded from your ADFS server.

        Click Create.

    Configure Attribute Mapping:

        Go to the Attribute mapping tab for your new SAML provider.

        This is where you map attributes from AD FS (e.g., email, name) to Cognito user pool attributes.

        For example, you will map the SAML attribute http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress to the Cognito attribute Email.

    Integrate with an App Client:

        Go to App integration > App client settings.

        Select your SAML provider in the "Enabled Identity Providers" list.

        Make sure you have a redirect URL configured for your application.

        Click Save changes.