# Create and Publish a WebSocket API

Follow the instructions in this tutorial to design and publish an API with a WebSocket backend and then invoke it using the **wscat** WebSocket client.


### Step 1 - Design a WebSocket API

1. Sign in to WSO2 API Cloud. This opens the API Publisher portal.
   

2.  Click **CREATE API** and then click **Design a New WebSocket API**.

     <html><div class="admonition note">
      <p class="admonition-title">Note</p>
      <p>The <b>CREATE</b> button will only appear for a user who has the <code>creator</code> role permission.</p>
      </div>
     </html>
    
     ![](../../assets/img/tutorials/create-websocket-api.png)

3.  Specify the following as details of the new WebSocket API.

    <table>
    <thead>
    <tr>
    <th>Field</th>
    <th>Sample value</th>
    </tr>
    </thead>
    <tbody>
    <tr>
    <td>Name</td>
    <td>EchoWebSocket</td>
    </tr>
    <tr>
    <td>Context</td>
    <td>/echowebsocket</td>
    </tr>
    <tr>
    <td>Version</td>
    <td>1.0</td>
    </tr>
    <tr>
    <td>Endpoint</td>
    <td><p>
    Use one of the following endpoints.
    <ul>
    <li>ws://echo.websocket.org:80</li>
    <li>wss://echo.websocket.org:443</li>
    </ul></td>
    </tr>
    <tr>
    <td>Business Plan</td>
    <td>Gold, Silver</td>
    </tr>
    </tbody>
    </table>
    
    ![](../../assets/img/tutorials/specify-websocket-api-values.png)

    <html>
     <div class="admonition note">
     <p class="admonition-title">Note</p>
     <p>The **CREATE & PUBLISH** option will appear only if the optional fields **Endpoint** and **Business plan(s)** are provided by a user who has <code>publisher</code> permission. You need to add a Name, Context, Version, and a valid Endpoint (For non-secured WebSockets enter the protocol as <code>ws://</code>  or for secured WebSockets enter the protocol as <code>wss://</code>) to create the API.</p>
     </div>
     </html>

4.  Click **CREATE** or **CREATE & PUBLISH**. 

     The overview page of the created WebSocket API appears.

     ![](../../assets/img/tutorials/overview-websocket-api.png)

5.  Optionally, enter the endpoint configurations.

     1. Click **Endpoint**.
     
     2. Click the **Endpoint Advanced Configurations** link as shown below and update the endpoint related configurations as required.

         ![](../../assets/img/tutorials/endpoint-view-of-websocket-api.png)

Now, you have created and configured the WebSocket API successfully.

### Step 2 - Publish the WebSocket API

Click **LIFECYCLE** to navigate to the API lifecycle and click **PUBLISH** to publish the API to the API Developer Portal.

### Step 3 - Invoke a WebSocket API

1. Sign in to the **DEVELOPER PORTAL**.

2. Click on the WebSocket API.
   
     The API overview appears.

3. Subscribe to the API.

    1. Click **KEY GENERATION WIZARD**.
    
         This wizard takes you through the steps of creating a new application, subscribing, generating keys, and generating an access token to invoke the API. 

         <div class="admonition note">
         <p class="admonition-title">Note</p>
         <p> 
         You can use any application (e.g., JWT or OAuth) to subscribe to the API.
         </p>
         </div>

         ![](../../assets/img/tutorials/websocket-api-credential-page.png)

    2. Copy the authorization token that appears.

         ![](../../assets/img/tutorials/websocket-api-key-generation-wizard.png)

4. Try out the operations.

    1. Install wscat client. 

         `npm install -g wscat`

    2. Invoke the API using following command.
        
         ``` java tab="WS"
         wscat -c ws://localhost:9099/echowebsocket/1.0.0 -H "Authorization: Bearer [accesstoken]" 
         ```

         ``` java tab="WSS"
         wscat -c wss://localhost:8099/echowebsocket/1.0.0 -H "Authorization: Bearer [accesstoken]"
         ```

      <html>
      <div class="admonition note">
      <p class="admonition-title">Note</p>
      <p><b>BasicAuth</b> and <b>API Keys</b> do not work as security schemes for WebSocket APIs.</p>
      </div> 
      </html>

You have successfully created and published your first WebSocket API, subscribed to it, obtained an access token for testing, and tested your API with the access token.
