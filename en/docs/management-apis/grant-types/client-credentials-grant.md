# Client Credentials Grant

The client credentials grant is suitable for machine-to-machine
authentication or for clients making requests to an API that does not
require the user’s permission. For example, application developers can
use this grant type to remotely authenticate applications. Only trusted
clients must be allowed to use this grant type.

In this grant type, the client requests an access token using only the
client credentials to authenticate a request for an access token. This
**does not have support for the [refresh token
grant](../refresh-token-grant)**.

Here are the cURL commands to use the client credentials grant:

``` powershell
curl -v -X POST -H "Authorization: Basic <base64 encoded client id:client secret value>" -k -d "grant_type=client_credentials&validity_period=3600" -H "Content-Type:application/x-www-form-urlencoded" https://gateway.api.cloud.wso2.com:443/token
```

``` powershell
curl -u <client id>:<client secret> -k -d "grant_type=client_credentials&validity_period=3600" -H "Content-Type:application/x-www-form-urlencoded" https://gateway.api.cloud.wso2.com:443/token
```

You will receive a response similar to the following:

**Response**

``` java
{"token_type":"Bearer","expires_in":3600,"access_token":"ca19a540f544777860e44e75f605d927"}
```
