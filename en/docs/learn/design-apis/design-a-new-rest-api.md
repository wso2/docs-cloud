# Design a New REST API

**API creation** is the process of linking an existing backend API implementation to the API Publisher, so that you can manage the API's lifecycle, documentation, security, community, and subscriptions. Alternatively, you can provide the API implementation in-line in the API Publisher itself.

Follow the instructions below to design a new REST API:

1. Sign in to WSO2 API Cloud. This opens the API Publisher portal.

2. Close the interactive tutorial that starts automatically if you are
    a first-time user, and then click **ADD NEW API**.

3. Select **Design a New REST API** and then click **Start Creating**. 

4. Specify the following as details of the API:

    1. On the **Design** tab specify the following and click **Next: Implement**:  
    
        <table><colgroup> <col/> <col/> <col/> </colgroup><tbody><tr><th colspan="2" >Field</th><th >Sample value</th></tr><tr><td colspan="2" class="confluenceTd">Name</td><td class="confluenceTd">PizzaShack</td></tr><tr><td colspan="2" class="confluenceTd">Context</td><td class="confluenceTd"><div class="content-wrapper"><p><code>/pizzashack</code></p><div><div class="confluence-information-macro-body"><p>The API context is used by the Gateway to identify the API. Therefore, the API context must be unique. This context is the API's root context when invoking the API through the Gateway.</p></div><div class="confluence-information-macro confluence-information-macro-tip"><span class="aui-icon aui-icon-small aui-iconfont-approve confluence-information-macro-icon"></span><div class="confluence-information-macro-body"><p>You can define the API's version as a parameter of its context by adding the <code>{version}</code> into the context. For example, <code>{version}/pizzashack</code>. WSO2 API Cloud assigns the actual version of the API to the <code>{version}</code> parameter internally. For example, <code>https://localhost:8243/1.0.0/pizzashack</code>. Note that the version appears before the context, allowing you to group your APIs based on the versions.</p></div></div></div></div></td></tr><tr><td colspan="2" class="confluenceTd">Version</td><td colspan="1" class="confluenceTd">1.0.0</td></tr><tr><td colspan="2" class="confluenceTd">Resources</td><td colspan="1" class="confluenceTd">URL Pattern: menu<br/>Request Type: GET</td></tr></tbody></table>
        
    2. On the **Implement** tab click **Managed API**, then specify the following and click **Next: Manage**:
        <table><colgroup> <col/> <col/> <col/> </colgroup><tbody><tr><th colspan="2" >Field</th><th >Sample value</th></tr><tr><td colspan="2" class="confluenceTd">Endpoint Type</td><td colspan="1" class="confluenceTd">HTTP/REST Endpoint</td></tr><tr><td colspan="2" class="confluenceTd">Endpoint</td><td colspan="1" rel="nofollow">https://localhost:9443/am/sample/pizzashack/v1/api/</a></p><p>The endpoint that you add is automatically added as the production and sandbox endpoints.</p></td></tr></tbody></table>

    3. On the **Manage** tab select `Unlimited` as the **Subscription Tier**. 
     

5.  Click **Save**.     


Now, you have successfully designed a REST API. which you can publish to the API Store.


       