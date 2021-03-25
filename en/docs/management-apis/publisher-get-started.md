# Get Started to Invoke Publisher APIs

The RESTful APIs exposed from WSO2 API Cloud's Publisher portal are implemented as CXF REST web applications based on REST best practices and specifications. API development is started with a Swagger specification with a contract-first approach. See the [full swagger definition](https://github.com/wso2/docs-cloud/blob/master/en/docs/management-apis/restapis/publisher-v1.yaml) written using swagger 2.0. This can be also retrieved from the Web app itself using the URL `https://<host-name[:port]>/api/am/publisher/swagger.json`


The API comes with a pluggable security mechanism. Since API security is implemented as a CXF handler, if you need to plug a custom security mechanism, you can write your own handler and add it to the web service.

Before invoking the API with the access token, you need to obtain the consumer key/secret key pair by calling the dynamic client registration endpoint. You can request an access token with the preferred grant type. An example is shown below,

```
curl -X POST -H "Authorization: Basic base64encode(email_username@Org_key:password)" -H "Content-Type: application/json" -d @payload.json https://gateway.api.cloud.wso2.com/client-registration/register
```

####Sample request:

```
{
    "callbackUrl": "www.google.lk",
    "clientName": "rest_api_publisher",
    "tokenScope": "Production",
    "owner": "email_username@Org_key",
    "grantType": "password refresh_token",
    "saasApp": true
}
```

####Sample response:

```
{
    "callBackURL": "www.google.lk",
    "jsonString":
    "{
    \"username\":\"email_username@Org_key\",
    \"redirect_uris\":\"www.google.lk\",
    \"tokenScope\":[Ljava.lang.String;@3a73796a,
    \"client_name\":\"admin_rest_api_publisher\",
    \"grant_types\":\"authorization_code password refresh_token iwa:ntlm
    urn:ietf:params:oauth:grant-type:saml2-bearer client_credentialsimplicit\"
    }",
    "clientName": null,
    "clientId": "HfEl1jJPdg5tbtrxhAwybN05QGoa",
    "clientSecret": "l6c0aoLcWR3fwezHhc7XoGOht5Aa"
}
```

During the API invocation process request, you need to invoke the CXF handler first, which calls an introspection API to validate the token. Then generate the access token using the already created OAuth application. A sample call to generate the access token is given below:

**Note**: Access token must be generated using the correct scope for the resource. Scope for each resource is given in the resource documentation.

**Note**: The consumer key and consumer secret keys must be Base64 encoded in the format `consumer-key:consumer-secret`

```
curl -k -d "grant_type=password&username=email_username@Org_key&password=admin&scope=apim:api_view" -H "Authorization: Basic SGZFbDFqSlBkZzV0YnRyeGhBd3liTjA1UUdvYTpsNmMwYW9MY1dSM2Z3ZXpIaGM3WG9HT2h0NUFh" https://gateway.api.cloud.wso2.com/token
```

####Token response:

```
{
   "scope":"apim:api_view",
   "token_type":"Bearer",
   "expires_in":3600,
   "refresh_token":"33c3be152ebf0030b3fb76f2c1f80bf8",
   "access_token":"292ff0fd256814536baca0926f483c8d"
}
```

Now you have a valid access token that you can use to invoke an API. Navigate through the API descriptions to find the required API, obtain an access token as described above and invoke the API with the authentication header. If you use a different authentication mechanism, this process may change.

**Note**: The implementation of WSO2 API Cloud is similar to DCR. Since retrieve client application, edit, and delete is only available in DCRM specifications, you cannot perform these actions using REST APIs. 
