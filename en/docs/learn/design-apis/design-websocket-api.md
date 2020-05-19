# Design a WebSocket API

WebSocket is a protocol similar to HTTP and is part of the HTML5 specification. It enables simultaneous two-way communication (full-duplex communication) between the client and the server over a single connection. 

The WebSocket protocol is designed to achieve the following:

-   Reduce unnecessary network traffic and latency.
-   Allow streaming through proxies and firewalls while simultaneously supporting upstream and downstream communication.
-   Be backward compatible with the pre-WebSocket world by starting up as an HTTP connection before switching to WebSocket frames.

A WebSocket API allows an API creator to expose a WebSocket backend as an API to offer services via a WebSocket protocol while providing OAuth security, Throttling, Analytics, etc.

Follow the instructions below to design a WebSocket API.

1. Sign in to WSO2 API Cloud. This opens the API Publisher portal.

2.  Click **CREATE API** and then click **Design a New WebSocket API**.

3.  Specify the details of the new WebSocket API.

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
    

    <html>
     <div class="admonition note">
     <p class="admonition-title">Note</p>
     <p>The **CREATE & PUBLISH** option will appear only if the optional fields **Endpoint** and **Business plan(s)** are provided by a user who has <code>publisher</code> permission. You need to add a Name, Context, Version, and a valid Endpoint (For non-secured WebSockets enter the protocol as <code>ws://</code>  or for secured WebSockets enter the protocol as <code>wss://</code>) to create the API.</p>
     </div>
     </html>

4.  Click **CREATE** or **CREATE & PUBLISH**. This displays the overview page of the created WebSocket API.


5.  Optionally, enter the endpoint configurations.

     1. Click **Endpoint**.
     
     2. Click on the cogwheel icon, which is inline with the endpoint that you need to configure, and update the endpoint related configurations as required. 
     

Now you have successfully created and configured a WebSocket API. Next, let's publish the API.

