# Authenticate Users that are External to WSO2 Cloud

According to the architecture of WSO2 API Cloud, a users need to be
registered in the WSO2 Cloud user store in order to consume WSO2 API Cloud
services. However, some organizations may want to connect their internal
developers or API consumers (end-users) to WSO2 API Cloud without explicitly
adding them to the WSO2 Cloud user store. In such cases, organizations can
connect their internal identity providers and user stores to WSO2 API
Cloud.

If you want to **authenticate external users for Web UI access** , you need to do
the following:

-   [Configure an External Identity Provider for WSO2 API Cloud
    Authentication](../configure-an-external-identity-provider-for-api-cloud-authentication)
    : You can do this when you want the organization to link their IdP to
    WSO2 Cloud to provide SSO-based authentication for API
    Cloud apps.

If you want to authenticate subscribers who are not in WSO2 Cloud's user store, you can do the following:

-   [Authenticate External Users for API Invocation](../authenticate-external-users-for-api-invocations).
