# Authorization Code Grant

Instead of requesting authorization directly from the resource owner
(resource owner's credentials), in this grant type, the client directs
the resource owner to an authorization server. The authorization server
works as an intermediary between the client and resource owner to issues
an authorization code, authenticate the resource owner and obtain
authorization. As this is a redirection-based flow, the client must be
capable of interacting with the resource owner's user-agent (typically a
Web browser) and receiving incoming requests (via redirection) from the
authorization server.

The client initiates the flow by directing the resource owner's
user-agent to the authorization endpoint (you can use the
`/authorize` endpoint for the authorization code grant
type of OAuth 2.0). It includes the client identifier, response\_type,
requested scope, and a redirection URI to which the authorization server
sends the user-agent back after granting access. The authorization
server authenticates the resource owner (via the user-agent) and
establishes whether the resource owner granted or denied the client's
access request. Assuming the resource owner grants access, the
authorization server then redirects the user-agent back to the client
using the redirection URI provided earlier. The redirection URI includes
an authorization code.

The client then requests an access token from the authorization server's
`/token` endpoint by including the authorization code
received in the previous step. When making the request, the client
authenticates with the authorization server. It then includes the
redirection URI used to obtain the authorization code for verification.
The authorization server authenticates the client, validates the
authorization code, and ensures that the redirection URI matches the URI
used to redirect the client from the `/authorize` endpoint in the previous
response. If valid, the authorization server responds back with an
access token and, optionally, a refresh token.

#### Invoke the Token API to generate tokens

The Authorization API URL is
`https://gateway.api.cloud.wso2.com/authorize`

-   query component:
    `response_type=code&client_id=<consumer_key>&scope=PRODUCTION&redirect_uri=<application_callback_url>`
-   headers:
    `Content-Type: application/x-www-form-urlencoded`

For example, the client directs the user-agent to make the following
HTTP request using TLS.

``` java
GET
/authorize?response_type=code&client_id=wU62DjlyDBnq87GlBwplfqvmAbAa&scope=PRODUCTION&redirect_uri=https%3A%2F%2Fclient%2Eexample%2Ecom%2Fcb
HTTP/1.1 
Host: server.example.com 
Content-Type:
application/x-www-form-urlencoded 
```

The authorization server redirects the user-agent by sending the
following HTTP response:

``` java
HTTP/1.1 302 Found 
Location:
https://client.example.com/cb?code=SplxlOBeZQQYbYS6WxSbIA
```

Now the client makes the following HTTP request using TLS to the `/token`
endpoint.

``` java
POST /token HTTP/1.1 
Host: server.example.com 
Authorization: Basic
SVpzSWk2SERiQjVlOFZLZFpBblVpX2ZaM2Y4YTpHbTBiSjZvV1Y4ZkM1T1FMTGxDNmpzbEFDVzhh
Content-Type:
application/x-www-form-urlencoded 
grant_type=authorization_code&code=SplxlOBeZQQYbYS6WxSbIA&redirect_uri=https%3A%2F%2Fclient%2Eexample%2Ecom%2Fcb
```

The `/token` endpoint responds in a manner similar to the password grant
type.

``` xml
<Authenticators>
   <Authenticator name="BasicAuthenticator" disabled="false" factor="1">
      <Status value="10" loginPage="/authenticationendpoint/login.do" />
   </Authenticator>
</Authenticators>
```
