
# Enforce Throttling and Resource Access Policies

Throttling allows you to limit the number of hits to an API during a given period of time, typically to:
- Protect your APIs from security attacks.
- Protect your backend services from overuse.
- Regulate traffic according to infrastructure limitations.
- Regulate usage for monetization. 

**In this tutorial**, you engage throttling and resource access
policies at various levels to your API and observe how the API Gateway
enforces them in the API.

!!! note
    
    **Before you begin** ,
    
    -   Follow [Create and Publish an API](../create-and-publish-an-api) to create and publish the `PhoneVerification` API.
    -   Follow [Subscribe to and Invoke an API](../subscribe-to-and-invoke-an-api) to subscribe to the API using the `Bronze` throttling tier.
    

Let's get started.

1.  Sign in to the API Store and select the
    `PhoneVerification` API.

2.  Subscribe to the API using the `Default Application` and `Bronze` tier if you have not done so already.  
    ![](../../assets/img/learn/tutorials/subscription-options.png)

3.  In the API Store, click the **APPLICATIONS** menu, click
    `DefaultApplication` to open it, and then click
    the **Production Keys** tab. If you already have an access token for
    the application, you may have to scroll down and click
    **Re-generate** . Access tokens expire 1 hour after creation unless
    you extend the period.   
      
    Let's invoke this API.

4.  Click on the API, then go to its **API Console** tab and expand the
    GET method.  
    ![](../../assets/img/learn/tutorials/api-console-tab.png)

5.  Give values to the parameters (PhoneNumber 18006785432 and
    LicenseKey 0) and click **Try it out** to invoke the API.  
    ![](../../assets/img/learn/tutorials/specify-parameter-values.png)  

6.  Note the response that appears in the API Console. As we used a
    valid phone number in this example, the response returns as valid.  
    ![](../../assets/img/learn/tutorials/api-response-body.png)

7.  Note that you subscribed to the API on the Bronze throttling tier.
    The Bronze tier allows you to make a 1000 calls to the API per
    minute. If you exceed your quota, you get a throttling error as
    shown below.  
    ![](../../assets/img/learn/tutorials/throttling-error.png)  
    Let's try to invoke the API using an unavailable resource name.
8.  Click the **APIs** menu in the API Store, click the API you want to
    invoke and then copy the production URL in the API's **Overview**
    tab.  

9.  Append the payload to the API's URL you copied earlier. For example,
    [https://gateway.api.cloud.wso2.com:443/t/companyn3/phoneverify/1.0.0](https://gateway.api.cloud.wso2.com/t/companyn3/phoneverify/1.0.0)
    /
    **[CheckPhoneNumber?PhoneNumber=18006785432&LicenseKey=0](http://192.168.1.2:8280/phoneverify/1.0.0?PhoneNumber=123456&LicenseKey=0)**
    .  
    Let's invoke the API.

10. Install [cURL](http://curl.haxx.se/download.html) or any other REST
    client.

11. Go to the command-line and invoke the API using the following cURL
    command.  
    Note that the `PhoneVerification` API's
    resource name is `CheckPhoneNumber`, but
    we use an undefined resource name as
    `CheckPhoneNum`.

    ``` java
    curl -k -H "Authorization: Bearer <access token in step 3>" '<API's URL in step 9>/CheckPhoneNum?PhoneNumber=18006785432&LicenseKey=0'
    ```

    Here's an example:

    ``` java
        curl -k -H "Authorization: Bearer 0bc0500523dddc5c973971f16b19103e" 'https://gateway.api.cloud.wso2.com:443/t/companyn3/phoneverify/1.0.0/CheckPhoneNum?PhoneNumber=18006785432&LicenseKey=0'
    ```

12. Note that t he call gets blocked by the API Gateway with a 'no
    matching resource' message. It doesn't reach your backend services
    as you are trying to access a REST resource that is not defined for
    the API.  
    ![](../../assets/img/learn/tutorials/no-matching-resource.png) 

You have seen how the API Gateway enforces throttling and resource
access policies for APIs.
