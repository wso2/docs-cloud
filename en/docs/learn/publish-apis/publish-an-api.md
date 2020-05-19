# Publish an API

**API Publishing** is the process of making a created API visible in the DevPortal and available for subscription. An API that is in the CREATED state of the lifecycle will have the  API metadata added to the DevPortal, but not deployed to the API Gateway. Therefore, it will not be visible to subscribers in the DevPortal. When the API is published, it gets deployed on the API Gateway, and the API lifecycle state changes to **PUBLISHED**. 

Follow the steps below to publish an API:

1.  Sign in to WSO2 API Cloud by providing your username and password. This opens the API Publisher portal where you will see the list of created APIs. If you have not created an API yet, follow the steps [here](/learn/design-apis/design-new-rest-api/) to design a new REST API. 

2.  Click on an API that is in the **CREATED** state.

3.  Click **Lifecycle**. This displays the lifecycle state transition grid.

      <html><div class="admonition note">
      <p class="admonition-title">Note</p>
      <ul>Before you publish the API, be sure that you satisfy the following requirements:       </ul>
      <ul>
      <li>Specify an endpoint URL</li>
      <li>Select business plan(s)</li>
      </ul>
      </div>
    </html>

    
     If any of the above requirements are not satisfied, it is indicated in the lifecycle page and you have to navigate to the relevant sections and provide the missing information such as endpoint URL and business plans.
    
4.  Click **PUBLISH**. 
    
     If required, you can select the following options when publishing an API. 

     -   **Require re-subscription when publish the API** : If selected, it invalidates the current user subscriptions and forces the users to subscribe again. 
     -   **Deprecate old versions after publish the API** : If selected, all prior versions of the API that are published will be set to the DEPRECATED state automatically.

        
     If the API is published successfully, the lifecycle state should change to **PUBLISHED**.  
     
You can also navigate to the DevPortal and check whether the API that you published is visible under the **APIs** listing.
     
