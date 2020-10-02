# Password Grant

You can obtain an access token by providing the resource owner's
username and password as an authorization grant. It requires the base64
encoded string of the
`                   consumer-key:consumer-secret                 `
combination. You need to meet the following prerequisites before using
the Token API to generate a token.

#### Prerequisites

-   A valid user account in the API Store.  
-   A valid consumer key and consumer secret pair. Initially, these keys
    must be generated through the API Store by clicking the **Generate**
    link on **My Subscriptions** page.

#### Invoke the Token API to generate tokens

1.  Combine the consumer key and consumer secret keys in the following format and encode the combined string using base64.
    **[consumer-key:consumer-secret](http://consumer-keyconsumer-secret)**
    Encoding to base64 can
    be done via http://base64encode.org.  
    Here's an example consumer key and secret combination:
    `wU62DjlyDBnq87GlBwplfqvmAbAa:ksdSdoefDDP7wpaElfqvmjDue`
2.  Access the Token API using a REST client such as cURL with the
    following parameters.  

    -   Token API URL -
        [https://gateway.api.cloud.wso2.com/token](https://api.cloud.wso2.com:8243/token)
        .
    -   payload -
        `grant_type=password&username=<username>&password=<password>&scope=<scope>`. Replace the `username` and `password` values as appropriate. If
        your email is `john@johns.org` and the organization key is
        `johnsorg`, then the username is **`john@johns.org@johnsorg`**
        You can find the organization key via
        https://cloudmgt.cloud.wso2.com/cloudmgt/site/pages/organization.jag
  

        !!! tip
        
                <scope\> is optional.
        
                You define scopes for your API's resources so that the resource
                can only be accessed through a token that has been issued for at
                least the scope belonging to the resource. For example, if a
                resource has a scope named 'update' and if the token is issued
                for the scopes 'read' and 'update', then the token is allowed to
                access the resource. If the token is issued for 'read' only, the
                request bearing the particular token will be blocked.
        

    -   headers -
        `Authorization: Basic <base64 encoded string>, Content-Type: application/x-www-form-urlencoded`. Replace the `<base64 encoded string>` as appropriate.

    For example, use the following cURL command to access the Token API.
    It generates two tokens as an access token and a refresh token. You
    can use the refresh token at the time a token is renewed.

    ``` java
    curl -k -d "grant_type=password&username=<username>&password=<password>" -H "Authorization: Basic <base64 encoded (consumer key:consumer secret)>" -H "Content-Type: application/x-www-form-urlencoded" https://gateway.api.cloud.wso2.com/token
    ```

    User access tokens have a fixed expiration time, which is set to 60
    minutes by default. When a user access token expires, you need to regenerate the token.

Instead of using the Token API, you can also generate access tokens from the
Devportal UI.
