# Secure APIs using Basic Authentication

Basic authentication is a simple HTTP authentication scheme in which the request will contain an authorization header with a valid  base64 encoded username and password. The WSO2 API Manager is able to authenticate requests using Basic and OAuth2 authentication 
schemes. In addition to using these schemes individually, it is also possible to use 
the OAuth2 and Basic schemes at the same time. 

The following topics describe how to work with basic authentication:

## Enable basic authentication for an API

Basic authentication is an API level configuration. 

Follow the steps below to configure basic authentication:

1. Sign in to the API Publisher and click on an API for which you need to configure basic authentication. 

2. Configure basic authentication as follows under the **Application Level Security** section in the **Runtime Configuration** of the **API Details** page:

    ![](../../../assets/img/learn/secure-apis/basic_authentication.png)


## Understand multiple authentication schemes

WSO2 API Cloud can authenticate requests using mutual SSl, basic auth, OAuth2 and API key authentication schemes. 
In addition to using these schemes individually, it is also possible to use multiple schemes at the same time.

 
- If you enable multiple schemes, the priority will be given in the order of mutual SSL, OAuth2, basic auth and API key. 
When it comes to OAuth2, basic auth, and API key schemes, API Cloud will authenticate with only one authentication scheme based on the above order.

- Mutual SSL is treated as a transport level authentication scheme and it is considered to be different from the application security schemes.

- You are required to specify either mutual SSL or OAuth2/Basic auth/API key as a mandatory scheme. If you do not specify a mandatory scheme, authentication will be skipped.
  <html>
         <div class="admonition info">
         <p class="admonition-title">Note</p>
         <p>If OAuth2/basic auth is set as the mandatory scheme, the request will be authenticated using only one of the schemes.</br>
i.e., if authentication using the OAuth2 scheme is attempted and fails, only then basic authentication will be applied.</p>
         </div>
         </html>


##Invoke an API using basic authentication

Use the cURL command below to invoke the API:

``` bash tab="Format"
curl -k -X GET "<API_URL>" -H  "accept: application/json" -H  "Authorization: Basic base64(username:password)"
```

``` bash tab="Example"
curl -k -X GET "https://localhost:8243/pizzashack/1.0.0/menu" -H  "accept: application/json" -H  "Authorization: Basic c2hhbmk6c2hhbmkxMjM="
```

## Basic authentication with scopes

WSO2 API Cloud allows you to configure scopes with role bindings, which can associate with API resources. Basic authentication uses credentials of the user to authenticate with basic authentication protected APIs.

If you associate an API resource with scopes protected with the basic authentication scheme, API Cloud will perform the role validation of the defined scopes in the resource against the authenticated user roles.