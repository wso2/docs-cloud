# Subscribe to an API

APIs Published in WSO2 API Cloud are secured with OAuth tokens. Therefore, an API consumer should first subscribe to the API and generate an OAuth token before invoking the API. To subscribe to an API, you need to create an application.

Follow the instructions below try out subscribing to an API: 

1.  Sign in to (WSO2 API Cloud)[https://api.cloud.wso2.com] with your credentials. This opens the API Publisher portal.

2.  On the API Publisher, click an API to open it.
    <html>
         <div class="admonition info">
         <p class="admonition-title">Note</p>
         <p>Here we use the `PhoneVerification` API that is created by following the tutorial  [create and publish an API](../../tutorials/create-and-publish-an-api). </p> 
         </div>
     </html>   

3.  the **Overview** tab of the API, click **View in Store**. This takes you to the `PhoneVerification` API overview page in the API Store. Note the subscription options on the right-hand side of the page.
    
4.  Under **Applications** select **New Application**. This takes you to the **Add Application** page.

5.  Specify the following values and click **Add** to register an OAuth2.0 application, which you can use to consume the `PhoneVerification` API.

    <table>
         <tr> 
         <th>
         Name
         </th>
         <td>
         TestApp
         </td>
         </tr>
         <tr> 
         <th>Per Token Quota
         </th>
         <td>50PerMin
         </td>
         </tr>
         </table>
       This displays a message requesting whether you want to return to the API detail page. Click **Yes**. 

5.  On the API detail page, 
    - Under **Applications**, select the newly created `TestApp` application.
    - Under **Tiers**, select `Bronze`.

6.  Click **Subscribe**.  

This subscribes the `TestApp` application to the `PhoneVerification` API on the selected business plan, and displays a message that you have successfully subscribed.

Now if you want to invoke the `PhoneVerification` API, you can generate production keys for the `TestApp` application and test it with the access token that you generated. 

