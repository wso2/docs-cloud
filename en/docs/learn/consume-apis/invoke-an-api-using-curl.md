# Invoke an API using cURL

The API Store has an integrated API Console using which you can read API
documentation and **invoke APIs** . Alternatively, you can use a tool
like cURL to invoke APIs.

**In this tutorial** , you invoke an API using cURL, the open source
command-line tool and library for transferring data. The examples here
use the `PhoneVerification` API, which is created
in section Create and Publish an API .
    

Let's get started .

1.  Log in to the API Store using the URL
    **`http://<hostname>/Store?tenant=<tenant_name>`**
    and click the API that you want to subscribe to.

2.  Click the **APPLICATIONS** menu and click **ADD APPLICATION** to
    create a new application.  

3.  Give a name and a tier for the application and click **Add**.  
    
4.  Go back to the API's subscription options and select the application
    you just created, the Bronze tier, and click **Subscribe**.

5.  When prompted, choose to view subscriptions. Then, go to the
    **Production Keys** tab and click **Generate keys**.

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
    
          
    

    Let's invoke the API that you just subscribed to.

6.  Install [cURL](http://curl.haxx.se/download.html) if it is not there
    in your environment. Note that cURL comes by default in some
    operating systems. You can also use any other REST client.

7.  Open the command line and execute the following cURL command:

    ``` java
    curl -k -H "Authorization: Bearer <access token>" -v '<API URL>'
    ```

    Be sure to replace the placeholders as follows:

    -   **\<access token\>** : Give the token generated in step 5
    -   **\<API URL\>** : Click the **APIs** menu, click the API you
        want to invoke and then copy the production URL in the API's
        **Overview** tab.    
        Then, append the payload to the production URL. E.g.,
        `https://gateway.api.cloud.wso2.com:443/t/companyn3/phoneverify/1.0.0/                                                       CheckPhoneNumber?PhoneNumber=18006785432&LicenseKey=0`.

    Here's an example:

    ``` java
        curl -k -H "Authorization: Bearer 1fa22cef-c791-3105-9ac4-58511c199aa0" 'https://gateway.api.cloud.wso2.com:443/t/companyn3/phoneverify/1.0.0/CheckPhoneNumber?PhoneNumber=18006785432&LicenseKey=0'
    ```

8.  Note the result that appears on the command line.

9.  Similarly, invoke the POST method using the following cURL command:

    ``` java
        curl -k -H "Authorization: Bearer 1fa22cef-c791-3105-9ac4-58511c199aa0" --data "PhoneNumber=18006785432&LicenseKey=0" https://gateway.api.cloud.wso2.com:443/t/companyn3/phoneverify/1.0.0/CheckPhoneNumber
    ```

In this tutorial, you subscribed to an API and invoked it using cURL.
