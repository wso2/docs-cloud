# Block Subscription to an API

An API creator **blocks subscription** to an API as a way of disabling
access to it and managing its usage. A blocking can be
temporary or permanent. You can go ahead and `unblock` the API to
allow API invocations again.

Let's take a look at how you can block subscription to an API in the API
Publisher and observe how the subscribers can interact with it in the
API Store. We will also look at how to unblock a blocked API and observe how the subscriber experience changes when
you unblock the API.

!!! note
    
    You block APIs by subscriptions. That is, a given user is blocked access
    to a given API subscribed to using a given application. If a user is
    subscribed to two APIs using the same application and you block access
    to only one of the APIs, s/he can still continue to invoke the other
    APIs that s/he subscribed to using the same application. Also, s/he can
    continue to access the same API subscribed to using different
    applications.
    
    Blocking happens in two levels:  
    
    -   **Block production** **and sandbox access** : API access is blocked
        with both production and sandbox keys.
    -   **Block production access only** : Allows sandbox access only.
        Useful when you want to fix and test an issue in an API. Rather than
        blocking all access, you can block production access only, allowing
        the developer to fix and test.
    
    When the API Gateway
    caching is enabled (it
    is enabled by default), even after blocking a subscription, consumers
    might still be able to access APIs until the cache expires, which
    happens approximately every 15 minutes.
    

1.  Sign in to the API Publisher.
2.  Create two APIs by the names `TestAPI1` and
    `TestAPI2` and publish them to the API Store.  
      
3.  Sign in to the API Store. Click the **APIs** menu and note that the
    two APIs are visible in the APIs page.  
    
4.  Subscribe to both APIs using the same application. You can use an
    existing application or create a new one.  
    
5.  Click the **APPLICATIONS** menu, click the application that you used
    to subscribe to the API with
    `DefaultApplication`, go to its
    **Production Keys** tab, and re-generate the access token. By
    default, access tokens expire an hour after creation.  
    
6.  Invoke both APIs using the access token you got in the previous
    step. We use [cURL](http://curl.haxx.se/download.html) here. The
    command is,

    ``` java
    curl -k -H "Authorization: Bearer <access token>" '<API URL>'
    ```

    Be sure to replace the placeholders as follows:

    -   **\<access token\>** : Give the token generated in step 5
    -   **\<API URL\>** : Go to the API's **Overview** tab in the API
        Store and copy the production URL and append the payload to it.

    Here's an example:

    ``` java
    curl -k -H "Authorization: Bearer f1d4d097-ebcc-3f02-8d91-0bd4e882ffcd" 'https://gateway.api.cloud.wso2.com:443/t/companyn3/test1/1.0.0/CheckPhoneNumber?PhoneNumber=18006785432&LicenseKey=0'
    ```
 
    You have subscribed to two APIs and invoked them successfully. Let's
    block one subscription and see the outcome.

7.  Block an API.
    1.  Sign back into the API Publisher.
    2.  Click on the API that you need to block.  
        In this case, click on the `TestAPI1`
        API.
    3.  Click **Subscriptions** to navigate to the managed subscription
        section.  
          
    4.  Click **Block** .  
        Note that the **Block** link immediately turns to **Unblock** ,
        allowing you to activate the subscription back at any time.
8.  Invoke the APIs to test the blocked API.

    1.  Sign back in to the API Store.
    2.  Invoke `TestAPI1` and
        `TestAPI2` again.

    !!! note
    
        You might have to **regenerate the access token** for
        `DefaultApplication` as done in step5, if the
        access token expiration time (1 hour by default) has passed since
        the last time you generated it.
    

9.  Note that you can invoke `TestAPI2` again but
    when you invoke `TestAPI1` , it gives a message
    that the requested API is temporarily blocked. Neither the API
    creator nor any subscriber can invoke the API until the block is
    removed.  
    

    !!! tip
    
        **Tip** : You might still be able to invoke an API within 15 minutes
        after blocking a subscription, until the cache is renewed.
    

10. BGO to the API Store, click **APPLICATIONS**, select the
    application that you used to subscribe to the two APIs earlier,
    And then click the application's **Subscriptions** tab. You will see that your subscription is now blocked.  
    
11. Unblock the API.  

    1.  Go back to the API Publisher.
    2.  Click on the respective API  
        In this case click `TestAPI1 1.0.0`.
    3.  Click **Subscriptions** and click **Unblock** corresponding to
        the respective subscription.  
        Make sure to click on the subscription that corresponds to the
        correct Application.

    If you invoke `TestAPI1` again, you will
    notice that you can invoke the API as usual.

    !!! tip
    
        **Tip** : You might still be unable to invoke an API within 15
        minutes after unblocking a subscription, until the cache is renewed.
    

    You have subscribed to two APIs, blocked subscription to one and
    tested that you cannot invoke the blocked API.
