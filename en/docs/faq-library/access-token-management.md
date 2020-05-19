# Access Token Management

1.  #### How can I subscribe and generate tokens for my API?

    You can **subscribe** to API via the DevPortal. Follow this
    [tutorial](https://docs.wso2.com/display/APICloud/Subscribe+to+and+Invoke+an+API)
    to subscribe and invoke your API.

2.  #### How can I regenerate access tokens?

    Follow the below steps to re generate the access tokens for the
    applications for which your APIs are subscribed to.

    1. Navigate to the "Applications" option which is found at the top
    left hand corner of the Store UI and click it. This will take you to
    your applications page.


    2\. Select the application which your API is subscribed to and go to the
    **Production/Sandbox Keys** tab.

    3\. Click **Re-Generate**.

    4\. Now that you have regenerated the token you will need to go back to
    the API. In the top menu where you selected the Production Keys tab you
    will see an option as "Subscriptions". Click on that tab and select your
    API.

    5\. Now you will be able to invoke your API successfully.

3.  #### **How can I edit scopes of my API?**

In WSO2 API Manager once you have created scopes you are not able to
edit the scope using API Publisher UI. Using swagger console you can
achieve this with following below steps.

1\. On the publisher UI Design tab click Edit Source

2\. In the sources you can see scope under x-wso2-security : apim :
x-wso2-scopes : (your scope name)

3\. Add or edit scope and roles in this directive

4\. Then click Apply Changes (This will only update the swagger file not
the API you will not see the role until you save the API)

5\. **Save the API** which will deploy the API with the respective roles
for the scope .

6\. Then you will see the scope updated.

