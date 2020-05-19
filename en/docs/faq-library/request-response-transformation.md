# Request/Response Transformation

1.  #### The backend web service does not match the API design that I expect. What should I do?

    You can extend the default message mediation sequence using
    mediators. The API Cloud comes with a powerful mediation engine that
    can transform and orchestrate API calls on the fly.
   

2.  #### What type of mediators are supported by the API Cloud?

    See [WSO2 Cloud
    Mediators](../../get-started/key-concepts/#mediators).
    

3.  #### What properties can I retrieve from an API using a property mediator within a sequence?

    | Property                                                  | Description                                                                                                           |
    |-----------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------|
    | SYNAPSE\_REST\_API\_VERSION                               | Retrieves the version of the API. E.g., 1.0.0.                                                                        |
    | REST\_SUB\_REQUEST\_PATH                                  | Retrieves the sub request with path and query parameters. E.g., "/CheckPhoneNumber?PhoneNumber=1234567&LicenseKey=0". |
    | REST\_API\_CONTEXT or api.ut.context                      | Retrieves the context of the API in the form /t/tenantDomain/context/version for an API. E.g., "/t/tenant/new/1.0.0". |
    | REST\_FULL\_REQUEST\_PATH                                 | Retrieves the entire request path. E.g., "/t/tenant/new/1.0.0/CheckPhoneNumber?PhoneNumber=1234567&LicenseKey=0".     |
    | SYNAPSE\_REST\_API\_VERSION\_STRATEGY                     | For example, "context".                                                                                               |
    | TRANSPORT\_IN\_NAME                                       | Retrieves the transport. For example, "https".                                                                        |
    | SYNAPSE\_REST\_API                                        | Retrieves the name of the API. For example, " [admin-AT-tenant.com](http://admin-AT-tenant.com) --NewAPI:v1.0.0".     |
    | api.ut.HTTP\_METHOD                                       | The HTTP method which was used for the invocation. (E.g.: GET/POST)                                                   |
    | [api.ut.application.name](http://api.ut.application.name) | The name of the OAuth2 application used for the invocation. (E.g,: DefaultApplication)                                |
    | api.ut.apiPublisher                                       | The name of the person who published the API.  (E.g.: <clouduser@gmail.com> @wso2cloud)                               |
    | api.ut.userId                                             | The user who invoked the API. (E.g.: <subuser@gmail.com> @wso2cloud)                                                  |


4.  #### How to send a POST request with no payload (no Body) ?

    When carrying out a POST request from the API Cloud to the back-end
    ,API Cloud expects a request body parameter to be present.This is
    the default behavior of ESB/API Manager. But in case we need to do a
    POST request with no body we set the property in the in sequence of
    the API.

    `<property name="FORCE_POST_PUT_NOBODY" value="true" scope="axis2" type="BOOLEAN"/>`

    Setting this property in a custom sequence will allow to do a post
    without body. However when we set this API cloud will send its
    default content type which is application/x-www-form-urlencoded and
    do the post request with no body. We cannot remove the content type
    completely but we can change the value of it using a property as
    mentioned below.

    `<property name="Content-Type" value="text/plain" scope="transport"/>`

    This will change change the content type to text/plain. Simillarly,
    you can set the expected content type in this property in you custom
    sequence.

5.  #### How can I disable chunking for my APIs?

    This can be done with the use of a custom mediation extension which
    will disable chunking, as described below.

    Save the content below into an xml file and upload it as the **In
    sequence** of your API from the API Publisher.

    ``` java
        <?xml version="1.0" encoding="UTF-8"?>
        <sequence xmlns="http://ws.apache.org/ns/synapse"
                 name="disable-chunking">
               <property name="DISABLE_CHUNKING" value="true" scope="axis2" />
        </sequence>
    ```


6.  #### How to convert incoming and outgoing message formats?

    You can change the message formats of your requests in the API
    Cloud. For this we use synapse which is a powerful mediation engine.

  

