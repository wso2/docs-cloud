# How to Migrate to Choreo?

## Migration process

-  It is not possible to automate the migration process due to several reasons. WSO2 API Cloud and Choreo are two distinct platforms with different architectures. Therefore, automating the migration process is too complicated. Additionally, some API Cloud customers have customizations (such as custom domains and user stores) that require manual migration.
-  Depending on the customer's need, WSO2 can arrange a demo to showcase the API Management capabilities of Choreo.
-  As the first step of the migration, WSO2 will assign an engineer to migrate some APIs and mediation logic to Choreo as a proof of concept(PoC) for the customer use case.
<html>
<div class="admonition info">
<p class="admonition-title">Note</p>
<p>If a customer's backends are secured and accept traffic only from WSO2 API Cloud, the customer should do the needful to allow the Choreo platform access. Alternatively, the customer can provide a sandbox-like environment with fewer restrictions.</p>
</div>
</html>

-  If satisfied with the PoC, customers can create their organization in Choreo and invite the assigned engineer to implement APIs and mediation logic. Once implemented, the customer will need to test all use cases and confirm that all test cases are working.
-  Next, customers can migrate additional configurations like custom domains, external identity providers/user stores, theming, etc. WSO2 can either assign an engineer to set these up or assist the customer in doing so themselves.
-  Customers can then ask their API consumers/application developers to subscribe to the new APIs, generate credentials, and change their application code to use the new API endpoints and credentials. Once satisfied, consumers can move their API traffic to the newly created Choreo APIs. 
-  Customers can decide how to transfer their production traffic to the new Choreo APIs. Until all production traffic is routed to Choreo, the API Cloud organization will remain active until its end-of-life on December 31, 2023.

## What should customers do during the migration process?

-  Customers should assign an individual or team to assist the WSO2 engineer during the migration process from steps 2 to 6 in the migration process above. The assignee should be able to explain their use cases and also test new APIs and other configurations. 
-  After migrating to Choreo, customers must create new applications (in the API Store) to subscribe to the new APIs, which will generate new consumer keys/secrets. The new keys/secrets must be updated on the client applications by releasing a new version of the client application and testing it. This method has two advantages: further testing can be done using the new client application, and the previous version of the client application can still work with the API Cloud until the migration to Choreo is complete.
-  Choreo uses OAuth 2.0 bearer token-based authentication for API access. The only difference between API Cloud and Choreo is that the OAuth 2.0 token issued by Choreo is a JWT token, compared to the opaque token issued by API Cloud. However, this should not impact client applications because both tokens are strings with different lengths. 
-  The default API endpoint format is different in Choreo than in API Cloud. Therefore, client applications have to be modified with the new endpoints. If a custom domain was configured in API Cloud, a different custom domain has to be set up in Choreo because the same domain cannot be used in both systems.
-  If customers have external API consumers, they should be informed about steps 2 to 4 in advance. Once consumers are satisfied with the new APIs, they can move to the new client application and Choreo APIs.
-  Currently, Choreo only offers fixed API throttling policies (10KPerMin, 20KPerMin, 50KPerMin, Unlimited). Adding custom throttling policies will be an upcoming feature. Application-level throttling will also be available soon. If you are using any advanced throttling capabilities, do [contact us](mailto:cloud@wso2.com).
