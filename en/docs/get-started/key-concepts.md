# Key Concepts

Let's take a look at some concepts and terminology that you need to know
in order to get started with WSO2 API Cloud.

### WSO2 Cloud's user model

You can register to all of the WSO2 Public Cloud offerings using a valid email address, and
create multiple organizations under the same login. The system creates a
unique tenant domain name for each organization you create. The user who
creates an organization is assigned admin rights to it.

In WSO2 Public Cloud, users are authorized by their email addresses and
are decoupled from organizations and tenant domains. This allows one
user to be in multiple organizations (tenant domains) at the same time
and sign in to each organization using a single email address. If users
are added to more than one organization, they are prompted to select the
organization before signing in to its Cloud.  

![WSO2-Cloud-user-model](../assets/img/key-concepts/wso2-cloud-user-model.png)
  
------------------------------------------------------------------------

### API Cloud components

The API Cloud comprises of the API Publisher portal, Devportal, Gateway, and the Key
Manager. Given below is a brief description of each component:

-   ####**API Publisher**
   Enables API providers to publish APIs, share documentation, provision API keys and gather feedback on API
    features, quality, and usage. The API Publisher is opened automatically when you sign in to the API Cloud.

-   ####**API Store** 
   API Store is a state-of-the-art web interface that allows API publishers to host and advertise their APIs, while allowing API consumers to self register, discover, evaluate, subscribe to and consume APIs. Any user can view the API Store of any tenant registered in the Cloud.
    If you know the name of the tenant, you can access its Store via
    the following URL:</br>
    **`https://api.cloud.wso2.com/store?tenant=>`**.

-   ####**API Gateway** 
   Secures, protects, manages, and scales API calls.
    It is a simple API proxy that intercepts API requests and applies
    policies such as throttling and security. It also gathers API usage
    statistics.
-   ####**API Key Manager** 
    Handles all security and key-related
    operations. API Gateway connects with the Key Manager to check the
    validity of OAuth tokens when APIs are invoked. The Key Manager also
    provides a token API to generate OAuth tokens that can be accessed
    via the Gateway.  
      
    When the API Gateway receives API calls, it contacts the Key Manager
    service to verify the validity of the tokens and do security checks.
    For example, when the Gateway receives a log call, it forwards the
    calls to the Key Manager server. You must pass username, password,
    consumer key and consumer secret key with it to register. All tokens
    used for validation are based on OAuth 2.0 protocol. Secure
    authorization of APIs is provided by the OAuth 2.0 standard for key
    management. The API Gateway supports API authentication with OAuth
    2.0 and enables IT organizations to enforce rate limits and
    throttling policies.

    When the API Gateway receives API invocation calls, it similarly
    contacts the API Key Manager service for verification. This
    verification call happens every time the Gateway receives an API
    invocation call if caching is not enabled at the Gateway level. For
    this verification, the Gateway passes an access token, the API and
    its version to the Key Manager.

    Communication between API Gateway and Key Manager happens either
    through a Web service call or a Thrift call. The default
    communication protocol is Apache
    [Thrift](http://thrift.apache.org/static/files/thrift-20070401.pdf)
    , which is an RPC framework used to develop scalable, cross-language
    services. Thrift is much faster than SOAP over HTTP communication.

   Additionally, statistics are provided by the monitoring component, which integrates with WSO2 Data Analytics Server.

------------------------------------------------------------------------  

### Users and roles

The API Cloud offers distinct community roles that are applicable to
most enterprises:

-   **APICloudPublisher** : A publisher manages a set of APIs across the
    enterprise or business unit and controls the API lifecycle,
    subscriptions, and monetization aspects. The publisher is also
    interested in usage patterns for APIs and has access to all API
    statistics.
-   **APICloudSubscriber** : A subscriber uses the API Devportal to discover
    APIs, read the documentation, and forums, rate/comment on the APIs,
    subscribes to APIs, obtain access tokens, and invoke the APIs.

------------------------------------------------------------------------

### API Lifecycle

An API is the published interface, while the Service is the
implementation running in the backend. APIs have their own lifecycles
independent of the backend Services they rely on. This
lifecycle is exposed in the API publisher portal and is managed
by the API publisher role.

Following are the default API lifecycle states:

-   **CREATED:** API metadata is added to the API Devportal, but it is not
    deployed in the API gateway and therefore, is not visible to
    subscribers in the API Devportal.
-   **PROTOTYPED:** the API is deployed and published in the API Devportal
    as a prototype.A prototyped API is usually a mock implementation
    made public in order to get feedback about its usability. Users can
    invoke the API without a subscription.
-   **PUBLISHED** : The API is visible in the API Devportal and available
    for subscription.
-   **DEPRECATED:** When an API is deprecated, new subscriptions are
    disabled. But the API is still deployed in the Gateway and is
    available at runtime to existing subscribers. Existing subscribers
    can continue to use it as usual until the API is retired.
-   **RETIRED** : The API is unpublished from the API gateway and
    deleted from the API Devportal.
-   **BLOCKED:** Access to the API is temporarily blocked. Runtime calls
    are blocked and the API is not shown in the API Devportal anymore.

------------------------------------------------------------------------

### Applications

An application is a logical collection of APIs. An application is
primarily used to decouple the consumer from the APIs. It allows you to:

-   Generate and use a single key for multiple APIs
-   Subscribe multiple times to a single API with different SLA levels

You subscribe to APIs through an application. Applications are available
at different SLA levels and have application-level throttling tiers
engaged in them. A throttling tier determines the maximum number of
calls you can make to an API during a given period of time.

The API Cloud comes with a pre-created, default application . You can
also create your own applications.

------------------------------------------------------------------------

### Access tokens

An **access token** i s a simple string that is passed as an HTTP header
of a request. For example, "`Authorization: Bearer NtBQkXoKElu0H1a1fQ0DWfo6IX4a`."
Access tokens authenticate API users and applications, and ensure better
security (e.g., prevent **DoS attacks** ). If a token that is passed
with a request is invalid, the request is discarded in the first stage
of processing. Access tokens work equally well for SOAP and REST calls.

There are two types of access tokens:

-   User access tokens
-   Application access tokens

#### User access tokens

Tokens to authenticate the final user of an API. User access tokens
allow you to invoke an API even from a third-party application like a
mobile app . You generate/renew a user access token by calling the Login
API through a REST client. For more information, see [Token
API](_Token_API_) .

#### Application access tokens

Tokens to authenticate an application, which is a logical collection of
APIs. They allow you to access all APIs associated with an application
using a single token, and also subscribe multiple times to a single API
with different SLA levels. Application access tokens leverage OAuth 2.0
to provide simple key management.

The steps below describe how to generate/renew application access
tokens:

1.  Sign in to the API Devportal.
2.  Click the **Applications** menu and then click the application to
    open it.

3.  Under the **Production Keys** tab, scroll down and click
    **Regenerate**.

### Throttling

Throttling allows you to limit the number of successful hits to an API
during a given period of time, typically in cases such as the following:

-   To protect your APIs from common types of security attacks such as
    denial of service (DoS).
-   To regulate traffic according to infrastructure availability.
-   To make an API, application or a resource available to a consumer at
    different levels of service, usually for monetization purposes.


------------------------------------------------------------------------

### API visibility and subscription

Visibility settings prevent certain user roles from viewing and
modifying APIs created by another user role.  

-   **Public** : the API is visible to all users (registered and
    anonymous), and can be advertised in multiple stores (central and
    non-WSO2 stores).
-   **Visible to my domain** : the API is visible to all users who are
    registered to the API's tenant domain.
-   **Restricted by Roles** : The API is visible to its tenant domain
    and only to the user roles that you specify. Accepted roles are
    admin, publisher, subscriber, and appclouduser.  

Given below is how visibility levels work for users in different roles:

-   API `creator` and `publisher`
    roles can see all APIs in their tenant Devportal even if you restrict
    access to them. This is because those roles have permission to view
    and edit all APIs in the API Publisher, and therefore, does not have
    to be restricted in the API Devportal.
-   Anonymous users can only see APIs that have visibility as
    `Public`.
-   Registered users can see
    -   public APIs of all tenant domains
    -   all APIs in the registered user's tenant domain as long as the
        API is not restricted to a role that the user is assigned to

An API's visibility is directly related to the API's **subscription
availability** because you cannot subscribe to something you don't see
in the API Devportal. 

------------------------------------------------------------------------

### API resources

An API is made up of one or more resources. Each resource handles a
particular type of request and is analogous to a method (function) in a
larger API.

API resources accept following attributes:  

<table>
<thead>
<tr class="header">
<th>Attribute name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>OAuth Scopes</td>
<td><a href="#KeyConcepts-OAuthscopes">OAuth scopes</a></td>
</tr>
<tr class="even">
<td>URL Pattern</td>
<td><div class="content-wrapper">
<p>A URL pattern can be one of the following types:</p>
<ul>
<li>As a url-mapping. E.g., <code>/state/town/*</code></li>
<li>As a uri-template. E.g., <code>/{state}/{town}</code></li>
</ul>
<p>The terms url-mapping and uri-template come from the [Synapse configuration language](https://synapse.apache.org/Synapse_Configuration_Language.html). When an API is published in the API Publisher, a corresponding XML definition is created in the API Gateway. This XML file has a dedicated section for defining resources. See examples below:</p>
<div class="code panel pdl" style="border-width: 1px;">
<div class="codeContent panelContent pdl">
<pre class="html/xml" data-syntaxhighlighter-params="brush: html/xml; gutter: false; theme: Confluence" data-theme="Confluence" style="brush: html/xml; gutter: false; theme: Confluence"><code>&lt;resource methods=&quot;POST GET&quot; url-mapping=&quot;/state/town/*&quot;&gt;
&lt;resource methods=&quot;POST GET&quot; uri-template=&quot;/{texas}/{houston}&quot;&gt;</code></pre>
</div>
</div>
<p>url <code>-mapping</code> performs a one-to-one mapping with the request URL, whereas the uri <code>-template</code> performs a pattern matching.</p>
<p>Parametrizing the URL allows the API Manager to map the incoming requests to the defined resource templates based on the message content and request URI. Once a uri-template is matched, the parameters in the template are populated appropriately. As per the above example, a request made to <a href="http://gatewa_hostgateway_port/">http://gatewa_host:gateway_port/api/v1/texas/houston</a> sets the value of <code>               state</code> to <code>texas</code> and the value of <code>town</code> to <code>               houston</code>. You can use these parameters within the synapse configuration for various purposes and gain access to these property values through the <code>               uri.var.province</code> and <code>uri.var.district</code> properties.</p></div></td>
</tr>
<tr class="odd">
<td>HTTP Verb</td>
<td>The HTTP methods that specify the desired action to be performed on the resource. These methods can be GET, POST, PUT, DELETE or OPTIONS. Multiple methods can be selected.</td>
</tr>
<tr class="even">
<td>Auth Type</td>
<td><p>The authentication type of each HTTP method of the resource. You can give one of the following:<br/>
</p>
<ul>
<li><strong>None</strong> : No authentication is applied and the API Gateway skips the authentication process</li>
<li><strong>Application</strong> : Authentication is done by the application. The resource accepts application access tokens.<br/>
</li>
<li><strong>Application User</strong> : Authentication is done by the application user. The resource accepts user access tokens.<br/>
</li>
<li><strong>Application and Application User</strong> : Both application and application user level authentication is applied. Note that if you select this option in the UI, it appears as <strong>Any</strong> in the API Manager's internal data storage and data representation, and <strong>Any</strong> will appear in the response messages as well.</li>
</ul>
<p><strong>Note</strong> that for the resources that have HTTP verbs (GET, POST etc.) requiring authentication (i.e., Auth Type is not NONE), set <strong>None</strong> as the Auth type of <strong>OPTIONS</strong> . This is to support Cross Origin Resource Sharing between the API Devportal and Gateway.</p>
<p>The auth type is cached in the API Manager for better performance. If you change the auth type through the UI, it takes about 15 minutes to refresh the cache. During that time, the server returns the old auth type from the cache.</p></td>
</tr>
</tbody>
</table>

Once a request is accepted by a resource, it will be mediated through an
in-sequence. Any response from the backend is handled through the
out-sequence. Fault sequences are used to mediate errors that might
occur in either sequence. The default in-sequence, out-sequence, and
fault sequences are generated when the API is published.  

------------------------------------------------------------------------

### Swagger API Console

WSO2 API Devportal provides an integrated Swagger UI, which is part of the
Swagger project. You can use it for interactive API documentation and to
invoke APIs.

[Swagger](http://swagger.io/) is a 100% open source,
standard, language-agnostic specification and a complete framework for
describing, producing, consuming, and visualizing RESTful APIs, without
the need of a proxy or third-party services. Swagger allows consumers to
understand the capabilities of a remote service without accessing its
source code and interact with the service with a minimal amount of
implementation logic. Swagger helps describe services in the same way
that interfaces describe lower-level programming code.

The [Swagger UI](https://github.com/swagger-api/swagger-ui) is a
dependency-free collection of HTML, JavaScript, and CSS that dynamically
generate documentation from a Swagger-compliant API. Swagger-compliant
APIs give you interactive documentation, client SDK generation, and more
discoverability. The Swagger UI has JSON code and its UI facilitates
easier code indentation, keyword highlighting and shows syntax errors on
the fly. You can add resource parameters, summaries and descriptions to
your APIs using the Swagger UI.

The API Publisher has integrated Swagger to facilitate simple,
**interactive API documentation** and invocation. The documentation is
given in a Swagger API definition, which is the JSON representation of
the API that is created using the information provided at the time the
API is created. The Swagger JSON files are saved in the registry. You
can edit the API definition using the **Edit Swagger Definition** button
in the API Publisher.

Also, see the [Swagger 2.0
specification](https://github.com/swagger-api/swagger-spec/blob/master/versions/2.0.md).

------------------------------------------------------------------------

### OAuth scopes

Scopes enable fine-grained access control to API resources based on user
roles. You define scopes to an API's resource. When a user invokes the
API, his/her OAuth 2 bearer token cannot grant access to any API
resource beyond its associated scopes.

You can apply scopes to an API resource at the time the API is created
or modified. In the API Publisher, click the **API -\> Add** menu (to
add a new API) or the **Edit** link next to an existing API. Then,
navigate to the **Manage** tab and scroll down to see the **Add Scopes**
button.

|                |                                                                                                                                                    |
|----------------|----------------------------------------------------------------------------------------------------------------------------------------------------|
| **Scope Key**  | A unique key for identifying the scope. Typically, it is prefixed by part of the API's name for uniqueness but is not necessarily reader-friendly. |
| **Scope Name** | A human-readable name for the scope. It typically says what the scope does.                                                                        |
| **Roles**      | The user role(s) that are allowed to obtain a token against this scope. E.g., manager, employee.                                                   |

T o illustrate the functionality of scopes, assume you have the
following scopes attached to resources of an API:

Assume that users named **Tom** and **John** are assigned the employee
role and both the employee and manager roles respectively *.*

Tom requests a token through the Token API as
`grant_type=password&username=nuwan&password=xxxx&scope=news_read                            news_write`. However, as Tom is not in the manager role, he will only be granted a
token bearing the news\_read scope. The response from the Token API will
be similar to the following:

``` java
"scope":"news_read",
"token_type":"bearer",
"expires_in":3299,
"refresh_token":"8579facb65d1d3eba74a395a2e78dd6",
"access_token":"eb51eff0b4d85cda1eb1d312c5b6a3b8"
```

Next, John requests a token as
`         grant_type=password&username=john&password=john123&scope=                   news_read news_write                 `
. As John has both roles assigned, the token will bear both the
requested scopes and the response will be similar to the following:

``` java
"scope":"news_read news_write", 
"token_type":"bearer", 
"expires_in":3299, 
"refresh_token":"4ca244fb321bd555bd3d555df39315",
"access_token":"42a377a0101877d1d9e29c5f30857e"
```

T his means that Tom can only access the GET operation of the API while
John can access both as he is assigned to both the employee and manager
roles. If Tom tries to access the POST operation, there will be an HTTP
403 Forbidden error as follows:

``` xml
<ams:fault xmlns:ams="http://wso2.org/apimanager/security">
   <ams:code>900910</ams:code>
      <ams:message>The access token does not allow you to access the requested resource</ams:message>
      <ams:description>Access failure for API: /orgnews, version: 1.0.0 with key: eb51eff0b4d85cda1eb1d312c5b6a3b8
   </ams:description>
</ams:fault>
```

------------------------------------------------------------------------  

### Endpoints

An endpoint is a specific destination for a message such as an address,
WSDL, a failover group, a load-balance group etc.

WSO2 API Cloud supports a range of different endpoint types that
allow the API Gateway to connect with advanced types of backends. It
supports such as HTTP endpoints, URL endpoints (also known as address endpoint), WSDL
endpoints, Failover endpoints, and Load-balanced endpoints. 

Note the following:

-   You can expose both REST and SOAP services to consumers through
    APIs.
-   You cannot call backend services secured with OAuth through APIs
    created in the API Publisher. At the moment, you can call only
    services secured with username/password.
-   The system reads gateway endpoints from the
    `api-manager.xml` file. When there are multiple
    gateway environments defined, it picks the gateway endpoint of the
    production environment. You can define both HTTP and HTTPS gateway
    endpoints as follows:

    `<GatewayEndpoint>http://${carbon.local.ip}:${http.nio.port},https://${carbon.local.ip}:${https.nio.port}</GatewayEndpoint>          `

-   If both types of endpoints are defined, the HTTPS endpoint will be
    picked as the server endpoint.

------------------------------------------------------------------------

### Sequences

The API Cloud has a default mediation flow that is executed in each API
invocation. There are 3 default sequences engaged as
`in`, `out` and
`fault`.

<table>
<thead>
<tr class="header">
<th>Sequence</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>in</td>
<td>In-sequence is the first place that will be mediated through, once a request is dispatched to a resource of an API. At the end of the in-sequence the request can be forwarded to a back-end application for further processing.</td>
</tr>
<tr class="even">
<td>out</td>
<td>Any responses coming from the back-end system are mediated through the out-sequence of the resource of the API.</td>
</tr>
<tr class="odd">
<td>fault</td>
<td><p>Fault sequence is there to handle any errors that may occur while mediating a message through a resource.</p>
<div>
When the sequence or the proxy service encounters an error during mediation or while forwarding a message, the message that triggered the error is delegated to the specified fault sequence. Using the available mediators it is possible to log the erroneous message, forward it to a special error-tracking service, and send a SOAP fault back to the client indicating the error. We need to configure the fault sequence with the correct error handling instead of simply dropping messages.
</div></td>
</tr>
</tbody>
</table>
  

------------------------------------------------------------------------

### Mediators

Sometimes, the backend implementation of a Web service does not exactly
match your desired API design. In that case, you do various message
transformations and orchestrate multiple backend services to achieve the
design you want.

The API Cloud comes with a powerful mediation engine that can transform
and orchestrate API calls on the fly. It is built on the WSO2 ESB and
supports a variety of mediators that you can use as building blocks for
your sequences. Given below is the list of mediators supported in the
API Cloud:

<table>
<thead>
<tr class="header">
<th>Category</th>
<th>Mediator</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Core</td>
<td>Call</td>
<td>Invokes a service in non-blocking, synchronous manner.</td>
</tr>
<tr class="even">
<td><br />
</td>
<td><p>Sequence</p></td>
<td>Inserts a reference to a sequence.</td>
</tr>
<tr class="odd">
<td><br />
</td>
<td>Drop</td>
<td>Drops a message.</td>
</tr>
<tr class="even">
<td><br />
</td>
<td><p>Enrich</p></td>
<td>Enriches a message.</td>
</tr>
<tr class="odd">
<td><br />
</td>
<td><p>Property</p></td>
<td>Sets or removes properties associated with the message.</td>
</tr>
<tr class="even">
<td><br />
</td>
<td>Log</td>
<td>Logs a message.</td>
</tr>
<tr class="odd">
<td>Filter</td>
<td>Filter</td>
<td>Filters a message using XPath, if-else type of logic.</td>
</tr>
<tr class="even">
<td><br />
</td>
<td><p>Validate</p></td>
<td>Validates XML messages against a specified schema.</td>
</tr>
<tr class="odd">
<td><br />
</td>
<td><p>Switch</p></td>
<td>Filters messages using XPath and switch logic.</td>
</tr>
<tr class="even">
<td><br />
</td>
<td><p>ConditionalRouter</p></td>
<td>Implements complex routing rules (header-based routing, content-based routing, and other rules).</td>
</tr>
<tr class="odd">
<td>Transform</td>
<td><p>XSLT</p></td>
<td>Performs XSLT transformations on the XML payload.</td>
</tr>
<tr class="even">
<td><br />
</td>
<td><p>FastXSLT</p></td>
<td>Performs XSLT transformations on the message stream.</td>
</tr>
<tr class="odd">
<td><br />
</td>
<td><p>URLRewrite</p></td>
<td>Modifies and rewrites URLs or URL fragments.</td>
</tr>
<tr class="even">
<td><br />
</td>
<td><p>XQuery</p></td>
<td>Performs XQuery transformation.</td>
</tr>
<tr class="odd">
<td><br />
</td>
<td><p>Header</p></td>
<td>Sets or removes SOAP headers.</td>
</tr>
<tr class="even">
<td><br />
</td>
<td><p>Fault (also called Makefault)</p></td>
<td>Creates SOAP Faults.</td>
</tr>
<tr class="odd">
<td><br />
</td>
<td><p>PayloadFactory</p></td>
<td>Transforms or replaces message content in between the client and the backend server.</td>
</tr>
<tr class="even">
<td>Advanced</td>
<td>Cache</td>
<td>Evaluates messages based on whether the same message came to the ESB.</td>
</tr>
<tr class="odd">
<td><br />
</td>
<td><p>ForEach</p></td>
<td>Splits a message into a number of different messages by finding matching elements in an XPath expression of the original message.</td>
</tr>
<tr class="even">
<td><br />
</td>
<td><p>Clone</p></td>
<td>Clones a message.</td>
</tr>
<tr class="odd">
<td><br />
</td>
<td><p>Iterate</p></td>
<td>Splits a message.</td>
</tr>
<tr class="even">
<td><br />
</td>
<td><p>Aggregate</p></td>
<td>Combines a message.</td>
</tr>
<tr class="odd">
<td><br />
</td>
<td><p>Callout</p></td>
<td>Blocks Web service calls.</td>
</tr>
<tr class="even">
<td><br />
</td>
<td><p>Transaction</p></td>
<td>Executes a set of mediators transactionally.</td>
</tr>
<tr class="odd">
<td><br />
</td>
<td>DBReport</td>
<td>Writes data to the database.</td>
</tr>
<tr class="even">
<td><br />
</td>
<td><p>DBLookup</p></td>
<td>Retrieves information from the database.</td>
</tr>
<tr class="odd">
<td><br />
</td>
<td><p>Entitlement</p></td>
<td>Evaluates user actions against a XACML policy.</td>
</tr>
<tr class="even">
<td><br />
</td>
<td><p>Script</p></td>
<td>Executes a mediator written in Scripting language.</td>
</tr>
</tbody>
</table>

You can extend the API Gateway's default mediation flow to do custom
mediation by providing an extension as a Synapse mediation sequence. You
can design all the sequences using a tool like WSO2 Integration Studio and then
store the sequence in the Gateway's registry. 

------------------------------------------------------------------------  

### Response caching

Response caching stores the response messages per each API in a cache .
It improves performance because the backend server does not have to
process the same data for a request multiple times. To offset the risk
of stale data in the cache, you can set a time period after which the
cache is cleared periodically.

Response caching is automatically disabled in the Cloud. You can enable
it when creating a new API or editing an existing API. Go to the API's
**Manage** tab in the API Publisher, and select
`Enable` from the **Response Caching** drop-down list
and give a time-out period. 

------------------------------------------------------------------------

### Gateway caching

When an API call hits the API Gateway, the Gateway carries out security
checks to verify if the token is valid. During these verifications, the
API Gateway extracts parameters such as access token, API, and API
version that are passed to it. Since all traffic to APIs goes through
the API Gateway, this verification process can become an overhead if the
API name, version, and other validation information are not cached.
Therefore, caching is enabled at the Gateway by default.

When caching is enabled and a request hits the Gateway, it first
populates the cached entry for a given token. If a cache entry does not
exist in the cache, it calls the Key Manager server. This process is
carried out using Web Service calls. Once the Key Manager server returns
the validation information, it gets stored in the Gateway. Because the
API Gateway issues a Web service call to the key manager server only if
it does not have a cache entry, the number of Web service calls to the
key manager server is reduced.

------------------------------------------------------------------------

### Admin Portal

WSO2 API Cloud provides you an admin portal which allows to perform
administration on the Applications and APIs you have published. The left
navigation bar of the admin portal directs to different administration
tasks as below.

<table>
<colgroup>
<col style="width: 16%" />
<col style="width: 83%" />
</colgroup>
<tbody>
<tr class="odd">
<td>THROTTLING POLICIES</td>
<td><p>THROTTLING POLICIES contains the settings for the throttling configurations of API Manager. Under that,</p>
<p>ADVANCED THROTTLING - Allows you to create and update advanced throttling polices.
<p>APPLICATION TIERS - Allows you to create and update application level throttling tiers. </p>
<p>SUBSCRIPTION TIERS - Allows you to create and update API subscription level throttling tiers.</p>
<p>BLACK LIST - Blacklists requests by APIs, Applications, Users and IP Addresses.</p></td>
</tr>
<tr class="even">
<td>LOG ANALYZER</td>
<td><p>Allows you to view and download load balancer logs as well as Gateway logs for a specified time period</p></td>
</tr>
<tr class="odd">
<td>ANALYTICS</td>
<td><p>API AVAILABILITY - provides statistics of API Availability</p>
<p>MANAGE ALERTS - provides configuring alerts for different behaviors of APIs, requests, response times etc.</p></td>
</tr>
</tbody>
</table>


