# Common Cloud APIs

This section provides details of the common Cloud APIs that are available:

!!! note
    
    Before you add or delete users from your tenant, you must
    first sign in as admin to your tenant space in the Cloud.
    

### Login

<table>
<tbody>
<tr class="odd">
<td>Description</td>
<td>Log in to WSO2 Cloud's tenant space as admin.</td>
</tr>
<tr class="even">
<td>URI</td>
<td><p><code>                             https://cloudmgt.cloud.wso2.com/cloudmgt                                           /site/blocks/user/authenticate/ajax/login.jag                           </code></p></td>
</tr>
<tr class="odd">
<td>URI Parameters</td>
<td><div class="page" title="Page 2">
<section>
<div class="layoutArea">
<div class="column">
<ul>
<li>action: login</li>
<li><div class="page" title="Page 1">
<section>
<div class="layoutArea">
<div class="column">
<p>userName: Admin's username</p>
</div>
</div>
</section>
</div></li>
<li><div class="page" title="Page 1">
<section>
<div class="layoutArea">
<div class="column">
<p>password: Password of the admin</p>
</div>
</div>
</section>
</div></li>
</ul>
</div>
</div>
</section>
</div></td>
</tr>
<tr class="even">
<td>HTTP Methods</td>
<td>POST</td>
</tr>
<tr class="odd">
<td>Example</td>
<td><div class="content-wrapper">
<div class="page" title="Page 1">
<section>
<div class="layoutArea">
<div class="column">
<div class="page" title="Page 2">
<section>
<div class="layoutArea">
<div class="column">
<p><code>                       curl -c cookies -k -v -X POST https://cloudmgt.cloud.wso2.com/cloudmgt/site/blocks/user/authenticate/ajax/login.jag -d 'action=login&amp;userName=&lt;user name&gt; &amp;password=adminpassword'                      </code></p>
<div>
The <code>                       &lt;user name&gt;                      </code> should be <code>                       email@organization_key                      </code> . For example, if the e-mail is jhon@gmail.com, the <code>                       &lt;user name&gt;                      </code> should be <strong>jhon@gmail.com@organization_key</strong> . You can find the organization_key on the <strong>Manage</strong> page of the cloud.
</div>
</div>
</div>
</section>
</div>
</div>
</div>
</section>
</div>
</div></td>
</tr>
</tbody>
</table>

### addUserToTenant

<table>
<tbody>
<tr class="odd">
<td>Description</td>
<td>Create a new user in the Cloud</td>
</tr>
<tr class="even">
<td>URI</td>
<td><code>                           https://cloudmgt.cloud.wso2.com/cloudmgt/site/blocks/tenant/users/add/ajax/add.jag                                      </code></td>
</tr>
<tr class="odd">
<td>URI Parameters</td>
<td><div class="page" title="Page 2">
<section>
<div class="layoutArea">
<div class="column">
<ul>
<li>action: addUserToTenant</li>
<li>userEmail: Email address of the user</li>
<li>password: User's password should meet at least three of the below criteria:
<ul>
<li>Uppercase letters</li>
<li>Lowercase letters</li>
<li>Numbers</li>
<li>Special characters</li>
</ul></li>
<li>firstName: User's first name (alphanumeric characters only)</li>
<li>lastName: User's last name (alphanumeric characters only)</li>
<li>roles: User's roles. Can take one or more of the following roles in a comma-separated list: integrationclouduser, subscriber, publisher, admin, devicemgtuser, devicemgtadmin</li>
</ul>
</div>
</div>
</section>
</div></td>
</tr>
<tr class="even">
<td>HTTP Methods</td>
<td>POST</td>
</tr>
<tr class="odd">
<td>Example</td>
<td><div class="page">
<section>
<div class="layoutArea">
<div class="column">
<div class="page">
<section>
<div class="layoutArea">
<div class="column">
<p><code>                      curl -k -v -X POST                                            https://cloudmgt.cloud.wso2.com/cloudmgt/site/blocks/tenant/users/add/ajax/add.jag -b cookies -H 'Content­Type:application/x­www­form­urlencoded' -H 'Accept­Language:en­US,en;q=0.5' -­d 'action=addUserToTenant&amp;userEmail=myemail@wso2.com&amp;password=testPassword&amp;firstName=testFirstName&amp;lastName=testLastName&amp;roles=subscriber'                     </code></p>
</div>
</div>
</section>
</div>
</div>
</div>
</section>
</div></td>
</tr>
</tbody>
</table>

### deleteUserFromTenant

<table>
<tbody>
<tr class="odd">
<td>Description</td>
<td>Delete an existing user from your tenant</td>
</tr>
<tr class="even">
<td>URI</td>
<td><p><code>                             https://cloudmgt.cloud.wso2.com/cloudmgt/site/blocks/tenant/users/add/ajax/add.jag                           </code></p></td>
</tr>
<tr class="odd">
<td>URI Parameters</td>
<td><ul>
<li>action: deleteUserFromTenant</li>
<li>userName: Email address of the user</li>
</ul></td>
</tr>
<tr class="even">
<td>HTTP Methods</td>
<td>POST</td>
</tr>
<tr class="odd">
<td>Example</td>
<td><div class="page">
<section>
<div class="layoutArea">
<div class="column">
<div class="page">
<section>
<div class="layoutArea">
<div class="column">
<div class="page">
<section>
<div class="layoutArea">
<div class="column">
<p><code>                          curl -­b cookies -­k -v -X POST https://cloudmgt.cloud.wso2.com/cloudmgt/site/blocks/tenant/users/add/ajax/add.jag -­H 'Content­Type:application/x­www­form­urlencoded' -H 'Accept­Language:en­US,en;q=0.5'  -d 'action=deleteUserFromTenant&amp;userName=myemail@wso2.com'                         </code></p>
</div>
</div>
</section>
</div>
</div>
</div>
</section>
</div>
</div>
</div>
</section>
</div></td>
</tr>
</tbody>
</table>

### getUsersOfTenant

<table>
<tbody>
<tr class="odd">
<td>Description</td>
<td>Get all existing users of your tenant</td>
</tr>
<tr class="even">
<td>URI</td>
<td><p><code>                             https://cloudmgt.cloud.wso2.com/cloudmgt/site/blocks/tenant/users/get/ajax/get.jag                           </code></p></td>
</tr>
<tr class="odd">
<td>URI Parameters</td>
<td><ul>
<li>action: getUsersofTenant</li>
</ul></td>
</tr>
<tr class="even">
<td>HTTP Methods</td>
<td>POST</td>
</tr>
<tr class="odd">
<td>Example</td>
<td><div class="page">
<section>
<div class="layoutArea">
<div class="column">
<div class="page">
<section>
<div class="layoutArea">
<div class="column">
<div class="page">
<section>
<div class="layoutArea">
<div class="column">
<p><code>                          curl -­b cookies -­k -v -X POST https://cloudmgt.cloud.wso2.com/cloudmgt/site/blocks/tenant/users/get/ajax/get.jag -­H 'Content­Type:application/x­www­form­urlencoded' -H 'Accept­Language:en­US,en;q=0.5' -d 'action=getUsersofTenant'
</code></p>
</div>
</div>
</section>
</div>
</div>
</div>
</section>
</div>
</div>
</div>
</section>
</div></td>
</tr>
</tbody>
</table>

