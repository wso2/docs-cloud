# API Security

1.  #### How can I block a certain user from accessing my API?

    1\. Log in to the Admin Dashboard as the admin user of your organization.
    ( <https://api.cloud.wso2.com/admin/> )

      
    2. Click on Black List under the Throttle Policies section and click
    Add Item (Refer to the screenshot below)

    [![](https://2.bp.blogspot.com/-LRXndfF0rCw/WWzsv3J0RPI/AAAAAAAAC3k/Pz6jKP6INTwB7SPuOpCWT4YlTNvbExmAgCLcBGAs/s640/throttling_policies.png){width="640"
    height="419"}](https://2.bp.blogspot.com/-LRXndfF0rCw/WWzsv3J0RPI/AAAAAAAAC3k/Pz6jKP6INTwB7SPuOpCWT4YlTNvbExmAgCLcBGAs/s1600/throttling_policies.png)  

    3. Select the condition type as the user and give the fully
    qualified username as the value and click to blacklist.

    For example, if you want to block the user
    `                         cloud@wso2.com                       `
    from invoking APIs, you have to provide the value as
    `                         cloud@wso2.com                        @cloudorg           `
    by appending the organization key at the end of the username with
    the **'@'** character.

    If you follow the above steps, the user will not be able to invoke
    APIs until you remove this the blacklist policy.

2.  #### How can I control the requests which reach my APIs?

    API Cloud uses a concept called throttling which allows you to limit
    the number of hits to an API during a given period of time. This can
    help you to

    -   Protect your APIs from security attacks

    -   Protect your backend services from overuse

    -   Regulate traffic according to infrastructure limitations

    -   Regulate usage for monetization.

      
    For information on different levels of throttling in WSO2 Cloud, see
    [Throttling
    tiers](https://docs.wso2.com/display/APICloud/Key+Concepts) . For
    more information on configuring throttling for your APIs refer
    [this](https://docs.wso2.com/display/APICloud/Enforce+Throttling+and+Resource+Access+Policies)
    tutorial.

3.  #### How can I block subscription to my APIs?

    An API creator blocks subscription to an API as a way of disabling
    access to it and managing its usage and monetization. If you want to
    block any subscriptions created by your API consumers all you need
    to do is follow the simple steps explained in the
    [tutorial](https://docs.wso2.com/display/APICloud/Block+Subscription+to+an+API)
    .
