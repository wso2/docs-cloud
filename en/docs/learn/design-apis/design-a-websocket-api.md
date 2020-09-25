# Design a WebSocket API

WebSocket is a protocol similar to HTTP and is part of the HTML5 specification. It enables simultaneous two-way communication (full-duplex communication) between the client and the server over a single connection. 

The WebSocket protocol is designed to achieve the following:

-   Reduce unnecessary network traffic and latency.
-   Allow streaming through proxies and firewalls while simultaneously supporting upstream and downstream communication.
-   Be backward compatible with the pre-WebSocket world by starting up as an HTTP connection before switching to WebSocket frames.

A WebSocket API allows an API creator to expose a WebSocket backend as an API to offer services via a WebSocket protocol while providing OAuth security, Throttling, Analytics, etc.

Follow the instructions below to design a WebSocket API.

1. Sign in to WSO2 API Cloud. This opens the API Publisher portal.

2. Close the interactive tutorial that starts automatically if you are
    a first-time user, and then click **ADD NEW API**.

3. Select **Design a New WebSocket API** and then click **Start Creating**.

4.  Specify the following as details of the new WebSocket API.
 
     1. On the **Design** tab, specify the following and then click **Next: Implement**.

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
         </tbody>
         </table>

     2. On the **Implement** tab, click **Managed API** to expand the section, specify the following and then click **Next: Manage**:

         <table>
         <thead>
         <tr>
         <td>Endpoint</td>
         <td><p>
          Use one of the following endpoints.
         <ul>
         <li>ws://echo.websocket.org:80</li>
         <li>wss://echo.websocket.org:443</li>
         </ul></td>
         </tr>
         </tbody>
         </table>
 
     3. On the **Manage** tab, under **Throttling Settings**, select `Gold` and `silver` as the **Subscription Tiers**.


5.  Click **Save**. This displays the overview page of the created WebSocket API.

Now you have successfully created and configured a WebSocket API, which you can publish to the API Store.
