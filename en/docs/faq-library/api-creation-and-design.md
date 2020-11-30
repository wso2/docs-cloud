# API Creation and Design

1.  #### I have an existing swagger. How can I create my API in API Cloud?

    You can use publicly hosted Swagger files to create APIs using WSO2
    API Cloud or you can simply upload your swagger YAML or JSON file to
    create an API without a hassle.

2.  #### How can I create a Mock API?

    You can create a sample API with an inline script and then make it
    available for testing purpose for your API subscribers. You do not
    need to have an actual service backend but rather mock the response
    using the inline script. This is provided through the API Cloud’s
    prototyped API feature. 

3.  #### How can I create a SOAP API?

    All you need to have is a publicly hosted WSDL and a backend URL and
    this can be achieved easily in the API Cloud.

4.  #### How can I use a single API to route to different backend services?

    API Cloud provides an out of the box feature called the dynamic
    endpoint functionality. This allows you to dynamically pick the
    backend to which each call is routed based on the call’s properties.
    You can refer to this
    [post](http://wso2.com/blogs/cloud/multiple-endpoints-per-api/) on
    how to achieve this.

5.  #### How can I use dynamic endpoints, with different credentials for each backend?

    Assuming that you have already designed your API, follow the steps
    below.

    1.  Select **Non-Secured** as the **Endpoint Security Scheme** in
        the **Implement** tab.

    2.  Provide your credentials for each endpoint. A sample message
        mediation sequence is given below. There is an authorization
        header for each endpoint in the sequence. The corresponding
        backend will be called with its authorization header.  

        ``` java
        <sequence xmlns="http://ws.apache.org/ns/synapse" name="dynamic_ep">
            <property expression="json-eval($.operation)" name="operation" />
            <filter regex="menu" source="$ctx:operation">
                <then>
                    <property name="Authorization" expression="fn:concat('Basic ', 'abcdfffghksjdksk==')" scope="transport"/>
                    <header name="To" value="YOUR_BACKEND_1" />
              </then>
             <else>
                   <property name="Authorization" expression="fn:concat('Basic ', 'HjhslhhishhssHH=')" scope="transport"/>
                   <header name="To" value="YOUR_BACKEND_2" />
             </else>
           </filter>
           <property expression="get-property('To')" name="ENDPOINT_ADDRESS" />
        </sequence>
        ```

6.  #### What content types are supported in API Cloud? 

    API Cloud Gateway servers process requests and responses with the
    following content types. If you have a requirement to process
    payloads of other content types, send a support request to the WSO2
    Cloud team.

    -   application/x-www-form-urlencoded

    -   multipart/form-data

    -   text/html

    -   application/xml

    -   text/xml

    -   application/soap+xml

    -   text/plain

    -   application/json

    -   application/vnd.api+json

    -   application/json/badgerfish

    -   text/javascript

7.  #### What is meant by Context of an API?

    Context refers to the URI context path of the API which is case
    sensitive. The supported formats are listed below.

    1.  /foo

    2.  /foo/bar

    3.  /foo/{version}/bar (case sensitive) - allows the version to be
        within the context

8.  #### Why should I add tags for an API?

    You can use keywords and common search terms as tags to group APIs
    that have similar characteristics. After publishing the API,
    consumers can click these tags to jump to a group of similar APIs.

9.  #### How can I add documentation for my APIs?

    API documentation helps API subscribers to understand the
    functionality of the API and for API publishers to market APIs and
    sustain competition.

10. #### What is meant by each API resource auth types?

    -   **None** : No authentication is applied and the API Gateway
        skips the authentication process
    -   **Application** : Authentication is done by the application. The
        resource accepts  application access tokens.  
    -   **Application User** : Authentication is done by the 
        application user. The resource accepts user access tokens.  
    -   **Application and Application User** : Both  application level
        and  application user level authentication is applied. Note that
        if you select this option in the UI, it appears as **Any** in
        the API Cloud internal data storage and data representation, and
        **Any** will appear in the response messages as well.

11. #### How can I display multiple API versions in the API Store?

    - Follow the steps below to show multiple versions of an API in the
    API Store.

    a\. Login to the API Publisher.  
    b. Go to the Management Console (
    <https://gatewaymgt.api.cloud.wso2.com/carbon> ).  
    c. If you are already logged into the API Publisher, you are
    automatically logged into the Management Console.  
    d. Once you log in to the Management Console, navigate to the
    **Browse \> Resources** section and locate the
    `/_system/config/apimgt/applicationdata/tenant-conf.json`
    file in the registry. This can also be done by searching for the
    `/_system/config/apimgt/applicationdata/tenant-conf.json`
    file directly in the **Location** field.

    - Click **Edit as text**, add the following properties to the file
    and click **Save Content**.

    ``` java
        "DisplayMultipleVersions":true
        "DisplayAllAPIs":true
    ```

      

12. #### How can I convert a response in the backend from XML to JSON?

    a\. Go to edit the API

    b\. Select the "Manage" tab

    c\. Tick the message mediation checkbox

    d\. Select the " **xml\_to\_json\_out\_message** " sequence for the **Out
    Flow**

    e\. Save and publish the API.


13. #### Why testing backend connection gives an invalid result even if the backend service is available? 

    Clicking **Test** to check the endpoint will send an HTTP head call
    with SSL for checking if a given URL is serviceable. The HTTP head
    call is used here as it is a faster way to verify the endpoints.
    When the backend does not give any response for HTTP head call it
    returns a 404 error. This does not imply the backend is failing to
    serve other HTTP request methods as well. Therefore you get an
    invalid result when testing.
    
14. #### How can I enable CORS on the Token and Revoke APIs for a particular host?

    WSO2 API Cloud provides separate CORS enabled endpoints for Token and Revoke APIs. You can replace your existing endpoints with the following CORS enabled endpoints:

    - Token Endpoint - https://gateway.api.cloud.wso2.com/token-cors
    - Revoke Endpoint - https://gateway.api.cloud.wso2.com/revoke-cors 
    
    
