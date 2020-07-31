# Endpoint Types

An Endpoint is a specific destination for a message such as an address, WSDL, a failover group, a load-balance group, etc. WSO2 API Cloud supports a range of different endpoint types to connect with advanced types of back-ends.

|Type                     |Description                                                                                                                                                                                                                                                                                                                                                                                                       |
|-------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| HTTP/ REST Endpoint     | A REST service endpoint based on a URI template.                                                                                                                                                                                                                                                                                                                                                           |
| HTTP/ SOAP Endpoint     | The direct URL of the SOAP web service.                                                                                                                                                                                                                                                                                                                                                                             |
| Failover Group Endpoint | An endpoint that a service tries to connect to in case of a failure. Selecting the endpoint when the primary endpoint fails happens in a round-robin manner. Failover group is a group of leaf endpoints (i.e., address endpoint, HTTP endpoint, and WSDL endpoint). When a failure occurs in the current endpoint (while sending a message), the failover group endpoint will try to send the message to another endpoint. The failover group ensures that the message is delivered as long as there is at least one active endpoint among the listed endpoints.                              |
| Load Balance Endpoint   | The endpoints where the incoming requests are directed to in a round-robin manner. They automatically handle fail-over as well.                                                                                                                                                                                                                                                                            |
| Dynamic Endpoint        | An endpoint where requests can be dynamically routed to an address based on a specific condition (e.g., request parameters, payload etc.). When using this endpoint type, a mediation sequence should be applied to the message **IN Flow** of the API.  |
| Prototype Endpoint      | A type of HTTP Endpoint which can be used when Prototyping an API (for promoting and testing). |
| AWS Lambda      | An AWS Lambda endpoint can be used to invoke AWS Lambda functions through WSO2 API Gateway. |

!!! note
    - **Prototype Endpoints** will be available only for APIs that are in **CREATED** or **PROTOTYPED** state.

    -   You can expose both REST and SOAP services to consumers through APIs.
    -   You cannot call backend services secured with OAuth through APIs created in the API Publisher. At the moment, you can call only services secured with username/password (Basic Auth/ Digest Auth).



