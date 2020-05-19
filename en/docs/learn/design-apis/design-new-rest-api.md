# Design a New REST API

**API creation** is the process of linking an existing backend API implementation to the API Publisher, so that you can manage the API's lifecycle, documentation, security, community, and subscriptions. Alternatively, you can provide the API implementation in-line in the API Publisher itself.

Follow the instructions below to design a new REST API:

1. Sign in to WSO2 API Cloud. This opens the API Publisher portal.

2. Click **CREATE API** and then click **Design a New REST API**.

3. Specify the details of the API. 
    
     <table><colgroup> <col/> <col/> <col/> </colgroup><tbody><tr><th colspan="2" >Field</th><th >Sample value</th></tr><tr><td colspan="2" class="confluenceTd">Name</td><td class="confluenceTd">PizzaShack</td></tr><tr><td colspan="2" class="confluenceTd">Version</td><td colspan="1" class="confluenceTd">1.0.0</td></tr><tr><td colspan="2" class="confluenceTd">Context</td><td class="confluenceTd"><div class="content-wrapper"><p><code>/pizzashack</code></p><div><div class="confluence-information-macro-body"><p>The API context is used by the Gateway to identify the API. Therefore, the API context must be unique. This context is the API's root context when invoking the API through the Gateway.</p></div><div class="confluence-information-macro confluence-information-macro-tip"><span class="aui-icon aui-icon-small aui-iconfont-approve confluence-information-macro-icon"></span><div class="confluence-information-macro-body"><p>You can define the API's version as a parameter of its context by adding the <code>{version}</code> into the context. For example, <code>{version}/pizzashack</code>. WSO2 API Cloud assigns the actual version of the API to the <code>{version}</code> parameter internally. For example, <code>https://localhost:8243/1.0.0/pizzashack</code>. Note that the version appears before the context, allowing you to group your APIs based on the versions.</p></div></div></div></div></td></tr><tr><td colspan="2" class="confluenceTd">Endpoint</td><td colspan="1" rel="nofollow">https://localhost:9443/am/sample/pizzashack/v1/api/</a></p><p>The endpoint that you add is automatically added as the production and sandbox endpoints.</p></td></tr></tbody></table>
        
     <html>
     <div class="admonition note">
     <p class="admonition-title">Note</p>
     <p>The <b>CREATE & PUBLISH</b> option will only appear when a user who has <code>publisher</code> permission adds the details for the <b>Endpoint</b> and <b>Business plan(s)</b>, which are optional fields.</p>
     </div>
     </html>
     

4.  Click **CREATE** or **CREATE & PUBLISH** to create the API. This displays the overview page of the newly created API.     

5. Configure the API design configurations.

     1. Click **Design Configurations**.

         <html><div class="admonition note">
         <p class="admonition-title">Note</p>
         <p>By default, **All** users who have `creator` permission are allowed **Publisher Access Control** and public **Developer Portal visibility**.</p>
         <p>
         </div>
         </html>

     2. Add a tag and press enter.
   
         Let's add a tag named **pizza**.

         <html>
         <div class="admonition info">
         <p class="admonition-title">Info</p>
         <p>Tags can be used to filter out APIs matching specific search criteria. It is a good practice to add tags that explain the functionality and purpose of the API so that subscribers can search for APIs based on the tags.</p>
         </div>
         </html>

     3. Optionally, select **Yes** as the **Make this the Default Version** option.
   
         When an API is the default version -

         -  The API will be available in the Gateway without a version specified in the production and sandbox URLs.  
         -  You to create a new version of this API and set it as the default version. Thereafter, the same resources can be invoked in the client applications without changing the API gateway URL. 
         -  You can create new versions of an API with changes, while at the same time allowing the existing client applications to be invoked without the client having to change the URLs.

     4. Click **Save**.

6. Configure the runtime configurations.

     1. Click **Runtime Configurations**. 

         Transport Level Security  defines the transport protocol on which the API is exposed.  


       2. If you wish to limit the API availability to only one transport (e.g., HTTPS), uncheck the **Transport Level Security** checkbox.
           
           Both HTTP and HTTPS transports are selected by default.

7. Configure the resources.

     By default, the API will have five resources with `/*` as the URL pattern.

     1. Click **Show More** to navigate **Resource** page.


      2. Modify the resources as follows and click **SAVE** to update the resources.

          1. Click delete as shown in the image below. This remove all the existing resources.

          2. Click **(+)** to add a new resource.
      
             The newly added resource is displayed as follows:

3. Expand the created **GET** operation to add **Summary and Description** and **Operation governance**.

     In addition, you can add the resource **Parameters** using the **Parameters** section.

    
     You can define the following parameter types based on the resource parameters that you add.

     | Parameter Type                          | Description                                                                                                                                                                                     |
     |-----------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
     | `query`| Contains the fields added as part of the invocation URL that contains the data to be used to call the backend service.                                                                             |
     | `header`| Contains the case-sensitive names followed by a colon (:) and then by its value that carries additional information with the request, which defines the operating parameters of the transaction. |
     | `cookie` | Operations can also pass parameters in the Cookie header, as `Cookie: name=value`. Multiple cookie parameters are sent in the same header, separated by a semicolon and space.                                                                                            |
     | `body`| An arbitrary amount of data of any type is sent with a POST message.                                                                                                                                |

4. Optionally view the API definition.

     Click **API Definition**. The OpenAPI Specification (a.k.a Swagger definition) for the PizzaShack API appears.


Now, you have successfully designed a REST API. Next, let's Publish the API.


       