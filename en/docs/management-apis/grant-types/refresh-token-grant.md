# Refresh Token Grant

After an access token is generated, sometimes you might have to refresh
or renew the old token due to expiration or security concerns. You use
the refresh token grant when a new access token is needed. With this
grant type, the refresh token acts as credentials that are issued to the
client by the authorization server. Issuing a refresh token is optional.
If the authorization server issues a refresh token, it is included when
issuing an access token. Refresh tokens are issued for all other grant
types other than the **implicit grant** as recommended by the OAuth 2.0
specification.

!!! tip
    
    Be sure to keep the refresh token private, similar to the
    access token as this token issues access tokens without user
    interactions.
    

To use this grant type, you need a refresh token, using which you can
get a new access token and a refresh token. This can be done by issuing
a REST call to the Token API through a REST client like cURL, with the
following parameters:

-   Token API URL -
    `https://gateway.api.cloud.wso2.com/token`.
-   payload -
    `grant_type=refresh_token&refresh_token=<retoken>`. Replace the `<retoken>` value with the refresh token that you have.
-   headers -
    `Authorization :Basic <base64 encoded string of consumer-key:consumer-secret>, Content-Type: application/x-www-form-urlencoded`. Replace
    `<base64-encoded string-of-consumer-key:consumer-secret>` as appropriate.

For example, the following cURL command can be used to access the Token
API and grant a refresh token.

``` java
curl -k -d "grant_type=refresh_token&refresh_token=<retoken>" -H "Authorization: Basic SVpzSWk2SERiQjVlOFZLZFpBblVpX2ZaM2Y4YTpHbTBiSjZvV1Y4ZkM1T1FMTGxDNmpzbEFDVzhh" -H "Content-Type: application/x-www-form-urlencoded" https://gateway.api.cloud.wso2.com/token
```

When you use the refresh grant to get a new access token, the refresh
token is renewed by default. The new refresh token has a new expiry time
and the previous refresh token becomes inactive.

### Revoke access tokens

After issuing an access token, a user or an admin can revoke it
in case of theft or a security violation. You can do this by calling the
Revoke API using a REST Client. The Revoke API's endpoint URL is
`https://gateway.api.cloud.wso2.com/revoke`. The parameters required to invoke this API are as follows:

-   The token to be revoked.
-   Consumer key and consumer secret key. Must be encoded using Base64
    algorithm.

For example:

``` java
curl -k -d "token=<access-token-to-be-revoked>" -H "Authorization: Basic Base64Encoded(Consumer-key:consumer-secret)" https://gateway.api.cloud.wso2.com/revoke
```

!!! tip
    
    Even after revoking a token, it might still be available in the
    API Gateway cache to consumers until the cache expires in approximately 15 minutes.


