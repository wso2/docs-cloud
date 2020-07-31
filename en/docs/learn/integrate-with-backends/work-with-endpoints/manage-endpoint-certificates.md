# Manage Endpoint Certificates

If your API backend is secured with a self-signed certificate (or a certificate that is not signed by a CA) you need to import the backend certificate to WSO2 API Cloud. The following topics walk you through the steps you need to follow to mange endpoint certificates. 
   


## Add a Certificate for an Endpoint

1. Sign in to the API Publisher. 

2. Create a new API or click on an existing API.

3.  Click **Endpoints** and click **General Endpoint Configuration** to expand that section.
    ![](../../assets/img/learn/work-with-endpoints/open-general-endpoint-configuration.png)
 
4.  Click **\+ Add Certificate** in the Certificates section.
   
    The Upload Certificate dialog box appears.
    ![](../../../assets/img/learn/work-with-endpoints/upload-certificate.png)

    *  Enter the following information and click **Save**.
    
        | Name        | Description                                                                              |
        |-------------|------------------------------------------------------------------------------------------|
        | Alias       | Enter a name for your certificate.                                                       |
        | Endpoint    | Select an endpoint from the dropdown list.                                                |
        | Certificate | Drag and drop the certificate file or click on the drop zone to select the certificate via the UI |
      

         The uploaded certificate will be displayed.

         ![](../../../assets/img/learn/work-with-endpoints/uploaded-certificate.png)

5.  If required, repeat step 3 onwards to add certificates to other endpoints.



## Check Certificate Information

You can check the information of the certificate, (i.e., Status and subject DN).

To view the certificate information, click the info icon that corresponds to the respective certificate.

![](../../../assets/img/learn/work-with-endpoints/check-certificate-info.png)

The selected certificate details appear.

![](../../../assets/img/learn/work-with-endpoints/certificate-details.png)


## Delete a certificate

Click on the delete icon that corresponds to the respective certificate to delete a certificate.

![](../../../assets/img/learn/work-with-endpoints/delete-certificate.png)

