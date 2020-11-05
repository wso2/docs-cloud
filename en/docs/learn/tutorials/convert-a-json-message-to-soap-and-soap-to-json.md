# Convert a JSON Message to SOAP and SOAP to JSON

<html>
         <div class="admonition info">
         <p class="admonition-title">Note</p>
         <p>This tutorial uses the [WSO2 API Manager Tooling
    Plug-in](https://docs.wso2.com/display/AM260/Installing+the+API+Manager+Tooling+Plug-In).</p> 
         </div>
</html> 

WSO2 API Cloud comes with a powerful mediation engine that can transform
and orchestrate API calls on the fly. It is built on the WSO2 ESB and
supports a variety of mediators that you can use as building blocks for
your sequences.

You can provide an extension as a synapse mediation sequence to the API
Gateway's default mediation flow to transform message formats.

In this tutorial you convert a request message with a JSON payload
and a REST URL to a SOAP message, send it to the backend and then
convert the request from the backend to JSON.

The examples here use the `PhoneVerification` API,
which is created by following the tutorial [Create and Publish an
API](../create-and-publish-an-api). If you do not have this API or the
existing one is deprecated, simply create a new API with the backend as
<http://ws.cdyne.com/phoneverify/phoneverify.asmx>. It accepts both
SOAP and REST requests as shown
[here](http://ws.cdyne.com/phoneverify/phoneverify.asmx?op=CheckPhoneNumber).

Let's get started.

1.  Sign in to WSO2 API Cloud with your credentials. This opens the API Publisher.

2.  Click to edit the
    `PhoneVerification` API.  
    ![](../../assets/img/learn/tutorials/edit-api.png)

3.  Add the following resource to the API.

    !!! tip
    
        The resource you create here invokes the [SOAP 1.2 Web
        service of the
        backend](http://ws.cdyne.com/phoneverify/phoneverify.asmx?op=CheckPhoneNumber).
        Therefore, the recommended method is HTTP POST. As you do not
        include the payload in a query string, avoid giving any specific
        name in the URL pattern, which will be amended to the actual backend
        URL.
    

    <table>
    <thead>
    <tr class="header">
    <th>Field</th>
    <th>Sample value</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Resources</td>
    <td>URL pattern: /*</td>
    </tr>
    <tr class="even">
    <td><br />
    </td>
    <td>Request types: POST</td>
    </tr>
    </tbody>
    </table>

    ![](../../assets/img/learn/tutorials/api-definition.png)
   

4.  After the resource is added, expand it and note a parameter by the
    name **payload** already available. You can use this parameter to
    pass the payload to the backend. Edit its values as follows:

    | Parameter name | Description                           | Parameter Type | Data Type | Required |
    |----------------|---------------------------------------|----------------|-----------|----------|
    | payload        | Pass the phone number and license key | body           | Empty     | True     |

    ![](../../assets/img/learn/tutorials/payload-parameter.png)

    Next, let's write a sequence to convert the JSON payload to a SOAP
    request. We do this because the backend accepts SOAP requests.

5.  Navigate to the **Implement** page and change the endpoint of the
    API to <http://ws.cdyne.com/phoneverify/phoneverify.asmx?WSDL> .
    Once the edits are done, click **Save** .  
    ![](../../assets/img/learn/tutorials/save-changes.png) 

6.  Download and install the [WSO2 API Manager Tooling
    Plug-in](https://docs.wso2.com/display/AM260/Installing+the+API+Manager+Tooling+Plug-In)
    if you have not done so already. Open Eclipse by double clicking the
    `Eclipse.app` file inside the downloaded
    folder.

7.  Click **Window \> Open Perspective \> Other** to open the Eclipse
    perspective selection window. Alternatively, click **Open
    Perspective** on the top, right-hand corner.  
    ![](../../assets/img/learn/tutorials/open-perspective.png)

8.  On the dialog box that appears, select **WSO2 APIManager** and click
    **OK** .  
    ![](../../assets/img/learn/tutorials/select-api-manager.png)

9.  On the APIM perspective, click **Sign in** as shown below.
    ![](../../assets/img/learn/tutorials/sign-in.png)

10. On the **Add Registry** dialog box that opens, specify your cloud user name (in the
    format `<email@company_name>`) and password,
    and click **OK**.

    ![](../../assets/img/learn/tutorials/add-registry.png)

11. On the tree view that is displayed, expand the folder structure of the
    existing API.

12. Right click on the `in` sequence folder and click
    **Create** to create a new `in` sequence.  
    ![](../../assets/img/learn/tutorials/create-in-sequence.png)
 
13. Name the sequence as `JSONtoSOAP`. 
    Your sequence will now be visible on the APIM perspective.  

14. Under the
    **Mediators** section, drag and drop a **PayloadFactory**
    mediator to your sequence and specify the following values.

    !!! tip
    
        The **PayloadFactory** mediator transforms the content of
        your message. The `<args>` elements define
        arguments that retrieve values at runtime by evaluating the provided
        expression against the SOAP body. You can configure the format of
        the request/response and map it to the arguments.
    
        For example, in the following configuration, the values for the
        format parameters `PhoneNumber` and
        `LicenseKey` will be assigned with values that
        are taken from the `<args>` elements
        (arguments,) in that particular order.
    
        For details on how you got this configuration, see [PayloadFactory
        Mediator](https://docs.wso2.com/enterprise-service-bus/PayloadFactory+Mediator)
        in the WSO2 ESB documentation.
    
      
    ![](../../assets/img/learn/tutorials/payloadfactory-mediator.png)

    <table>
    <tbody>
    <tr class="odd">
    <td>Payload</td>
    <td><div class="content-wrapper">
    <div class="code panel pdl" style="border-width: 1px;">
    <div class="codeContent panelContent pdl">
    <div class="sourceCode" id="cb1" data-syntaxhighlighter-params="brush: xml; gutter: false; theme: Confluence" data-theme="Confluence" style="brush: xml; gutter: false; theme: Confluence"><pre class="sourceCode xml"><code class="sourceCode xml"><a class="sourceLine" id="cb1-1" title="1"><span class="kw">&lt;soap12:Envelope</span><span class="ot"> xmlns:xsi=</span><span class="st">&quot;http://www.w3.org/2001/XMLSchema-instance&quot;</span><span class="ot"> xmlns:xsd=</span><span class="st">&quot;http://www.w3.org/2001/XMLSchema&quot;</span><span class="ot"> xmlns:soap12=</span><span class="st">&quot;http://www.w3.org/2003/05/soap-envelope&quot;</span><span class="kw">&gt;</span></a>
    <a class="sourceLine" id="cb1-2" title="2">    <span class="kw">&lt;soap12:Body&gt;</span></a>
    <a class="sourceLine" id="cb1-3" title="3">        <span class="kw">&lt;CheckPhoneNumber</span><span class="ot"> xmlns=</span><span class="st">&quot;http://ws.cdyne.com/PhoneVerify/query&quot;</span><span class="kw">&gt;</span></a>
    <a class="sourceLine" id="cb1-4" title="4">             <span class="kw">&lt;PhoneNumber&gt;</span>$1<span class="kw">&lt;/PhoneNumber&gt;</span></a>
    <a class="sourceLine" id="cb1-5" title="5">             <span class="kw">&lt;LicenseKey&gt;</span>$2<span class="kw">&lt;/LicenseKey&gt;</span></a>
    <a class="sourceLine" id="cb1-6" title="6">        <span class="kw">&lt;/CheckPhoneNumber&gt;</span></a>
    <a class="sourceLine" id="cb1-7" title="7">     <span class="kw">&lt;/soap12:Body&gt;</span></a>
    <a class="sourceLine" id="cb1-8" title="8"><span class="kw">&lt;/soap12:Envelope&gt;</span></a></code></pre></div>
    </div>
    </div>
    </div></td>
    </tr>
    <tr class="even">
    <td>Args</td>
    <td><p>Give the following arguments:</p>
    <div class="table-wrap">
    <table>
    <colgroup>
    <col style="width: 33%" />
    <col style="width: 33%" />
    <col style="width: 33%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Type</th>
    <th>Value</th>
    <th>Evaluator</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>expression</td>
    <td><div class="line number14 index13 alt1">
    <code class="sourceCode java">                     <span class="co">//request/PhoneNumber                    </span></code>
    </div></td>
    <td>xml</td>
    </tr>
    <tr class="even">
    <td>expression</td>
    <td><code class="sourceCode java">                    <span class="co">//request/LicenseKey                   </span></code></td>
    <td>xml</td>
    </tr>
    </tbody>
    </table>
    </div></td>
    </tr>
    </tbody>
    </table>

15. Similarly, add a **Property** mediator to the same sequence and give
    the following values to the property mediator.  
    ![](../../assets/img/learn/tutorials/property-mediator.png)

    |                |                      |
    |----------------|----------------------|
    | Property Name  | messageType          |
    | Value Type     | Literal              |
    | Value          | application/soap+xml |
    | Property Scope | axis2                |

16. Save the sequence, which is in XML format (e.g.,
    `JSONtoSOAP.xml` ). This will be the
    `In` sequence for your API. Next, create an
    `out` sequence.

17. Right-click on the `out` sequence folder and
    click **Create** to create a new `out`
    sequence.  
    ![](../../assets/img/learn/tutorials/create-out-sequence.png)

18. Name the sequence `SOAPtoJSON`. Add a
    **Property** mediator to the sequence and give the following values
    to the property mediator.

    |                |                  |
    |----------------|------------------|
    | Property Name  | messageType      |
    | Value Type     | Literal          |
    | Value          | application/json |
    | Property Scope | axis2            |

    ![](../../assets/img/learn/tutorials/add-property-mediator.png)

19. Save the sequence, which is in XML format (e.g.,
    `SOAPtoJSON.xml`). This will be the
    `Out` sequence for your API.

20. Click the **Push all changes to the server** icon shown below to
    commit your changes to the Publisher server.  
    ![](../../assets/img/learn/tutorials/push-changes-to-server.png)

21. Sign back in to the API Publisher, click to **Edit** the API, navigate to the **Implement** tab, select **Enable
    Message Mediation** and engage the `In`
    and `out` sequences that you created earlier.  
    ![](../../assets/img/learn/tutorials/engage-sequences.png)

22. **Save** the API.  
    You have created an API, a resource to access the SOAP backend and
    engaged sequences to the request and response paths to convert the
    message format from JSON to SOAP and back to JSON. Let's subscribe
    to the API and invoke it.

23. Sign in to the API Store and subscribe to the API and create an
    access token if you have not done so already.  
    ![](../../assets/img/learn/tutorials/subscribe-to-api.png)

24. Go to the **API Console** tab and expand the POST method.

25. Provide the payload in the `body` parameter in
    JSON format and click **Try it out**. Here's a sample JSON
    payload: {"request":{"PhoneNumber":"18006785432","LicenseKey":"0"}}  
    ![](../../assets/img/learn/tutorials/try-out.png)

26. Note that you get a JSON response to the JSON request whereas the
    backend accepts SOAP messages. The request and response are
    converted by the sequences that you engaged at the API Gateway.  
    ![](../../assets/img/learn/tutorials/response.png)

In this tutorial, you converted a message from JSON to SOAP and back to
JSON using `In` and `Out` sequences.
