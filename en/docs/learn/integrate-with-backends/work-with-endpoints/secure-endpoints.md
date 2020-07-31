# Secure an Endpoint 

A secured endpoint is an endpoint that has access-protected resources. You have to specify the username and password when a request is sent to a secured endpoint. The endpoint authentication mechanism can either be basic authentication or digest authentication. The authentication mechanisms differ based on how the credentials are communicated and how access is granted by the backend server.

## Secure with Basic Auth

Basic Authentication is the simplest mechanism used to enforce access control on web resources. When basic authentication is used, the HTTP user agent needs to provide the user name and the password when making a request. The string containing the user name and the password separated by a colon is Base64 encoded and sent in the authorization header when calling the backend when authentication is required.


!!! info
    If the user name and password is admin, the following header will be sent to the backend.
    ```
    Authorization: Basic YWRtaW46YWRtaW4=` (where `YWRtaW46YWRtaW4=` is equivalent to Base64Encoded{admin:admin} )
    ```

When you create an API using the API Publisher, you can specify the endpoint of the API backend implementation via the **Endpoint** page as Production and Sandbox endpoints.

Follow the instructions below to use basic auth as the endpoint authentication type when using a secured endpoint:

1. Click **Endpoint** in the API Publisher.

2. Click **General Endpoint Configurations** to select the endpoint security mechanism. 
   ![](../../../assets/img/learn/work-with-endpoints/general-endpoint-detail.png)

3. Select **Basic Auth** as the endpoint authentication type and enter your credentials.

    !!! info
        The Endpoint Auth Type selected should match with the authentication mechanism supported by the secured endpoint.
   
    ![](../../../assets/img/learn/work-with-endpoints/basic-endpoint-security.png)

4. Click **SAVE.** 


## Secure with Digest Auth

Digest Authentication applies a hash function to the user name and password before sending the credentials over the network. It is a process of applying MD5 cryptographic hashing with the usage of nonce values to prevent replay attacks. It is a simple challenge-response authentication mechanism that can be used by a server to challenge a client request and by a client to provide authentication information for a secured endpoint.

!!! info
    The following is the sample format of the header that will be sent to the backend when Digest Auth is specified as the endpoint authentication type. The attributes added to the authorization header depends on the challenge header sent from the backend server.
    
    ``` java
    Authorization: Digest username="Admin", realm="admin@wso2.com", nonce="dcd98b7102dd2f0e8b11d0f600bfb0c093", uri="/dir/index.html", qop=auth, nc=00000001, cnonce="0a4f113b", response="6629fae49393a05397450978507c4ef1", opaque="5ccc069c403ebaf9f0171e9517f40e41"
    ```

Digest Authentication is safer than basic authentication, which uses unencrypted base64 encoding instead of a hashing mechanism.

When you create an API using the API Publisher, you can specify the endpoint of the API backend implementation via the **Endpoint** page as Production and Sandbox endpoints.

Follow the instructions below to use Digest Auth as the endpoint authentication type when using a secured endpoint:

1. Click **Endpoint** in the API Publisher.

2. Click **General Endpoint Configurations** to select the endpoint security scheme. 
   ![](../../../assets/img/learn/work-with-endpoints/general-endpoint-detail.png)

3. Select **Digest Auth** as the endpoint authentication type and enter your credentials.
   ![](../../../assets/img/learn/work-with-endpoints/general-endpoint-detail.png)

    !!! info

         The selected Endpoint Auth Type should match with the authentication mechanism supported by the secured endpoint.

4. Click **SAVE.**
