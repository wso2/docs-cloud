# API Invocations

1.  #### What is meant by Error codes received at API Gateway?

    <table>
    <thead>
    <tr class="header">
    <th>Error code</th>
    <th>Error Message</th>
    <th>Description</th>
    <th>Example</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><pre><code>700700</code></pre></td>
    <td>API blocked</td>
    <td>This API has been blocked temporarily. Please try again later or contact the system administrators.</td>
    <td>Invoke an API which is in the <strong>BLOCKED</strong> lifecycle state</td>
    </tr>
    <tr class="even">
    <td><pre><code>900800</code></pre></td>
    <td>Message throttled out</td>
    <td><p>The maximum number of requests that can be made to the API within a designated time period is reached and the API is throttled for the user.</p></td>
    <td>Invoke an API exceeding the tier limit</td>
    </tr>
    <tr class="odd">
    <td><pre><code>900801</code></pre></td>
    <td>Hard limit exceeded</td>
    <td>Hard throttle limit has been reached</td>
    <td>Invoke an API exceeding the hard throttle limit</td>
    </tr>
    <tr class="even">
    <td><code>               900802              </code></td>
    <td>Resource level throttle out</td>
    <td>Message is throttled out because resource level has exceeded</td>
    <td>Sending/Receiving messages beyond authorized resource level</td>
    </tr>
    <tr class="odd">
    <td><code>               900803              </code></td>
    <td>Application level throttle out</td>
    <td>Message is throttled out because application level is exceeded</td>
    <td>Sending/Receiving messages beyond authorized application level</td>
    </tr>
    <tr class="even">
    <td><pre><code>900900</code></pre></td>
    <td><p>Unclassified authentication failure</p></td>
    <td>An unspecified error has occurred</td>
    <td>Backend service for key validation is not accessible when trying to invoke an API</td>
    </tr>
    <tr class="odd">
    <td><pre><code>900901</code></pre></td>
    <td><p>Invalid credentials</p></td>
    <td>Invalid authentication information provided</td>
    <td>Using an older access token after an access token has been renewed.</td>
    </tr>
    <tr class="even">
    <td><pre><code>900902</code></pre></td>
    <td><p>Missing credentials</p></td>
    <td>No authentication information provided</td>
    <td>Accessing an API without <strong>Authorization: Bearer</strong> header</td>
    </tr>
    <tr class="odd">
    <td><pre><code>900905</code></pre></td>
    <td><p>Incorrect access token type is provided</p></td>
    <td><p>The access token type used is not supported when invoking the API. The supported access token types are application and user accesses tokens. See <a href="https://docs.wso2.com/display/AM210/Key+Concepts#KeyConcepts-Accesstokens">Access Tokens</a> .</p></td>
    <td>Invoke an API with application token, where the resource only allows application user tokens</td>
    </tr>
    <tr class="even">
    <td><pre><code>900906</code></pre></td>
    <td><p>No matching resource found in the API for the given request</p></td>
    <td>A resource with the name in the request can not be found in the API.</td>
    <td>Invoke an API resource that is not available</td>
    </tr>
    <tr class="odd">
    <td><pre><code>900907</code></pre></td>
    <td><p>The requested API is temporarily blocked</p></td>
    <td>Happens when the API user is blocked.</td>
    <td>Invoke API resource with a subscription that has been blocked by the API publisher</td>
    </tr>
    <tr class="even">
    <td><pre><code>900908</code></pre></td>
    <td><p>Resource forbidden</p></td>
    <td>The user invoking the API has not been granted access to the required resource.</td>
    <td>Invoke an unsubscribed API</td>
    </tr>
    <tr class="odd">
    <td><pre><code>900909</code></pre></td>
    <td><p>The subscription to the API is inactive</p></td>
    <td>The status of the API has changed to an inaccessible/unavailable state.</td>
    <td>Invoke an API resource with a subscription that has not yet been approved by the administrator.</td>
    </tr>
    <tr class="even">
    <td><pre><code>900910</code></pre></td>
    <td><p>The access token does not allow you to access the requested resource</p></td>
    <td><p>Can not access the required resource with the provided access token. Check the valid resources that can be accessed with this token.</p></td>
    <td>Invoke API resource with an access token that is not generated to be used with the resource's scope.</td>
    </tr>
    <tr class="odd">
    <td><code>               102511              </code></td>
    <td>Incomplete payload</td>
    <td>The payload sent with the request is too large and the client is unable to keep the connection alive until the payload is completely transferred to the API Gateway</td>
    <td>Sending a large PDF file with the POST request</td>
    </tr>
    </tbody>
    </table>

    #### Other useful Error Codes

    **General errors**

    |                |                                               |
    |----------------|-----------------------------------------------|
    | **Error Code** | **Detail**                                    |
    | 303000         | Load Balance endpoint is not ready to connect |
    | 303000         | Recipient List Endpoint is not ready          |
    | 303000         | Failover endpoint is not ready to connect     |
    | 303001         | Address Endpoint is not ready to connect      |
    | 303002         | WSDL Address is not ready to connect          |

    **Failure on endpoint in the session**

    |                |                                                               |
    |----------------|---------------------------------------------------------------|
    | **Error Code** | **Detail**                                                    |
    | 309001         | Session aware load balance endpoint, No ready child endpoints |
    | 309002         | Session aware load balance endpoint, Invalid reference        |
    | 309003         | Session aware load balance endpoint, Failed session           |

    **Non-fatal warnings**

    |                |                                                |
    |----------------|------------------------------------------------|
    | **Error Code** | **Detail**                                     |
    | 303100         | A failover occurred in a Load balance endpoint |
    | 304100         | A failover occurred in a Failover endpoint     |

    **Referring real endpoint is null**

    |                |                             |
    |----------------|-----------------------------|
    | **Error Code** | **Detail**                  |
    | 305100         | Indirect endpoint not ready |

    **Callout operation failed**

    |                |                                                      |
    |----------------|------------------------------------------------------|
    | **Error Code** | **Detail**                                           |
    | 401000         | Callout operation failed (from the callout mediator) |

2.  #### Why am I seeing an error as “Missing credentials” as my API’s response?


    The Reason you are seeing this error is since you have not provided
    the OAuth token for invoking your API. It could be due to one of the
    following reasons.

      

    1.  You have not yet subscribed to the API.

    2.  You have not selected the correct application which you
        subscribed the API to - Perhaps the application selected from
        the dropdown in the API console is not the actual application
        which you subscribed to and hence the reason the keys are not
        appearing for your application. Select the correct application
        from the list and then invoke your API.

3.  #### Why am I seeing an error as “Invalid credentials” as my API’s response?

    The reason you are seeing this error is since the provided access
    token is invalid or the provided access token has expired. 

4.  #### How to avoid your backend endpoint getting suspended by the API Gateway?

    -   Go to API Publisher and select the API that you want to change.
        Then click **Edit** from API Overview.
    -   Under the **Implement** tab, select **Advanced Options** on the
        endpoint which you want to re-configure as shown below.

    -   Modify the values. If you want to disable the suspension
        rules, set both **Initial Duration** and **Max Duration** to
        `0`.  
     
    -   Save changes and re-publish the API.

5.  #### How to increase endpoint timeout for an API?

The warning "a callback is not registered (anymore) to process this
response" indicates that API gateway has received a response from
backend server after exceeding the endpoint timeout duration.

So, the gateway was unable to handle the response. You can increase the
endpoint timeout as follows.

-   Go to API Publisher and select the API that you want to change. Then
    click **Edit** from API Overview.
-   Under the **Implement** tab, select **Advanced Options** on the
    endpoint which you want to re-configure as shown below.
-   The endpoint timeout is set to 30s by default. Modify the value to
    increase the connection timeout.  
    Please note that the maximum allowed timeout is 2mins as API gateway
    has a global timeout value of 2mins.  
-   Save changes and re-publish the API.

  


