# Invoke an API using cURL

The API Store has an integrated API Console via which you can read API
documentation and **invoke APIs** . Alternatively, you can use a tool
like cURL to invoke APIs.

Follow the instructions below to invoke an API using cURL, which is an open source
command-line tool and library for transferring data. 

Before you begin,

- Subscribe to an API if you have not done so already. For detailed instructions on subscribing to an API, see [Subscribe to an API](../subscribe-to-an-api).
  

Let's get started .

1.  Sign in to the API Store with your credentials.

2.  Click **Applications**. This lists all the applications you have created. 

3.  Click view to open details of the application that you used to subscribe to the API. 

4.  Click the **Production Keys** tab and then click **Generate keys**.  

    By default the Client Credentials grant type will be used to
    generate access token. Make sure the Client Credentials grant type
    is selected when generating keys from the UI.

    !!! tip
    
        You can set a token validity period in the given text box. By
        default, it is set to one hour (3600 seconds). If you set a negative
        value (e.g., -1), the token will never expire.
    
        However, this non-expiring token too can be revoked in some
        situations such as changing user password, changing the client
        secret, calling the token revoke api, authorization service provider
        detects that the tokens are compromised due to a security breach
        etc.
    
        Hence,
    
        1.  It is not recommended to hard-code such access tokens in
            client's applications on any production environment to
            communicate with the API Manager.
        2.  You should use the recommended methods of obtaining the token by
            using the relevant grant type.
        3.  Hard coding the token needs to be done with caution and if doing
            so, the application needs to be provisioned to get a new token
            in case the current hard-coded token is invalidated by the
            system.

    After the keys are generated, you can invoke the API using curl.

5.  Install [cURL](http://curl.haxx.se/download.html) if it is not there
    in your environment. Note that cURL comes by default in some
    operating systems. You can also use any other REST client.

6.  Open the command line and execute the following cURL command:

    ``` java
    curl -k -H "Authorization: Bearer <access token>" -v '<API URL>'
    ```

    Be sure to replace the placeholders as specified below:

    -   `<access token>` : Specify the token generated in step 5
    -   `<API URL>` : Click the **APIs** menu, click the API you
        want to invoke and then copy the production URL in the API's
        **Overview** tab.    
        Then, append the payload to the production URL. E.g.,
        `https://gateway.api.cloud.wso2.com:443/t/companyn3/phoneverify/1.0.0/                                                       CheckPhoneNumber?PhoneNumber=18006785432&LicenseKey=0`.

    Here's an example:

    ``` java
    curl -k -H "Authorization: Bearer 1fa22cef-c791-3105-9ac4-58511c199aa0" 'https://gateway.api.cloud.wso2.com:443/t/companyn3/phoneverify/1.0.0/CheckPhoneNumber?PhoneNumber=18006785432&LicenseKey=0'
    ```

7.  Note the result that appears on the command line.

8.  Similarly, invoke the POST method using the following cURL command:

    ``` java
    curl -k -H "Authorization: Bearer 1fa22cef-c791-3105-9ac4-58511c199aa0" --data "PhoneNumber=18006785432&LicenseKey=0" https://gateway.api.cloud.wso2.com:443/t/companyn3/phoneverify/1.0.0/CheckPhoneNumber
    ```

Now you have successfully invoked the API using cURL.
