# Create Applications

An application is a logical representation of a physical application such as a mobile app, webapp, device, etc. If an application needs to consume an API, it should subscribe to the required API over a selected business plan. The business plan determines the usage quota allowed for the application. A single application can have multiple API subscriptions. Each application has a consumer key and consumer secret pair. The requests to the subscribed APIs are authenticated via the tokens generated using the latter mentioned security credentials.

Applications allow you to:

-   Generate and use a single key for multiple APIs.
-   Subscribe multiple times to a single API with different service level agreements (SLAs)/business plans that operate on per access token basis.

Let's take a look at the steps you need to follow to create a new application:

## Create a new application

1.  Sign in to (WSO2 API Cloud)[https://api.cloud.wso2.com] as an admin user and then access the API Store.
 
2.  Click **APPLICATIONS**.

3.  Click **ADD APPLICATION**.
    Let's create an application with the following details.
   
     <html>
        <table>
        <th>Field</th><th>Value</th>
        <tr><td>Application Name</td><td>PizzaShackApp</td></tr>
        <tr><td>Per Token Quota</td><td>10PerMin</td></tr>
        <tr><td>Description</td><td>PizzaShack Application</td></tr>
        </table>
     </html>


4.  Enter the application details and click **SAVE** to create the application. Once you successfully create an application, you will be redirected to the application overview page.

    
5.  Click **APPLICATIONS** to navigate to the Applications listing page. You will see the new application you created listed there. 

<html>
         <div class="admonition info">
         <p class="admonition-title">Note</p>
         <p>The application owner can edit or delete the application.</p>
         </div>
         </html>



