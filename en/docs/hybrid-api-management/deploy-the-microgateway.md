# Deploy the Microgateway

This section walks you through the following Microgateway deployment
scenarios:

-   A single node Microgateway deployment.
-   A high availability deployment scenario where you have two
    Microgateway instances fronted by a load balancer.

!!! tip
    
    If you want to run the Microgateway on Docker, see [Deploying the
    Microgateway as a Docker
    Container](../deploy-microgateway-as-docker-container).
    

The following topics provide step-by-step instructions to get started
with your Microgateway deployment:

### Prerequisites

To download and run the Microgateway:

-   Ensure that you have the **Java SE Development Kit (JDK)**
    installed. You can install either [OpenJDK
    8](https://openjdk.java.net/install/) or [Oracle JDK 1.8.\*](https://www.oracle.com/java/technologies/javase-downloads.html).

    !!! note
    
        Important!
    
        WSO2 recommends installing JDK 8u161 or later.
    

-   Be sure that you meet the following system requirements:
     <table>
    <colgroup>
    <col style="width: 11%" />
    <col style="width: 88%" />
    </colgroup>
    <tbody>
    <tr class="odd">
    <td>Physical</td>
    <td><div class="content-wrapper">
    <ul>
    <li>3 GHz Dual-core Xeon/Opteron (or latest)</li>
    <li>4 GB RAM (2 GB for JVM and 2 GB for the operating system)</li>
    <li>10 GB free disk space</li>
    <li>~ Recommended minimum - 2 Cores.</br>
        <html>
     <div class="admonition note">
     <p class="admonition-title">Note</p>
     <p>For high concurrencies and better performance you can use 4 Cores.</p>
     </div>
     </html>
     </li>
     </ul>
    <p>Disk space is based on the expected storage requirement calculated by considering file uploads and backup policies.</p>
    </div></td>
    </tr>
    <tr class="even">
    <td>Virtual Machine (VM)</td>
    <td><ul>
    <li>2 compute units minimum (each unit having 1.0-1.2 GHz Opteron/Xeon processor)</li>
    <li>4 GB RAM</li>
    <li>10 GB free disk space</li>
    <li>One CPU unit for the operating system and one for JVM.</li>
    </ul>
    <p>~ 512 MB heap size. This is generally sufficient to process typical SOAP messages but the requirements vary with larger message sizes and the number of messages processed concurrently.</p></td>
    </tr>
    <tr class="odd">
    <td>EC2</td>
    <td><ul>
    <p>One c5.large instance to run one Microgateway instance.</p>
    </td>
    </tr>
    </tbody>
    </table>

###  Download a Microgateway instance

1.  Sign in to [WSO2 API Cloud](https://api.cloud.wso2.com/) ) as an
    admin user.

2.  On the API Publisher, click **Microgateways** .  
    ![](../assets/img/hybrid-api-management/click-microgateways.png)

3.  Click **DOWNLOAD MICROGATEWAY** to start the download. Once the Microgateway download completes, you can configure the Microgateway deployment depending on your use case.

### Configure the Microgateway deployment

Depending on your requirement you can either quickly [try out the basic
single node Microgateway deployment](#configure-a-single-node-microgateway-deployment) for testing purposes, or you can [try
out a production level high availability deployment](#configure-a production level high availability deployment).

#### Configure a single node Microgateway deployment

Follow the steps below if you want to configure a single node Microgateway deployment:

!!! tip
    
    Let’s refer to the Microgateway download location as
    `<MICROGATEWAY_HOME>` throughout this section.
    

1.  Navigate to `<MICROGATEWAY_HOME>/bin` , and
    execute the following command to start configuring the
    Microgateway:
    -  On Windows: `cloud-init.bat --run`.
    -  On Linux/Mac OS: `sh cloud-init.sh`.

    This allows you to configure the downloaded Microateway with the
    settings required to integrate with API Cloud.

2.  Provide your email address, organization key, and password.  
    Your organization key will be displayed as shown below.  
    ![](../assets/img/hybrid-api-management/organization-key.png)  
    The status of the Microgateway will be displayed on completion.  
    ![](../assets/img/hybrid-api-management/microgateway-status.png)
3.  Navigate to
    `<MICROGATEWAY_HOME>/bin`, and execute the following command to run the start up script:
    -  On Windows:`wso2server.bat --run`.
    -  On Linux/Mac OS: `sh wso2server.sh`.

    The Microgateway status will be updated when it starts.  
    ![](../assets/img/hybrid-api-management/updated-microgateway-status.png)  

Now you have configured a single Microgateway instance. The next step is
to [test the deployment](#test-the-deployment).


#### Configure a production level high availability deployment

Follow the steps below if you want to configure a production level high availability deployment:

!!! tip
    
    - In this high availability deployment you will have two Microgateway
    instances running on two nodes fronted by a load balancer as depicted in
    the following diagram:  
    ![](../assets/img/hybrid-api-management/high-availability-deployment.png)  
    Here, we will use NGINX is used as the load balancer.
    - We do not recommend running two Microgateway instances on a single node for production level high availability deployments.
    

1.  Be sure to download and run two Microgateway instances on two
    different nodes. Let’s refer to each Microgateway download location
    as `<MICROGATEWAY_HOME>` throughout this
    section.
    
    ??? info "Click here for instructions to run two Microgateway instances"
         Follow the steps below for each Microgateway instance that you downloaded.</br>1. Navigate to `<MICROGATEWAY_HOME>/bin`, and execute the following command to start configuring the Microgateway:</br>
          -  On Windows: `cloud-init.bat --run`.</br>
          -  On Linux/Mac OS: `sh cloud-init.sh`.</br> This allows you to configure the downloaded Microgateway with the settings required to integrate with API Cloud.</br>2. Provide your email address, organization key, and password.  
        Your organization key will be displayed as shown below:  
        ![](../assets/img/hybrid-api-management/organization-key.png)  
        The status of the Microgateway will be displayed on
        completion.  
        ![](../assets/img/hybrid-api-management/microgateway-status.png).</br>3. Navigate to`<MICROGATEWAY_HOME>/bin`, and execute the following command to run the start up script:  
        - On Windows: `wso2server.bat --run`.</br>
        - On Linux/Mac OS: `sh wso2server.sh`.</br>  
        The Microgateway status will be updated when it starts.  
        ![](../assets/img/hybrid-api-management/updated-microgateway-status.png).


2.  Install NGINX in a server configured in your
    cluster. For instructions on installing NGINX, see [installing NGINX
    community
    version](https://docs.nginx.com/nginx/admin-guide/installing-nginx/installing-nginx-open-source/#prebuilt)
    .
3.  Follow the steps below to create a SSL certificate for NGINX.
    1.  Create the server key.

        ``` java
        sudo openssl genrsa -des3 -out <key_name>.key 1024
        ```

    2.  Submit the certificate signing request (CSR).

        ``` java
                sudo openssl req -new -key <key_name>.key -out server.csr
        ```

    3.  Remove the password.

        ``` java
                sudo cp <key_name>.key <key_name>.key.org 
                sudo openssl rsa -in <key_name>.key.org -out <key_name>.key
        ```

    4.  Sign your SSL certificate.

        ``` java
                sudo openssl x509 -req -days 365 -in server.csr -signkey <key_name>.key -out <certificate_name>.crt
        ```

    5.  Copy the key and certificate files that you generated above to
        the `/etc/nginx/ssl/` location.

4.  Configure **NGINX** to direct HTTP and HTTPS requests based on your
    deployment.

    1.  Run the following command to identify the exact location of the
        `<NGINX_HOME>` directory.

        ``` java
        nginx -V
        ```

        Inspect the output to identify the
        `--prefix` tag that provides the
        location of the `<NGINX_HOME>`
        directory.

    2.  Update the `ngnix.conf` file with
        the required NGINX configuration given below. Alternatively, you
        can create a file with the `.conf`
        suffix and copy it to the
        `<NGINX_HOME>/conf.d` directory.

        !!! note
        
                Note the following with regard to the sample configuration
                below:
        
                -   `/etc/nginx/conf.d/hybrid_gateway_upstream.conf`
                    is the NGINX configuration file name.
                -   Placeholders `<IP1>` and
                    `<IP2>` represent the IP
                    addresses of Microgateway node 1 and node 2 respectively.
                -   `gateway.foo.com` is the
                    domain of the certificate you created in step 2 above. Note
                    that the DNS should be mapped to the NGINX public IP. If you
                    do not do the mapping, the client will have to add an entry
                    in `/etc/hosts` to resolve
                    the domain name.
                -   The key and the certificate for SSL is assumed to be in the
                    `<NGINX_HOME>/ssl/` location.
                    The placeholders `<cert.pem>`
                    and `<key.pem>` represent the
                    generated certificate file and key file.
                -   `/etc/nginx/log/wso2_hybrid_gateway/https/`
                    is the directory used for access logs. You need create the
                    directory if it does not exist.
        

        ``` java
        /etc/nginx/conf.d/hybrid_gateway_upstream.conf 
        upstream gateway_https {
            server <IP1>:8243;
            server <IP2>:8243;
        } 


        server {
            listen 80;
            server_name gateway.foo.com;
            rewrite ^/(.*) https://gateway_https/$1 permanent;
        }
         
        server {
            listen 443;
            server_name gateway.foo.com;
            proxy_set_header X-Forwarded-Port 443;
            ssl on;
            ssl_certificate /etc/nginx/ssl/<cert.pem>;
            ssl_certificate_key /etc/nginx/ssl/<key.pem>;
            location / {
                       proxy_set_header X-Forwarded-Host $host;
                       proxy_set_header X-Forwarded-Server $host;
                       proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
                       proxy_set_header Host $http_host;
                       proxy_read_timeout 5m;
                       proxy_send_timeout 5m;
                       proxy_pass https://gateway_https;
                }
         
                access_log /etc/nginx/log/wso2_hybrid_gateway/https/access.log;
                error_log /etc/nginx/log/wso2_hybrid_gateway/https/error.log;
        }
        ```

    3.  Execute the following command to restart the NGINX server:

        !!! tip
        
                You do not need to restart the server if you are simply making a
                modification to the VHost file. The following command is
                sufficient in such cases.
        
                ``` java
                sudo service nginx reload
                ```


        ``` java
        sudo service nginx restart
        ```

Once you configure the high availability deployment, the next step
is to test the deployment. Follow the instructions in the section below to test the deployment.

### Test the deployment

Follow the steps below to test your Microgateway deployment:

1.  Sign in to WSO2 API Cloud.

2.  Create and publish an API via the API Publisher portal.
    
3.  Subscribe to the API. For detailed information on how to subscribe, see [Subscribe to an API](../../learn/consume-apis/subscribe-to-an-api).
    
4.  [Invoke the API using
    curl](../../learn/consume-apis/invoke-an-api-using-curl)
    .  
    The curl command to invoke the GET method of the API should be
    similar to the following:  

    ``` java
        curl -k -X GET --header 'Accept: text/xml' --header 'Authorization: Bearer dXNlckBvcmcuY29tQHRlc3RPcmcxMjM6UGFzc3dvcmQ=’
        'https://gateway.api.cloud.wso2.com:443/t/ccc2222/phoneverify/1.0.0/CheckPhoneNumber?PhoneNumber=18006785432&LicenseKey=0'
    ```

    Replace
    `           https://gateway.api.cloud.wso2.com:443          ` in the
    above curl command with your Microgateway URL as indicated below,
    and then run it. The response to this curl should be identical to
    that received in the previous step.  

    ``` java
        curl -k -X GET --header 'Accept: text/xml' --header 'Authorization: Bearer dXNlckBvcmcuY29tQHRlc3RPcmcxMjM6UGFzc3dvcmQ=’
        'https://on-premise-gateway-ip:8243/t/ccc2222/phoneverify/1.0.0/CheckPhoneNumber?PhoneNumber=18006785432&LicenseKey=0'
    ```

    Note that you can also use the HTTP port for API invocations. The
    HTTP port number would be 8280 by default. An example is given
    below.

    ``` java
        curl -X GET --header 'Accept: text/xml' --header 'Authorization: Bearer dXNlckBvcmcuY29tQHRlc3RPcmcxMjM6UGFzc3dvcmQ=’
        'http://on-premise-gateway-ip:8280/t/ccc2222/phoneverify/1.0.0/CheckPhoneNumber?PhoneNumber=18006785432&LicenseKey=0'
    ```

5.  If your request is successful, your response will be similar to the
    following.  

    ``` java
        <?xml version="1.0" encoding="utf-8"?>
        <PhoneReturn xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://ws.cdyne.com/PhoneVerify/query">
          <Company>Toll Free</Company>
          <Valid>true</Valid>
          <Use>Assigned to a code holder for normal use.</Use>
          <State>TF</State>
          <RC />
          <OCN />
          <OriginalNumber>18006785432</OriginalNumber>
          <CleanNumber>8006785432</CleanNumber>
          <SwitchName />
          <SwitchType />
          <Country>United States</Country>
          <CLLI />
          <PrefixType>Landline</PrefixType>
          <LATA />
          <sms>Landline</sms>
          <Email />
          <AssignDate>Unknown</AssignDate>
          <TelecomCity />
          <TelecomCounty />
          <TelecomState>TF</TelecomState>
          <TelecomZip />
          <TimeZone />
          <Lat />
          <Long />
          <Wireless>false</Wireless>
          <LRN />
        </PhoneReturn>
    ```

