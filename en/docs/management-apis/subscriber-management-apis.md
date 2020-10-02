# Subscriber Management REST APIs

!!! tip
    
    Before you begin, follow the steps [here](../devportal-get-started) to get the OAuth bearer token with the
    `apim:subscribe` scope so that you can consume the APIs listed on this page.
      

## REST APIs that can be invoked with an admin access token

Following are the APIs that you can invoke with an access token generated with admin credentials.

### Subscriber Authentication API

####Request

<table>
<tbody>
<tr class="odd">
<td>HTTP Request method</td>
<td>POST</td>
</tr>
<tr class="even">
<td>URL</td>
<td>https://gateway.api.cloud.wso2.com/api/am/user/subscriber/authenticate/</td>
</tr>
<tr class="odd">
<td>Headers</td>
<td><p>Content-Type: application/json<br />
Authorization: Bearer &lt;Bearer token received by following prerequisites&gt;</p></td>
</tr>
<tr class="even">
<td>Payload</td>
<td><div class="content-wrapper">
<div class="code panel pdl" style="border-width: 1px;">
<div class="codeContent panelContent pdl">
<div class="sourceCode" id="cb1" data-syntaxhighlighter-params="brush: java; gutter: false; theme: Confluence" data-theme="Confluence" style="brush: java; gutter: false; theme: Confluence"><pre class="sourceCode java"><code class="sourceCode java"><a class="sourceLine" id="cb1-1" title="1">{</a>
<a class="sourceLine" id="cb1-2" title="2">    <span class="st">&quot;username&quot;</span>:<span class="st">&quot;alex@wso2.com@testcompany&quot;</span>,</a>
<a class="sourceLine" id="cb1-3" title="3">    <span class="st">&quot;password&quot;</span>:”xxxx”    </a>
<a class="sourceLine" id="cb1-4" title="4">}</a></code></pre></div>
</div>
</div>
<p>Username is constructed using the email address(alex@ <a href="http://wso2.com">wso2.com</a> ) and tenant domain(testcompany).</p>
</div></td>
</tr>
</tbody>
</table>

####Response

**Successful invocation**

``` java
{
   "success": true,
   "authenticated": true,
   "message": "User is successfully authenticated."
   }
   {
   "success": true,
   "authenticated": false,
   "message": "Authentication data is invalid."
}
```

**If the security token is invalid**

``` java
<ns1:XMLFault xmlns:ns1="http://cxf.apache.org/bindings/xformat">
   <ns1:faultstring>org.apache.cxf.interceptor.security.AuthenticationException: Unauthenticated request</ns1:faultstring>
</ns1:XMLFault>
```

!!! note
    
    The failure error given above will be converted into JSON format in a
    future releases of this API.
    

  

### Subscriber Invitation API

!!! tip
    
    Before you begin, be sure to enable self sign up to the API.
    
####Request

<table>
<tbody>
<tr class="odd">
<td>HTTP Request method</td>
<td>POST</td>
</tr>
<tr class="even">
<td>URL</td>
<td>https://gateway.api.cloud.wso2.com/api/am/user/subscriber/</td>
</tr>
<tr class="odd">
<td>Headers</td>
<td><p>Content-Type: application/json<br />
Authorization: Bearer &lt;Bearer token received by following prerequisites&gt;</p></td>
</tr>
<tr class="even">
<td>Payload</td>
<td><div class="content-wrapper">
<div class="code panel pdl" style="border-width: 1px;">
<div class="codeContent panelContent pdl">
<div class="sourceCode" id="cb1" data-syntaxhighlighter-params="brush: java; gutter: false; theme: Confluence" data-theme="Confluence" style="brush: java; gutter: false; theme: Confluence"><pre class="sourceCode java"><code class="sourceCode java"><a class="sourceLine" id="cb1-1" title="1">{</a>
<a class="sourceLine" id="cb1-2" title="2">    <span class="st">&quot;username&quot;</span>:<span class="st">&quot;alex.cse@gmail.com@testcompany&quot;</span>,   </a>
<a class="sourceLine" id="cb1-3" title="3">}</a></code></pre></div>
</div>
</div>
<p>Username is constructed using the email address(‘alex.cse@ <a href="http://gmail.com/">gmail.com</a> ’) and tenant domain(testcompany).</p>
</div></td>
</tr>
</tbody>
</table>


####Response

**Successful invocation**

``` java
{
   "success": true,
   "message": "User is invited successfully."    
}
```

**If the security token is invalid**

``` java
<ns1:XMLFault xmlns:ns1="http://cxf.apache.org/bindings/xformat">
   <ns1:faultstring>org.apache.cxf.interceptor.security.AuthenticationException: Unauthenticated request</ns1:faultstring>
</ns1:XMLFault>
```

!!! note
    
    The failure error given above will be converted into JSON format in the
    future releases of this API.
    

  

### Subscriber Invitation Verification API

!!! tip
    
    Before you begin...
    
    This API is required to invite a member or approve a self sign up
    request made by a user. You need to obtain the registration link of the
    user to invoke this API. This is an intermediate step to verify the
    confirmation key of members, before adding them to your organization
    
####Request

<table>
<tbody>
<tr class="odd">
<td>HTTP Request method</td>
<td>POST</td>
</tr>
<tr class="even">
<td>URL</td>
<td><a href="https://gateway.api.cloud.wso2.com/api/am/user/subscriber">https://gateway.api.cloud.wso2.com/api/am/user/subscriber</a> <a href="https://gateway.api.cloud.wso2.com/api/am/user/subscriber/authenticate/">/confirm-invitee/</a></td>
</tr>
<tr class="odd">
<td>Headers</td>
<td><p>Content-Type: application/json<br />
Authorization: Bearer &lt;Bearer token received by following prerequisites&gt;</p></td>
</tr>
<tr class="even">
<td>Payload</td>
<td><div class="content-wrapper">
<div class="code panel pdl" style="border-width: 1px;">
<div class="codeContent panelContent pdl">
<div class="sourceCode" id="cb1" data-syntaxhighlighter-params="brush: java; gutter: false; theme: Confluence" data-theme="Confluence" style="brush: java; gutter: false; theme: Confluence"><pre class="sourceCode java"><code class="sourceCode java"><a class="sourceLine" id="cb1-1" title="1">{</a>
<a class="sourceLine" id="cb1-2" title="2">        <span class="st">&quot;confirmationKey&quot;</span>:<span class="st">&quot;a346c52d-f9b0-4415-c409-00300dbc23ba&quot;</span>,</a>
<a class="sourceLine" id="cb1-3" title="3">        <span class="st">&quot;isStoreInvitee&quot;</span>:<span class="st">&quot;true&quot;</span>,</a>
<a class="sourceLine" id="cb1-4" title="4">        <span class="st">&quot;isInvitee&quot;</span>: <span class="kw">null</span></a>
<a class="sourceLine" id="cb1-5" title="5">}</a></code></pre></div>
</div>
</div>
</div></td>
</tr>
</tbody>
</table>

The confirmation key is retrieved from the invitation link received by
the end user you need to add to the organization. A sample is given
below.

``` java
https://wso2store.wso2.com/site/pages/confirm-verification.jag?confirmation=11508277-080d-45e4-b7ac-956f76c3f93f&isStoreInvitee=true&tenant=mycompany.
```

You need to extract the following information, required for the request
query parameters.

| Parameter                                       | Description                                                                                                    |
|-------------------------------------------------|----------------------------------------------------------------------------------------------------------------|
| `                isStoreInvitee               ` | Obtained from the one-time link of a self-signed up user. If not found, pass this parameter with a null value. |
| `                IsInvitee               `      | Obtained from the one-time link of an invited user. If not found, pass this parameter with a null value.       |


####Response

**Successful invocation for new users to WSO2 Cloud**

``` java
{
        "success":true,
        "message":"Successfully confirmed the the confirmation key for the user sam@wso2.com","data":"{\"confirmationKey\":\"a346c52d-f9b0-4415-c409-00300dbc23ba\",\"email\":\"sam@wso2.com\"}"
}
```

You can add the user after successful confirmation

**Successful invocation for existing users to WSO2 Cloud**

``` java
{
        "success":true,
        "message":"The user : sam@wso2.com has been successfully invited. Please use the same password to login"
}
```

**Unsuccessful invocation (Invalid code)**

``` java
 {
     "success":false,
     "message":"The link you are trying to click or the provided confirmation code has expired or is not valid"
}
```

  

### Subscriber Registration API

!!! tip
    
    The tenant admin is recommended to perform this task.
    

####Request

<table>
<tbody>
<tr class="odd">
<td>HTTP Request method</td>
<td>POST</td>
</tr>
<tr class="even">
<td>URL</td>
<td>https://gateway.api.cloud.wso2.com/api/am/user/subscriber <a href="https://gateway.api.cloud.wso2.com/api/am/user/subscriber/authenticate/">/</a> addUser</td>
</tr>
<tr class="odd">
<td>Headers</td>
<td><p>Content-Type: application/json<br />
Authorization: Bearer &lt;Bearer token received by following prerequisites&gt;</p></td>
</tr>
<tr class="even">
<td>Payload</td>
<td><div class="content-wrapper">
<div class="code panel pdl" style="border-width: 1px;">
<div class="codeContent panelContent pdl">
<div class="sourceCode" id="cb1" data-syntaxhighlighter-params="brush: java; gutter: false; theme: Confluence" data-theme="Confluence" style="brush: java; gutter: false; theme: Confluence"><pre class="sourceCode java"><code class="sourceCode java"><a class="sourceLine" id="cb1-1" title="1">{</a>
<a class="sourceLine" id="cb1-2" title="2">    <span class="st">&quot;confirmationKey&quot;</span> : <span class="st">&quot;63621eb8-b8f7-40a6-cf3b-af02e8db722a&quot;</span>,</a>
<a class="sourceLine" id="cb1-3" title="3">    <span class="st">&quot;password&quot;</span>:<span class="st">&quot;sam211!1&quot;</span>,</a>
<a class="sourceLine" id="cb1-4" title="4">    <span class="st">&quot;firstName&quot;</span>: <span class="st">&quot;Sam&quot;</span>,</a>
<a class="sourceLine" id="cb1-5" title="5">    <span class="st">&quot;lastName&quot;</span> : <span class="st">&quot;de Mel&quot;</span></a>
<a class="sourceLine" id="cb1-6" title="6">}</a></code></pre></div>
</div>
</div>
</div></td>
</tr>
</tbody>
</table>

The confirmation key is retrieved from the invitation link received by
the end user. Note the guidelines below to for the formats of the input
parameters

<table>
<thead>
<tr class="header">
<th>Parameter</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>                Password               </code></td>
<td><p>The password should have at least three of the criteria mentioned below.</p>
<ul>
<li>Uppercase letters</li>
<li>Lowercase letters</li>
<li>Numbers</li>
<li>Special characters</li>
</ul></td>
</tr>
<tr class="even">
<td><code>                firstName               </code></td>
<td>The first name of the user (alphanumeric characters only)</td>
</tr>
<tr class="odd">
<td><code>                lastName               </code></td>
<td>The last name of the user (alphanumeric characters only)</td>
</tr>
</tbody>
</table>

####Response

**Successful invocation**

``` java
{
    "success":true,
    "message":"Successfully added the user to the tenant testrest"
}
```

**Unsuccessful invocation**

``` java
{
    "success":false,"
    message":"Unable to retrieve user information. Invalid confirmation key provided. Please check the confirmation key and try again"
}
```

  

### Reset password APIs

#### Step 1 - Initiation of the password reset API

##### Reset password initiation API

####Request

<table>
<tbody>
<tr class="odd">
<td>HTTP Request method</td>
<td>POST</td>
</tr>
<tr class="even">
<td>URL</td>
<td>https://gateway.api.cloud.wso2.com/api/am/user/subscriber <a href="https://gateway.api.cloud.wso2.com/api/am/user/subscriber/authenticate/">/reset-password/initiate</a></td>
</tr>
<tr class="odd">
<td>Headers</td>
<td><p>Content-Type: application/json<br />
Authorization: Bearer &lt;Bearer token received by following prerequisites&gt;</p></td>
</tr>
<tr class="even">
<td>Payload</td>
<td><div class="content-wrapper">
<div class="code panel pdl" style="border-width: 1px;">
<div class="codeContent panelContent pdl">
<div class="sourceCode" id="cb1" data-syntaxhighlighter-params="brush: java; gutter: false; theme: Confluence" data-theme="Confluence" style="brush: java; gutter: false; theme: Confluence"><pre class="sourceCode java"><code class="sourceCode java"><a class="sourceLine" id="cb1-1" title="1">{</a>
<a class="sourceLine" id="cb1-2" title="2">    <span class="st">&quot;email&quot;</span>:<span class="st">&quot;sam@wso2.com&quot;</span>,</a>
<a class="sourceLine" id="cb1-3" title="3">    <span class="st">&quot;callbackURL&quot;</span>: <span class="st">&quot;http://myapp.com/reset-password&quot;</span></a>
<a class="sourceLine" id="cb1-4" title="4">}</a></code></pre></div>
</div>
</div>
<div class="table-wrap">
<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Parameter</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>                      email                     </code></td>
<td>The registration email of the user you need to reset the password of.</td>
</tr>
<tr class="even">
<td><code>                      callbackURL                     </code></td>
<td><p>The URL the user is redirected to once they receive the email to reset the password. Two parameters will be appended with the callback URL which are needed to make the next request. You do not need to append this as it will auto get appended to the URL provided above. You need to extract those two parameters and send it in the request 2.</p>
<p>If a callback URL is not specified then the redirection would be the default redirection to the wso2 cloud reset password page.</p>
<p>An example of such a custom callback URL returned to the user is shown below<br />
<code>                                                                        http://myapp.com/reset-password?id=sam@wso2.com&amp;confirmation=14f6b1dc-75b7-472c-8a1f-11455f669dbd                                                                     </code></p>
<div class="table-wrap">
<table>
<thead>
<tr class="header">
<th>Parameter</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>                           id                          </code></td>
<td>The email of the user</td>
</tr>
<tr class="even">
<td><code>                           confirmationCode                          </code></td>
<td>The confirmation code which is returned for the password reset to be passed to the request 2</td>
</tr>
</tbody>
</table>
</div></td>
</tr>
</tbody>
</table>
</div>
</div></td>
</tr>
</tbody>
</table>

!!! note
    
    Follow Step 2 and 3 after you are re-directed.
    
####Response

**Successful invocation**

``` java
{
    "success":true,
    "message":"Successfully added the user to the tenant testrest"
}
```

**Unsuccessful invocation (Invalid security token)**

``` java
{
    "success":false,"
    message":"Unable to retrieve user information. Invalid confirmation key provided. Please check the confirmation key and try again"
}
```

  

#### Step 2 - Verifying the input values for password reset

##### Reset password verification API

####Request

<table>
<tbody>
<tr class="odd">
<td>HTTP Request method</td>
<td>POST</td>
</tr>
<tr class="even">
<td>URL</td>
<td>https://gateway.api.cloud.wso2.com/api/am/user/subscriber /reset-password/verify</td>
</tr>
<tr class="odd">
<td>Headers</td>
<td><p>Content-Type: application/json<br />
Authorization: Bearer &lt;Bearer token received by following prerequisites&gt;</p></td>
</tr>
<tr class="even">
<td>Payload</td>
<td><div class="content-wrapper">
<div class="code panel pdl" style="border-width: 1px;">
<div class="codeContent panelContent pdl">
<div class="sourceCode" id="cb1" data-syntaxhighlighter-params="brush: java; gutter: false; theme: Confluence" data-theme="Confluence" style="brush: java; gutter: false; theme: Confluence"><pre class="sourceCode java"><code class="sourceCode java"><a class="sourceLine" id="cb1-1" title="1">{</a>
<a class="sourceLine" id="cb1-2" title="2"><span class="st">&quot;email&quot;</span>:<span class="st">&quot;sam@wso2.com&quot;</span>,</a>
<a class="sourceLine" id="cb1-3" title="3"><span class="st">&quot;confirmationKey&quot;</span>:<span class="st">&quot;14f6b1dc-75b7-472c-8a1f-11455f669dbd&quot;</span></a>
<a class="sourceLine" id="cb1-4" title="4">}</a></code></pre></div>
</div>
</div>
<div class="table-wrap">
<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Parameter</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>                      email                     </code></td>
<td>The ID returned from the request in Step 1.</td>
</tr>
<tr class="even">
<td><code>                      confirmationKey                     </code></td>
<td><p>The confirmation parameter appended to the callback URL in Step 1</p></td>
</tr>
</tbody>
</table>
</div>
</div></td>
</tr>
</tbody>
</table>

####Response

**Successful invocation**

``` java
{  
   "success":true,
   "message":"Provided verification code for the email sam@wso2.com has been successfully verified",
  "data":"{\"confirmationKey\":\"e0ed4sf-2a36s-40ae-80ea                          eeffc5c41e2c\",\"verified\":true,\"userName\":\"sam@wso2.com\",\"email\":\"sam@wso2.com\"}"
}
```

You have to extract the `             confirmationKey            ` from
`             data            ` for Step 3.

  

#### Step 3 - Confirming password reset with new password

##### Reset password confirmation API

####Request

<table>
<tbody>
<tr class="odd">
<td>HTTP Request method</td>
<td>POST</td>
</tr>
<tr class="even">
<td>URL</td>
<td>https://gateway.api.cloud.wso2.com/api/am/user/subscriber /reset-password/confirm</td>
</tr>
<tr class="odd">
<td>Headers</td>
<td><p>Content-Type: application/json<br />
Authorization: Bearer &lt;Bearer token received by following prerequisites&gt;</p></td>
</tr>
<tr class="even">
<td>Payload</td>
<td><div class="content-wrapper">
<div class="code panel pdl" style="border-width: 1px;">
<div class="codeContent panelContent pdl">
<div class="sourceCode" id="cb1" data-syntaxhighlighter-params="brush: java; gutter: false; theme: Confluence" data-theme="Confluence" style="brush: java; gutter: false; theme: Confluence"><pre class="sourceCode java"><code class="sourceCode java"><a class="sourceLine" id="cb1-1" title="1">{</a>
<a class="sourceLine" id="cb1-2" title="2"><span class="st">&quot;email&quot;</span>:<span class="st">&quot;sam@wso2.com&quot;</span>,</a>
<a class="sourceLine" id="cb1-3" title="3"><span class="st">&quot;confirmationKey&quot;</span>:<span class="st">&quot;d4602-264a-4ef8-95fa-ea03291c1d64&quot;</span>,</a>
<a class="sourceLine" id="cb1-4" title="4">“newPassword”:”XXXXXXX”</a>
<a class="sourceLine" id="cb1-5" title="5">}</a></code></pre></div>
</div>
</div>
<div class="table-wrap">
<table>
<thead>
<tr class="header">
<th>Parameter</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>                      email                     </code></td>
<td>The email returned from the data element in Step 2.</td>
</tr>
<tr class="even">
<td><code>                      confirmationKey                     </code></td>
<td>The key returned from the data element in Step 2.</td>
</tr>
<tr class="odd">
<td><code>                      newPassword                     </code></td>
<td>Your new password, after the reset.</td>
</tr>
</tbody>
</table>
</div>
</div></td>
</tr>
</tbody>
</table>

####Response

**Successful invocation**

``` java
{  
   "success":true,
   "message":"Password has been successfully reset for the user sam@wso2.com. Please login with your new password."
}
```

You have now successfully reset the password, after completing the steps
listed above.

## REST APIs that can be invoked with a subscriber access token

### API Store statistics API

######Request

<table>
<tbody>
<tr class="odd">
<td>HTTP Request method</td>
<td>POST</td>
</tr>
<tr class="even">
<td>URL</td>
<td>https://gateway.api.cloud.wso2.com/api/am/user/subscriber/statistics</td>
</tr>
<tr class="odd">
<td>Headers</td>
<td><p>Content-Type: application/json<br />
Authorization: Bearer &lt;Bearer token received by following prerequisites&gt;</p></td>
</tr>
<tr class="even">
<td>Payload</td>
<td><div class="content-wrapper">
<div class="code panel pdl" style="border-width: 1px;">
<div class="codeContent panelContent pdl">
<div class="sourceCode" id="cb1" data-syntaxhighlighter-params="brush: java; gutter: false; theme: Confluence" data-theme="Confluence" style="brush: java; gutter: false; theme: Confluence"><pre class="sourceCode java"><code class="sourceCode java"><a class="sourceLine" id="cb1-1" title="1">{</a>
<a class="sourceLine" id="cb1-2" title="2">    <span class="st">&quot;statisticsType&quot;</span> : <span class="st">&quot;getProviderAPIUsage&quot;</span>,</a>
<a class="sourceLine" id="cb1-3" title="3">    <span class="st">&quot;toDate&quot;</span>:<span class="st">&quot;2018-02-22 17:11&quot;</span>,</a>
<a class="sourceLine" id="cb1-4" title="4">    <span class="st">&quot;fromDate&quot;</span>: <span class="st">&quot;2016-09-28 00:00&quot;</span></a>
<a class="sourceLine" id="cb1-5" title="5">}</a></code></pre></div>
</div>
</div>
<div class="table-wrap">
<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Parameter</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>statisticsType</code></pre></td>
<td><p>The type of statistics you need to retrieve for a particular time period.</p>
<ul>
<li><p>getTopAppUsers - Top Users For Applications</p></li>
<li><p>getAppApiCallType - API Usage from Resource Path</p></li>
<li><p>getPerAppAPIFaultCount - Faulty Invocations per Application</p></li>
<li><p>getProviderAPIUsage - API Usage per Application</p></li>
</ul></td>
</tr>
<tr class="even">
<td><pre><code>toDate</code></pre></td>
<td>The end date of the required period.</td>
</tr>
<tr class="odd">
<td><pre><code>fromDate</code></pre></td>
<td>The start date of the required period.</td>
</tr>
</tbody>
</table>
</div>
<p><br />
</p>
<p><br />
</p>
</div></td>
</tr>
</tbody>
</table>

Note that your response will differ according to the requested type of
statistics. A successful invocation would be similar to the sample given
below.

####Response

**Successful invocation**

``` java
{  
   "success":true,
   "message":"Successfully retrieved the statistics data for the statistics type getTopAppUsers for the user sam@wso2.com@testcompany",
"data":"[{\"appName\":\"iot_ui_testcompany\",\"userCountArray\":[{\"count\":52,\"user\":\"sam@wso2.com@testcompany\"}]}]"
}
```
