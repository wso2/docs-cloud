# Secure APIs using OAuth2 Access Tokens

You can secure APIs published on WSO2 API Cloud via OAuth 2.0, which is the de facto standard for access delegation in the REST API world. Any client application invoking a OAuth2 secured API needs to have a valid subscription to that particular API and provide a valid OAuth2.0 access token when invoking it. 

Once you have the got the required credentials, namely the consumer key and consumer secret for your application, you (application users) can obtain an access tokens to invoke APIs which are subscribed under the given application. WSO2 API Manager offers a set of OAuth2 grant types for obtaining access tokens depending on the type of the access token owner, type of the application and the trust relationship with the application. Please see [OAuth2 Grant Types]
({{base_path}}/learn/api-security/oauth2/grant-types/overview/) to understand more about the OAuth2 grant types.

### OAuth 2.0 Access Token Types

OAuth 2.0 access tokens come in two different flavors

   - [JWT Access Tokens]({{base_path}}/learn/api-security/oauth2/access-token-types/jwt-tokens)
    
   - [Opaque Access Tokens]({{base_path}}/learn/api-security/oauth2/access-token-types/opaque-tokens)
   
The token type is bound to the application and the consumer has to specify the supported token type at application creation time. Once the token type is specified, all the access tokens issues under that particular application will be in the specified access token type. 

For example, the **DefaultApplication** available for consumers in Developer Portal is in JSON Web Token (JWT) type, hence all the access tokens issued under the **DefaultApplication** are JWTs.

HTTP Authorization header is the most common method of providing authentication information for REST APIs. The access token (followed by **Bearer**) need to be sent via the authorization header, for the client application to authenticate the API that is being accessed. The format of the header is as follows.

``` bash tab="Format"
Authorization : Bearer <access-token>
        
```

``` bash tab="Example"
Authorization : Bearer NtBQkXoKElu0H1a1fQ0DWfo6IX4a
        
The string `NtBQkXoKElu0H1a1fQ0DWfo6IX4a` is a sample value of the access token that is being sent from the client application.
```

