# Microgateway

1.  #### Does the API Cloud send outbound calls to the microgateway?

    No. The microgateway only invokes the REST APIs of API Cloud to
    synchronize API definitions of your organization, update statistics
    on your API usage, and update the health status of the gateway.

2.  #### How do I monitor the health of the gateways? Is there any default health check APIs deployed on the gateway?

    You can configure your health check monitoring tool to send a
    requests to the <http://localhost:8280/services/Version> endpoint.

3.  #### How can I generate OAuth bearer tokens for my APIs using the microgateway? Do I need to use WSO2 API Cloud instead?

    You can generate tokens connecting to the microgateway token
    endpoints as well as API Cloud gateway token endpoints.

4.  #### Can I invoke the APIs deployed in the Cloud and microgateway both?

    Yes. If the backend API endpoint is reachable from Cloud gateway,
    you can invoke the API from both gateways.

5.  #### If my backend API endpoint is only reachable on the internal network, does the API Cloud allow me to create the API?

    Yes.

6.  #### How can I manage different environments in the application development lifecycle?

    Yes. You are required to register multiple organizations
    corresponding to each development stage and run multiple microgateways for each organization.

7.  #### Can I run multiple microgateways for the same organization?

    Yes. If you are running multiple microgateways on the same node,
    set an offset value(\<Offset\>0\</Offset\>) in the \[microgateway\]/repository/conf/carbon.xml file to avoid port conflicts
    when the gateways start.

8.  #### What is the mechanism of getting the security updates and bug fixes for my microgateway?

    You can contact <cloud@wso2.com> to get the exact details.
