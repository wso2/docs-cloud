# Secure APIs using Mutual SSL

In contrast to the usual one-way SSL authentication where a client verifies the identity of the server, in mutual SSL the server validates the identity of the client so that both parties trust each other. This builds a system that has a very tight security and avoids any requests made to the client to provide the username/password, as long as the server is aware of the certificates that belong to the client.

This section describes how you can create an API secured with mutual SSL and then invoke the secured API via the Devportal.

### Create an API Secured with Mutual SSL

1.  Create an API and navigate to the **Runtime Configurations** tab.
2.  Select **Mutual SSL**.
    ![](../../../assets/img/learn/secure-apis/enable-mutual-ssl.png)

3.  Click **Upload Certificate** to upload a new client certificate.
    
    !!! note
        This feature currently supports only the `.crt` format for certificates.

        If you need to use a certificate in any other format, you can convert it using a standard tool before uploading.

4.  Provide an alias and public certificate. Select the tier that should be used to throttle out the calls using this particular client certificate and click **Upload** .
    ![](../../../assets/img/learn/secure-apis/upload-certificate.png)
    
5.  **Save** the API
    
### Invoke an API secured with Mutual SSL using Postman

1.  Import the certificate and private key to Postman. Navigate to certificates tab in Postman settings.
    
    ![](../../../assets/img/learn/secure-apis/add-certificate-to-postman.png)
    
    Add the certificate and private key.
    ![](../../../assets/img/learn/secure-apis/provide-crt-and-private-key.png)
    
2.  Invoke the API from Postman.

#### Limitations

Following are the known limitations for this feature:

-   Application subscription is not permitted for APIs that are only protected with mutual SSL. Hence, subscription/application level throttling is not applicable for these type of APIs.

-   Resource level throttling is not applicable for the APIs that are only protected with mutual SSL.

-   Resource level security will not be applicable for the APIs that are only protected with mutual SSL.

-   Scope level security will not be applicable for the APIs that are only protected with mutual SSL.
