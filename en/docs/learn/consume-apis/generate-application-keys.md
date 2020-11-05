# Generate Application Keys

An API access token/key is a string that is passed as an HTTP header in an API request. WSO2 API Claud supports OAuth2.0 bearer token-based authentication for API access and the API key has to be submitted along with the API request in order to authenticate the access.

When an application developer registers an application in the API Store, a consumer-key 
and consumer-secret pair is generated, which represent the credentials of the application that is registered. The consumer-key becomes the unique identifier of the application, similar to a user's user name, and is used to authenticate the application/user. When an API key or an API access token is issued for an application, it is issued against the consumer-key. When sending an API request, the access token has to be passed as the authorization HTTP header value. 

For example, `Authorization: Bearer NtBQkXoKElu0H1a1fQ0DWfo6IX4a`


Follow the instructions below to generate application keys via the API Store:

1.  Sign in to [WSO2 API Cloud](https://api.cloud.wso2.com) as an admin user and then access the API Store.
            
2.  Click **APPLICATIONS** to navigate to the applications listing page and then click on the respective application for which you want to generate keys.
 
3.  Click **Production Keys** and then click **Generate Keys** to create an application access token. This generates an access token along with the application consumer key and secret.

     - If the application type is **JWT**, a JSON Web Token (JWT) is generated. Make sure to copy the JWT access token that appears so that you can use it in the future.
     
     -  If the application type is **OAuth**, the generated access token will be an opaque token.
     
     
     Once the keys are generated, you can find the consumer key and consumer secret pair via the application details page.
     
     
    !!! tip
        - In the Access token validity period field, you can set an expiration period to specify the validity period of the token after it is generated. Set this to a negative value to ensure that the token never expires.

        - When you generate access tokens for APIs that are protected by scopes, you can select the respective scopes and thereafter, generate the token for it.
  
