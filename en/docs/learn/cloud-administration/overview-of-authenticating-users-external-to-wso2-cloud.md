# Authenticate Users that are External to WSO2 Cloud

According to the architecture of WSO2 API Cloud, a users need to be
registered in the WSO2 Cloud user store in order to consume WSO2 API Cloud
services. However, some organizations may want to connect their internal
developers or API consumers (end-users) to WSO2 API Cloud without explicitly
adding them to the WSO2 Cloud user store. In such cases, organizations can
connect their internal identity providers and user stores to WSO2 API
Cloud.

If you want to **authenticate external users for Web UI access** , you need to do
one of the following:

-   [Configure an External Identity Provider for WSO2 API Cloud
    Authentication](../configure-an-external-identity-provider-for-api-cloud-authentication)
    : You can do this when you want the organization to link their IdP to
    WSO2 Cloud to provide SSO-based authentication for API
    Cloud apps.
-   [Configure an On-Premises User Store for API Cloud
    Authentication](../configure-an-on-premises-user-store-for-api-cloud-authentication)
    : You can do this when you want the organization to connect their local
    LDAP user store to WSO2 Cloud through the WSO2 Outbound
    Agent. This allows the organization to provide authentication for
    users in the LDAP, without having to share the credentials of the LDAP with
    WSO2 Cloud.  

If you want to authenticate subscribers who are not in WSO2 Cloud's user store, you can do the following:

-   [Authenticate External Users for API Invocation](../authenticate-external-users-for-api-invocations).
