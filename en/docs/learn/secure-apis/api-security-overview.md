# API Security Overview

Security is an integral part when it comes to API Management. An effective API management solution allows you to implement the core API security aspects, which are authentication, authorization, confidentiality, integrity, and availability.

When working with APIs, it is important to have an authorization mechanism to ensure secure access.

WSO2 API Cloud uses OAuth 2.0 as the primary method of authenticating API invocations. 
With WSO2 API Cloud, API publishers don’t need to worry about the security of their APIs because OAuth security is enforced on all published APIs. When it comes to API consumers, it is necessary to generate an access token to invoke an API after subscribing to an API.

WSO2 API Cloud provides a [token API](../../../management-apis/token-api) so that you can generate and renew user
and application access tokens. The response of the token API is a JSON
message. You can extract the token from the JSON message and pass it with an HTTP
Authorization header to invoke APIs subscribed under a particular application.

WSO2 API Cloud supports the most common authorization grant types. Click on a required grant type to understand how to use it to generate/renew access tokens and authorize:

- [Authorization Code Grant](../../../management-apis/grant-types/authorization-code-grant) 
- [Refresh Token Grant](../../../management-apis/grant-types/refresh-token-grant) 
- [Password Grant](../../../management-apis/grant-types/password-grant)  
- [Client Credentials Grant](../../../management-apis/grant-types/client-credentials-grant) 
- [SAML Extension Grant](../../../management-apis/grant-types/saml-extension-grant)

Instead of using the token API, you can also generate access tokens via the API Store. 

For information on how you can generate access tokens via the API Store, see [Generate Application Keys](../../consume-apis/generate-application-keys).  












