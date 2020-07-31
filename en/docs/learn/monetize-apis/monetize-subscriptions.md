# Monetize Subscriptions

The end-to-end API monetization support provided via WSO2 API Cloud
allows you to create subscription throttle policies so that you can
appropriately bill subscribers who consume your APIs. With WSO2 API
Cloud you can either create your own subscription throttle policies or
customize existing subscription throttle policies.

!!! tip
    
    If you want to use a subscription throttle policy to bill subscribers,
    you have to define the throttle policy as commercial (billable) instead
    of free .
    

The following topics walk you through the steps to create, edit, or
delete a subscription throttle policy:


### Create a subscription throttle policy

Follow the steps below to create a subscription throttle policy:

1.  Sign in to WSO2 API Cloud.
2.  On the API Publisher, click **Admin Dashboard** under **Configure**.    
    This takes you to the **Admin Dashboard** .
3.  On the left navigation pane, click **THROTTLING POLICIES** , and
    then click **SUBSCRIPTION POLICIES**. This displays the
    **Subscription Throttling Policies** screen.

    !!! tip
    
        The default tiers are Gold, Silver, and Bronze.
    

4.  To create a new commercial subscription throttle policy, click **ADD
    NEW POLICY** , specify the required values (be sure to select
    **Commercial** as the billing plan), and click **Save** . For
    example, the sample values in the following screen creates a new
    commercial subscription throttle policy named
    `Platinum`.  

Now you can apply the `Platinum` payment plan to your
APIs. (You can do this when creating or editing an API.)

Next let's take a look at how you can edit a subscription throttle
policy.

### Edit a subscription throttle policy

Follow the steps below to edit an existing subscription throttle policy:

1.  On the **Subscription Throttling Policies** screen, click **Edit**
    on the policy you want to edit.  
2.  Change the values as required.
3.  Click **Save** .
  

### Delete a subscription throttle policy

Follow the steps below to delete an existing subscription throttle
policy:

1.  On the **Subscription Throttling Policies** screen, click **Delete** on the policy you want to delete. This displays a message to confirm deletion.  
2.  Click **Yes**. This deletes the throttle policy.

Now that you understand how to create, edit, and delete subscription
throttle policies, you are ready to [set up billing
plans](../set-up-billing-plans).

  
