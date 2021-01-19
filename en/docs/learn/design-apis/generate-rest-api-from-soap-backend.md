# Generate a REST API from a SOAP Backend

You can use WSO2 API Cloud to easily expose legacy SOAP backends as REST APIs. 
WSO2 API Cloud supports generating REST APIs from WSDL 1.1 based SOAP backends.

Follow the instructions below to generate a REST API using an existing SOAP backend. For the purpose of demonstration, we will use sample values when following the instructions below: 

   <html><div class="admonition note">
      <p class="admonition-title">Note</p>
      <ul>Before you begin... </ul>
      <ul>
	<li>Make sure that you have a valid WSDL URL from the SOAP backend. It should belong to the WSDL 1.1 version.</li>
	<li>Be sure to specify the endpoint when creating a REST service from a SOAP WSDL. This is necessary because the endpoint does not get picked up by the WSDL unless you specify it.</li>
      </ul>
      </div>
    </html>

1.  Sign in to WSO2 API Cloud. This opens the API Publisher portal.

2.  Click **CREATE API** and then click **I Have a SOAP Endpoint**.
 
    <html><div class="admonition info">
      <p class="admonition-title">Info</p>
      <ul>
	<li>You can either select **WSDL URL** and specify the file URI (i.e., the relative path to the file with the API definition) or you can select **WSDL Archive/File** and upload your WSDL file.
        </li>
        <li>Following are the two options you can use to create APIs for SOAP backends:
           <ul>
      		<li>**Pass Through** – Creates a pass-through proxy for SOAP requests coming to the API Gateway. This option is selected by default in the UI</li>
      		<li>**Generate REST APIs** – Generates REST API definitions from the given WSDL URL.</li>
      	   </ul>
        </li>
       </ul>
      
      </div>
    </html>

3. Specify the WSDL URL for the SOAP backend and select **Generate REST APIs**. 
  Let's specify `http://ws.cdyne.com/phoneverify/phoneverify.asmx?wsdl` as the sample WSDL URL.

4. Click **Start Creating** and provide information of the API. Let's provide the following sample values for demonstration:

    | Field              | Sample value       |
    |--------------------|--------------------|
    | Name               | PhoneVerification  |
    | Context            | /phoneverify       |
    | Version            | 1.0                |
    | Access Control     | All                |
    | Visibility on Store| Unlimited          |
    | Tags               | phone              |

5. Click **Next:Implement**. This takes you to the **Implement** tab.

6. Click **Managed API** to expand the section.

7. Select the **Endpoint Type** as `HTTP/SOAP Endpoint` and specify the production endpoint URL. 
   Let's specify `http://ws.cdyne.com/phoneverify/phoneverify.asmx` as the sample production endpoint URL. 

8. Navigate to the **SOAP to REST Mapping** section and click on a resource to view the In and Out sequences of the API.</br>
	Following is an example that shows the generated sample API In-sequence for a POST method:

     ``` xml
        <header description="SOAPAction" name="SOAPAction" scope="transport" value="http://ws.cdyne.com/PhoneVerify/query/CheckPhoneNumber"/>
        <property name="REST_URL_POSTFIX" scope="axis2" action="remove"/>
        <property expression="json-eval($.CheckPhoneNumber.LicenseKey)" name="req.var.CheckPhoneNumber.LicenseKey"/>
        <property expression="json-eval($.CheckPhoneNumber.PhoneNumber)" name="req.var.CheckPhoneNumber.PhoneNumber"/>


        <payloadFactory description="transform" media-type="xml">
        <format>
        <soapenv:Envelope xmlns:soapenv="http://www.w3.org/2003/05/soap-envelope" xmlns:web="http://ws.cdyne.com/PhoneVerify/query">
        <soapenv:Header/>
        <soapenv:Body>
            <web:CheckPhoneNumber xmlns:web="http://ws.cdyne.com/PhoneVerify/query">
        <web:LicenseKey>$1</web:LicenseKey>
        <web:PhoneNumber>$2</web:PhoneNumber>
        </web:CheckPhoneNumber>

        </soapenv:Body>
        </soapenv:Envelope>
        </format>
        <args>
            <arg evaluator="xml" expression="get-property('req.var.CheckPhoneNumber.LicenseKey')"/>
        <arg evaluator="xml" expression="get-property('req.var.CheckPhoneNumber.PhoneNumber')"/>

        </args>
        </payloadFactory>
        <property description="messageProperty" name="messageType" scope="axis2" type="STRING" value="application/soap+xml"/>
     ```

	The incoming JSON message parameters are stored using properties. A payload factory mediator is used to generate the SOAP payload required by the backend.

9. Click **Next:Manage**. This takes you to the **Manage** tab.

10. On the **Manage** tab, select required **Subscription Tiers** for the API and then click **Save & Publish** to publish the API to the API Store.

11. Navigate to the API Store and subscribe to the API. For detailed instructions on how to subscribe to an API, see [Subscribe to an API](../../consume-apis/subscribe-to-an-api).

    Once you generate the production and sandbox keys, you will receive a valid access token to access the API.

12. Invoke the API. For detailed instructions, see [Invoke an API](../../consume-apis/invoke-an-api).
    
    Once you successfully invoke the API, you can observe the actual backend response you get.
    

