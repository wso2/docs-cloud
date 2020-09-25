# Customize the API Store Domain

Customizing the API Store domain makes your API store easier to find. It
is a quick and efficient way to differentiate your API Store from all
the other API Stores in WSO2 Cloud. Moreover, your company domain is an
important part of your developer community experience because
subscribers enter the API Store domain into a browser to get to your API
Store.

Follow the steps below to customize the API Store domain:

1.  Sign in to WSO2 API Cloud (
    [https://api.cloud.wso2.com](https://api.cloud.wso2.com/) ) as an
    admin user.

2.  On the API Publisher, click **Configure** and then select **Custom
    URL** from the drop-down menu.
    ![](../assets/img/customize/custom-url.png)  
    This displays the **Manage Custom Domains** page.  
    ![](../assets/img/customize/manage-custom-domains.png)

3.  Under **API Portal** , click the pencil icon to edit the existing
    **Custom Domain** of the **Store** .  
    ![](../assets/img/customize/api-portal-custom-domain.png)  
    This displays the **Modify Store Custom Domain** dialog box where
    you can specify a custom **Domain Name** for the Store.

4.  Specify a valid **Domain Name** and click **Verify** . This checks
    whether the CNAME record exists for the specified URL.  
    ![](../assets/img/customize/verify-domain-name.png)  
    If the CNAME verification is successful, you will see the following
    dialog box:  
    ![](../assets/img/customize/successfully-verified-domain-name.png)

5.  For each field, upload a valid file that satisfies the specified
    requirements.

    <table>
    <thead>
    <tr class="header">
    <th>Field</th>
    <th>Requirements</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><strong>SSL Certificate</strong></td>
    <td>This certificate file must satisfy the following requirements:
    <ul>
    <li><p>Should be in X509 format.</p></li>
    <li><p>Should not be expired.</p></li>
    <li><p>Should be issued directly or by a wild card entry for a provided custom URL. For example,</p>
    <ul>
    <li><p>In the direct method, if the CNAME is `store.wso2.com`, the issued SSL file must contain `store.wso2.com`.</p>
    </li>
    <li><p>In the wildcard method, if the CNAME is `store.wso2.com`, the issued SSL file should be `*.wso2.com`.</p></li>
    </ul></li>
    </ul></td>
    </tr>
    <tr class="even">
    <td><strong>SSL Key File</strong></td>
    <td>The private key of the certificate, which should be encrypted in the RSA format.</td>
    </tr>
    <tr class="odd">
    <td><strong>Chain File</strong></td>
    <td>The chain file to be used if the SSL connection to your custom URL fails with the <strong>SSL Certificate</strong> and <strong>SSL Key File</strong> .</td>
    </tr>
    </tbody>
    </table>

6.  Click **Proceed**. If the certificate files upload successfully,
    you will see a notification similar to the following:  
    ![](../assets/img/customize/successful-certificate-upload.png)  
    This confirms that you have successfully changed the API Store
    domain name.

    !!! tip
    
        It takes approximately 10 minutes for the changes to apply. Adding
        the configurations and restarting the load balancers can take some
        time.
    

7.  Access the API Store using your new URL. In this example, the new
    API Store URL is `https://store1.wso2stagingapps.com`.  
    ![](../assets/img/customize/updated-store-url.png)  



## Customize the API Store domain



