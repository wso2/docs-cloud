# Token API

Users need access tokens to invoke APIs subscribed under an application.
Access tokens are passed in the HTTP header when invoking APIs. WSO2 API
Cloud provides a token API that you can use to generate and renew user
and application access tokens. The response of the token API is a JSON
message. You extract the token from JSON and pass it with the HTTP
authorization header to access the API.

WSO2 API Cloud supports the following most common authorization grant types. Click on a required grant type to understand how to use it to generate/renew access tokens and authorize.

- [Authorization Code Grant](../grant-types/authorization-code-grant) 
- [Refresh Token Grant](../grant-types/refresh-token-grant) 
- [Password Grant](../grant-types/password-grant)  
- [Client Credentials Grant](../grant-types/client-credentials-grant) 
- [SAML Extension Grant](../grant-types/saml-extension-grant)