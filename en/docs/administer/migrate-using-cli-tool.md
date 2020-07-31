# Migrate APIs and Applications to a Target Tenant Using the CLI Tool

WSO2 API Cloud allows you to export and import APIs and applications between tenants using a CLI tool. For example, if you have an API running in a particular tenant (e.g., kim@wso2.com@testorgs), you can use the CLI tool to export the API and then import it to another tenant environment (e.g., kim@wso2.com@testorg1). Therefore, you do not have to take the time to create APIs and applications from scratch when you want to have the same APIs and applications in a different tenant.

### Understand the API import/export tool

The API import/export tool uses a RESTful API protected by basic
authentication.

#### The export functionality

The API export functionality retrieves the information required for the
requested API from the registry and databases and generates a ZIP file,
which the exporter can download. This exported ZIP file has the
following structure:

![Structure of the exported ZIP
file](../assets/img/administer/zip-file-structure.png)

The structure of the ZIP file is described below:

<table>
<thead>
<tr class="header">
<th>Sub directory/File</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Meta Information</p></td>
<td><ul>
<li><p><code>                api.json:               </code> contains all the basic information required for an API to be imported to another environment</p></li>
<li><p><code>                swagger.json:               </code> contains the API swagger definition</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Documents</p></td>
<td><ul>
<li><p><code>                docs.json:               </code> contains the summary of all the documents available for the API</p></li>
<li><p>Add the uploaded files for API documentation also</p></li>
</ul></td>
</tr>
<tr class="odd">
<td>Image</td>
<td>Thumbnail image of the API</td>
</tr>
<tr class="even">
<td>WSDL</td>
<td>WSDL file of the API</td>
</tr>
<tr class="odd">
<td>Sequences</td>
<td>The sequences available for the API</td>
</tr>
</tbody>
</table>

#### The import functionality

The import functionality uploads the exported ZIP file of the API to the
target environment. It creates a new API with all the registry and
database resources exported from the source environment. Note the
following:

-   The life cycle status of an imported API will always be
    `CREATED` even when the original API in the
    source environment has a different state. This is to enable the
    importer to modify the API before publishing it.
-   Tiers and sequences are provider-specific. If an exported tier is
    not already available in the imported environment, that tier is not
    added to the new environment. However, if an exported sequence is
    not available in the imported environment, it is added.
-   The importer can decide whether to keep the original provider’s name
    or replace it. Set the
    `--preserve-provider` flag
    to true to keep it. If you set it to false, the original provider is
    replaced by the user who is sending the CLI command. When working
    with the API cloud you need to set this flag to false, because
    exporting and importing happen between tenants in the API cloud.
-   Cross-tenant imports are not allowed by preserving the original
    provider. For example, if an API is exported from tenant A and
    imported to tenant B, the value of the
    `--preserve-provider` flag must always be
    `false`.



### Get Started

!!! note
    
    After running the CLI tool be sure to add an environment before you
    start working with the import/export CLI commands.This is necessary because all APIs and applications need to be imported or exported to a specific environment.
  

#### Run the CLI tool

1.  Click [here](https://github.com/wso2/docs-cloud/tree/master/en/docs/assets/attachments/administer) to view the available CLI tool archives and download the appropriate archive depending on your operating system (i.e., Mac, Windows, or Linux).
2.  Once the download completes, extract the downloaded CLI tool to a preferred location and `cd` into it.
3.  Navigate to the working directory where the executable of the CLI
    tool resides.

4.  Execute the following command to start the CLI tool.

    ``` java
    ./apimcli
    ```

5.  Add the location of the extracted folder to your system's
    `$PATH` variable to be able to access the
    executable from anywhere.

    !!! note
    
        For further instructions execute the following command.
    
        ``` java
            apimcli --help
        ```
    

#### Set global flags for CLI tool

The following are some global flags that you can use with the CLI tool.

``` java
      --verbose
           Enable verbose logs (Provides more information on execution)
      --insecure, -k
          Allow connections to SSL sites without certs
      --help, -h
          Display information and example usage of a command
```

  

#### Add environment

You can add an environment by running the following CLI command.

!!! note
    
    In API cloud importing and exporting of APIs and Applications take place
    between tenants as opposed to environments. Therefore, you need to only
    add one environment in the CLI tool. This environment will be used
    between tenants to call the endpoints of the API cloud.
    

``` java
apimcli add-env
```

1.  Make sure that the CLI import/export tool is running.
2.  Run the following CLI command in the specified format depending on your operating system:

    -   Command format on Linux should be as follows:
 ``` java
   
        apimcli add-env -n <environment-name> \
                                --registration <registration-endpoint> \
                                --apim <API-Manager-endpoint> \
                                --token <token-endpoint> \
                                --import-export <endpoint-for-environment> \
                                --admin <admin-REST-API-endpoint> \
                                --api_list <API-listing-REST-API-endpoint> \
                                --app_list <application-listing-REST-API-endpoint>
 ```

         
           **The flags you can set are as follows:**

        Required flags:  
           `--name, -n` : As we only
            need one environment when working with the API cloud, name
            the environment as wso2apicloud
  
        There are no short flags for the following flags:
        -   `--registration`

        -   `--apim`

        -   `--token`

        -   `--import-export`

        -   `--admin`

        -   `--api_list`

        -   `--app_list`

        **Example**
        
        ``` java
        apimcli add-env -n wso2apicloud \
                              --registration https://gateway.api.cloud.wso2.com/client-registration/register \
                              --apim https://gateway.api.cloud.wso2.com/pulisher \
                              --token https://gateway.api.cloud.wso2.com/token \
                              --import-export https://gateway.api.cloud.wso2.com/api-import-export \
                              --admin https://gateway.api.cloud.wso2.com/api/am/admin/ \
                              --api_list https://gateway.api.cloud.wso2.com/api/am/publisher/apis \
                              --app_list https://gateway.api.cloud.wso2.com/api/am/store/applications
        ```

        **Response Format:**
        ``` java
        Successfully added environment '<environment-name>'
        ```

        **Example Response:**
        ``` java
        Successfully added environment 'wso2apicloud'
        ```
--------------------------------------------------------------------------------------


    -   Command format on Mac OS should be as follows: 
 ``` java
        apimcli add-env -n <environment-name> --registration <registration-endpoint> --apim <API-Manager-endpoint> --token <token-endpoint> --import-export <endpoint-for-environment> --admin <admin-REST-API-endpoint> --api_list <API-listing-REST-API-endpoint> --app_list <application-listing-REST-API-endpoint>
 ```

         
           **The flags you can set are as follows:**

        Required flags:  
           `--name, -n` : As we only
            need one environment when working with the API cloud, name
            the environment as wso2apicloud.
  
        There are no short flags for the following flags:
        -   `--registration`

        -   `--apim`

        -   `--token`

        -   `--import-export`

        -   `--admin`

        -   `--api_list`

        -   `--app_list`

        **Example**
 
        ``` java
        apimcli add-env -n wso2apicloud --registration https://gateway.api.cloud.wso2.com/client-registration/register --apim https://gateway.api.cloud.wso2.com/pulisher --token https://gateway.api.cloud.wso2.com/token --import-export https://gateway.api.cloud.wso2.com/api-import-export --admin https://gateway.api.cloud.wso2.com/api/am/admin/ --api_list https://gateway.api.cloud.wso2.com/api/am/publisher/apis --app_list https://gateway.api.cloud.wso2.com/api/am/store/applications
        ```

        **Response Format:**
        ``` java
        Successfully added environment '<environment-name>'
        ```

        **Example Response:**
        ``` java
        Successfully added environment 'wso2apicloud'
        ```

    !!! Troubleshooting
        **Why do I get the following error?**

        ``` java
           [ERROR]: parsing /Users/<user-profile-name>/.wso2apimcli/env_keys_all.yaml
           panic: runtime error: invalid memory address or nil pointer dereference
           [signal SIGSEGV: segmentation violation code=0x1 addr=0x0 pc=0x1343b82]
        ```
        You get the above error if you have worked with two CLI tools. Carry
        out the following steps if you get the above error:

        1.  View the `env_keys_all.yaml` file and
        check if there are any NULL values.

        2.  Delete the `env_keys_all.yaml` file.

        3.  Execute the command that you initially executed.  
        For example if you got this error when trying to add an
        environment, then follow the steps mentioned under [Adding an
        environment](#MigratingtheAPIsandApplicationstoaTargetTenantUsingtheCLITool-Addinganenvironment)
        to reattempt to add the environment .

#### List environments

1.  Make sure that the CLI import/export tool is running.
2.  Run the following CLI command to list the environments.  
    There are no flags for the following CLI command:

    -  **Command:**
       ``` java
        apimcli list envs
       ```
     
    -  **Response:**

         Environments available in file '/Users/kim/.wso2apimcli/main_config.yaml'
         <table>
         <thead>
         <tr class="header">
         <th>NAME</th>
         <th>PUBLISHER ENDPOINT</th>
         <th>REGISTRATION ENDPOINT</th>
         <th>TOKEN ENDPOINT</th>
         </tr>
         </thead>
         <tbody>
         <tr>
         <td><p>wso2apicloud</p></td>
         <td><p> https://gateway.api.cloud.wso2.com/pulisher</p></td>
         <td><p> https://gateway.api.cloud.wso2.com/client-registration/register</p></td>
         <td><p> https://gateway.api.cloud.wso2.com/token</p></td>
         </tr>
         </tbody>
         </table> 



### Migrate APIs to a target tenant

#### Export an API

1.  Make sure that the CLI import/export tool is running.
2.  Run the following CLI command to export an existing API as a
    `.zip` archive.
    -   **Command:**
    
        ``` java
        apimcli export-api -n <API-name> -v <version> -r <provider> -e <environment> -u <username> -p <password> -k
        ```

         ``` java
         apimcli export-api --name <API-name> --version <version> --provider <provider> --environment <environment> --username <username> --password <password> --insecure
         ```

         **Flags:**

         -   Required flags:
           -   `--name, -n`
           -   `--version, -v`
           -   `--provider, -r` : The provider should be as follows:                               `<username>@<organization-key>`  
              For example, `kim@wso2.com@testorgs`
           -   `--environment, -e` : The name of the environment that you created in the API cloud, which is as follows: wso2apicloud.              `
           -   `--insecure, -k` : This allows connections to SSL sites without certificates.
 

    -   **Example:**
        ``` java
        apimcli export-api -n PhoneVerification -v 1.0.0 -r kim@wso2.com@testorgs -e wso2apicloud -k
        ```

    -   **Response:**
        ``` java
        Successfully exported API!
        Find the exported API at /Users/kim/.wso2apimcli/exported/apis/wso2apicloud/PhoneVerification_1.0.0.zip
        ```


#### Import an API

!!! note
    
    When you import an API, regardless the status of the imported API it
    will be added with the created state and you need to sign in to the
    Publisher and publish the API.
    
You can use the archive created in the previous section to import APIs to an API Manager instance.

1.  Make sure that the CLI import/export tool is running.

    !!! note
    
        If you have enabled secure endpoints when creating the API and your
        username or/and password differs in the two environments, please
        follow the steps below before importing the API.
    
        1. Unzip the .zip archive created in the previous section.
    
        2\. Go to the `<API-name-version>/Meta-information`
        directory and open the `api.json` file.  
        For example,
        `PhoneVerification_1.0.0/Meta-information`
        directory and open the `api.json` file.
    
        3\. Modify the `endpointUTPassword` with your
        endpoint password and save the `api.json` file.
    
        4\. Compress the `PhoneVerification_1.0.0` folder to
        a folder named
        `myExportedAPI`.                     `
    

-   Run the following CLI command and when prompted for credentials enter your user name and password to import an API.
    -   **Command:**
    
        ``` java
        apimcli import-api -f <environment>/<file> -e <environment> -u <username> -p <password> --preserve-provider <preserve_provider> -k
        ```

         ``` java
         apimcli import-api --file <environment>/<file> --environment <environment> --username <username> --password <password> --preserve-provider <preserve_provider> --insecure
         ```

         **Flags:**

         -   Required flags:
             - `--file, -f` : The file path of the exported API. For example, if your file path is /Users/kim/.wso2apimcli/exported/apis/wso2apicloud/PhoneVerification\_1.0.0.zip.,
            then you need to enter
            `wso2apicloud/PhoneVerification_1.0.0.zip`
            as the value for this flag.
             -   `--environment, -e` : The name of the environment that you created in the API cloud, which is as follows: wso2apicloud.
             -   `--insecure, -k` : This allows connections to SSL sites without certificates.
             -   `--preserve-provider` : The importer can decide whether to keep the original provider’s name or replace it. When working with the API cloud, you need to set this value to false because you need to import the API from a different tenant and replace the original tenant's details.  

    -   **Example:**
        ``` java
        apimcli import-api -f wso2apicloud/PhoneVerification_1.0.0.zip -e wso2apicloud --preserve-provider=false -k
        ```

    -   **Response:**
        ``` java
        ZipFilePath is /Users/kim/.wso2apimcli/exported/apis/wso2apicloud/PhoneVerification_1.0.0.zip
        Successfully imported API wso2apicloud/PhoneVerification_1.0.0.zip
        ```


#### List APIs

!!! note
    
    If you happen to list APIs that belong to a particular tenant (e.g.,
    `kim@wso2.com@testorg1`) and then you want to list
    APIs that belong to aother tenant (e.g.,
    `kim@wso2.com@testorgs`), be sure to first reset the
    user before listing APIs again.
    

1. Make sure that the CLI import/export tool is running.
2. Run the following CLI command to list the APIs.

      <html>
         <div class="admonition info">
         <p class="admonition-title">Tip</p>
         <p>You need to specify the user name as `username@organization-key`. For example, `kim@wso2.com@testorgs`.</p>
         </div>
      </html>


    -   **Command:**
    
        ``` java
        apimcli list apis -e <environment> -k
        ```

         ``` java
         apimcli list apis --environment <environment> --insecure
         ```

         **Flags:**

         -   Required flags:
             - `--environment, -e` : The name of the environment that you created in the API cloud, which is as follows: wso2apicloud.
             -   `--insecure, -k`  

    -   **Example:**
        ``` java
        apimcli list apis -e wso2apicloud -k
        ```

    -   **Response:**
        ``` java
        Environment: wso2apicloud
        No. of APIs: 2
        +-------------------+---------+-------------------------+-----------+-----------------------+--------------------------------------+
        |       NAME        | VERSION |         CONTEXT         |  STATUS   |    PROVIDER           |                  ID                  |
        +-------------------+---------+-------------------------+-----------+-----------------------+--------------------------------------+
        | PhoneVerification | 1.0.0   | /t/testorg1/phoneverify | CREATED   | kim@wso2.com@testorg1 | e72e2291-d135-4a1c-ba03-9278ede71075 |
        | WorldBank         | 1.0.0   | /t/testorg1/wb          | PUBLISHED | kim@wso2.com@testorg1 | b89a62a7-c27a-4fcc-9d24-0db0ee63d289 |
        +-------------------+---------+-------------------------+-----------+-----------------------+--------------------------------------+
        ```


------------------------------------------------------------------------

### Migrate applications to a target tenant

#### Export an application

You can export applications from the Devportal and download them as a
zipped file.

1.  Make sure that the CLI import/export tool is running.
2.  Run the following CLI command to export an existing application as a
    `.zip` archive.

       <html>
         <div class="admonition info">
         <p class="admonition-title">Tip</p>
         <p>You need to specify the user name as `username@organization-key`. For example, `kim@wso2.com@testorgs`.</p>
         </div>
       </html>


    -   **Command:**
    
        ``` java
        apimcli export-app -n <application-name> -o <owner> -e <environment> -k
        ```

         ``` java
         apimcli export-app --name <application-name> --owner <owner> --environment <environment> --insecure
         ```

         **Flags:**

         -   Required flags:
             -   `--name, -n`
             -   `--owner, -o` : The owner should be as follows:        `<username>@<organization-key>`  
        For example, `kim@wso2.com@testorgs`
             -   `--environment, -e` : The name of the environment that you created in the API cloud, which is as follows: wso2apicloud.
             -   `--insecure, -k` : This allows connections to SSL sites without certificates.    

    -   **Example:**
        ``` java
        apimcli export-app -n TestApp -o kim@wso2.com@testorg1 -e wso2apicloud -k
        ```

    -   **Response:**
        ``` java
        ZipFilePath is /Users/kim/.wso2apimcli/exported/apis/wso2apicloud/PhoneVerification_1.0.0.zip
        Successfully imported API wso2apicloud/PhoneVerification_1.0.0.zip
        ```



#### Import an application

!!! note
    
    If you have been executing previous commands specifying credentials of a particular tenant and now you want to run the import application CLI command for another tenant, then you need to first reset the user before running the import an application command.
    

You can import an application to a target tenant as a zipped
application. When you import an application as a zipped file, a new
application is created within the target tenant.

1.  Make sure that the CLI import/export tool is running.
2.  Run the following CLI command to import an existing ap plicatio n as
    a `.zip` archive.
    -   **Command:**
    
        ``` java
        apimcli import-app -f <environment>/<file> -e <environment> -s <skip_subscriptions> -o <owner> -r <preserve_owner> -k
        ```

         ``` java
         apimcli import-app --file <environment>/<file> --environment <environment> --skipSubscriptions <skip_subscriptions> --owner <owner> --preserveOwner <preserve_owner> --insecure
         ```

         **Flags:**

         -   Required flags:
             - `--file, -f` : The file path of the exported App. For example, if your file path is /Users/kim/.wso2apimcli/exported/apps/wso2apicloud/kim@wso2.com@testorg1_TestApp.zip., then you need to enter
            `wso2apicloud/PhoneVerification_1.0.0.zip` as the value for this flag.
             -   `--environment, -e` : The name of the environment that you created in the API cloud, which is as follows: wso2apicloud.
             -   `--insecure, -k` : This allows connections to SSL sites without certificates.
             -   `--skipSubscriptions, -s`  
        You can opt to skip importing the subscriptions of the
        application by defining this flag. This parameter is set to
        false by default.
             -   `--owner, -o` The owner of the
        imported application can be specified by providing an username
        of a valid user based on your preference. The application
        importer can set the preferred owner’s username as the value of
        the `--owner` or
        `-o` flag.
             -   `--preserveOwner, -r`  
        You can also import the application by preserving the
        application owner information, based on the previous tenant. The
        application importer can add the
        `--preserveOwner` or `-r` flag in
        order to define that this flag is set to true. This parameter is
        set to false by default. Therefore, the default value is used
        when you do not define this flag. If you import the application
        without specifying any of the optional flags, you will be added
        as the owner of the application in the imported environment. If
        both the `--owner` and the
        `--preserveOwner` flags are set,
        then the `--owner` flag gets higher
        priority over the `--preserveOwner`
        flag. 

    -   **Example:**
        ``` java
        apimcli import-app -f wso2apicloud/kim@wso2.com@testorg1_TestApp.zip -e wso2apicloud -o kim@wso2.com@testorgs --preserveOwner --skipSubscriptions -u kim@wso2.com@testorgs -p admin123# -k

        ```

    -   **Response:**
        ``` java
        ZipFilePath is /Users/kim/.wso2apimcli/exported/apps/wso2apicloud/kim@wso2.com@testorg1_TestApp.zip
        Completed importing the Application wso2apicloud/kim@wso2.com@testorg1_TestApp..zip
        Succesfully imported Application!
        ```
  

#### List apps

1.  Make sure that the CLI import/export tool is running.
2.  Run the following CLI command to list the apps.

       <html>
         <div class="admonition info">
         <p class="admonition-title">Tip</p>
         <p>You need to specify the user name as `username@organization-key`. For example, `kim@wso2.com@testorgs`.</p>
         </div>
       </html>


    -   **Command:**
    
        ``` java
        apimcli list apps -e <environment> -o <owner> -k
        ```

         ``` java
         apimcli list apps --environment <environment> --owner <owner> --insecure
         ```

         **Flags:**

         -   Required flags:
             -   `--environment, -e` : The name of the environment that you created in the API cloud, which is as follows: wso2apicloud.
             -   `--owner, -o`
             -   `--insecure, -k` : This allows connections to SSL sites without certificates.    

    -   **Example:**
        ``` java
        apimcli list apps -e wso2apicloud -o admin -k

        ```

    -   **Response:**
        ``` java
        Environment: wso2apicloud
        No. of Applicationss: 2
        +--------------------------------------+--------------------+-------+---------+----------+
        |       ID                             |        NAME        | OWNER |  STATUS | GROUP-ID |                    
        +--------------------------------------+--------------------+-------+---------+----------+
        | e13b5bcf-dee5-48fe-9f23-bf46fc17a378 | DefaultApplication |       | APPROVED |          |
        | 153ad3d3-fa26-4dda-af54-27eee3327848 | TestApp.           |       | APPROVED |          |
        +--------------------------------------+--------------------+-------+---------+----------+

        ```


------------------------------------------------------------------------

### Reset user

If you want to list APIs or applications that belong to a particular tenant, you need to first reset the user before listing APIs or applications for the particular tenant.

1.  Make sure that the CLI import/export tool is running.
2.  Run the following CLI command to reset user details.
    -   **Command:**
    
        ``` java
        apimcli reset-user -e <environment>
        ```

         ``` java
         apimcli reset-user --environment <environment>
         ```

         **Flags:**

         -   Required flags:
             -   `--environment, -e` : The name of the environment that you created in the API cloud, which is as follows: wso2apicloud.
             
    -   **Example:**
        ``` java
        apimcli reset-user -e wso2apicloud

        ```

    -   **Response:**
        ``` java
        Successfully cleared user data for environment: wso2apicloud
        ```

------------------------------------------------------------------------

### Check the version of the CLI

1.  Make sure that the CLI import/export tool is running.
2.  Run the following CLI command to check the version of the CLI.
    -   **Command:**
    
        <html>
         <div class="admonition info">
         <p class="admonition-title">Tip</p>
         <p>There are no flags to set for the following CLI commands:</p>
         </div>
       </html>


        ``` java
        apimcli version
        ```

             
    -   **Example:**
        ``` java
        apimcli Version: 1.1.0
        ```

------------------------------------------------------------------------

### Set HTTP request timeout

1.  Make sure that the CLI import/export tool is running.
2.  Run the following CLI command to set the HTTP request timeout.
    -   **Command:**
    
        ``` java
        apimcli set --http-request-timeout <http-request-timeout>
        ```

         **Flags:**

         -   Required flags:
             -   `--http-request-timeout
             
    -   **Example:**
        ``` java
        apimcli set --http-request-timeout 10000

        ```

------------------------------------------------------------------------

### Set export directory

1.  Make sure that the CLI import/export tool is running.
2.  Run the following CLI command to the change the default location of
    the export directory.
    -   **Command:**
    
        ``` java
        apimcli set --export-directory <export-directory-path>
        ```
             
    -   **Example:**
        ``` java
        apimcli set --export-directory /Users/kim/Downloads/MyExports

        ```

