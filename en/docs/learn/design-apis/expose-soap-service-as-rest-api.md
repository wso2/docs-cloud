# Expose a SOAP Service as a REST API

WSO2 API Cloud supports exposing existing SOAP and WSDL based services as REST APIs.
The organizations that have SOAP/WSDL based services can easily bridge their existing services to REST without having to bear the cost of a major migration. WSO2 API Cloud supports two types of services. One service performs a pass-through of the SOAP message to the backend, and the other service generates [a RESTful API from the backend SOAP service]({{base_path}}/learn/design-apis/generate-rest-api-from-soap-backend/).

Follow the instructions below to expose a SOAP service as a RESTful API via the **Pass Through** option:

1.  Sign in to WSO2 API Cloud. This opens the API Publisher portal.

2.  Click **CREATE API** and then click **I Have a SOAP Endpoint**.

3. Select the **Pass Through** option and then select one of the following options:

     * WSDL URL - If you select this option, you need to provide an endpoint URL.

     * WSDL Archive/File - If you select this option, click Browse and upload either an individual WSDL file or a WSDL archive, which is a WSDL project that has multiple WSDLs.

     <html><div class="admonition note">
     <p class="admonition-title">Note</p>
     <p>When uploading a WSDL archive, all the dependent WSDLS/XSDS that are referred to in the parent WSDL file should reside inside the WSDL archive itself. If not, the validation will fail at the point of API creation.</p>
     </div>
     </html>

     This example uses the WSDL [Phone Verify](http://ws.cdyne.com/phoneverify/phoneverify.asmx?wsdl) from CDYNE as the endpoint, but you can use any SOAP backend of your choice.

4.  Click **NEXT** to proceed to the next phase.
5.  Provide the information in the table below and click **CREATE**.

    | Field   | Sample Value       |
    |---------|--------------------|
    | Name    | PhoneVerification  |
    | Context | /phoneverify       |
    | Version | 1.0                |
    | Endpoint| http://ws.cdyne.com/phoneverify/phoneverify.asmx|
    | Business Plans| Unlimited|
    
     This displays the created API in the Publisher portal.
     
6. Click **API Definition** to view the API definition of the created schema.

  
     <html><div class="admonition note"><p class="admonition-title">Note</p>
     <p>
     If you want to add scopes to the resources that were created, click  **Resources**, create the new scopes and then specify them under operation scope. If you specify a scope, you need to use the same scope when generating access tokens for the subscribed application to invoke the API.
     </p>
     </div></html>   


     <html><div class="admonition note">
     <p class="admonition-title">Note</p>
     <p> When creating this API, **API Level** was selected as the default **Rate limiting level**. For more information on setting advanced throttling policies,
     see [Enforce Throttling and Resource Access Policies]({{base_path}}/learn/apply-throttling-and-rate-limiting/set-throttling-limits/).</p>
     </div>
     </html>

Now, the SOAP service is created and configured successfully as a RESTful API. 

