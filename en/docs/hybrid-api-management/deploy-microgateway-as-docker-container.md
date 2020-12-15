# Deploy the Microgateway as a Docker Container

!!! note
    
    Before you begin,
    
    Install Docker. For instructions, see [https://docs.docker.com/install](https://docs.docker.com/install).
    

1.  Sign in to [docker.cloud.wso2.com](http://docker.cloud.wso2.com)
    with your username and password.

    ``` java
    docker login docker.cloud.wso2.com
    Username: your_username@wso2.com
    Password: ******
    Login Succeeded
    ```

2.  Pull the docker image.</br> 
    A sample command is given below:

    ``` java
    docker pull docker.cloud.wso2.com/wso2am-cloud-micro-gw:2.6.0
    ```

3.  Run the docker container.

    ``` java
    docker run -p127.0.0.1:8243:8243 -p127.0.0.1:8280:8280 -e "WSO2_CLOUD_ORG_KEY=your_organization_key" -e "WSO2_CLOUD_EMAIL=your_username@wso2.com" -e "WSO2_CLOUD_PASSWORD=your_cloud_password" docker.cloud.wso2.com/wso2am-cloud-micro-gw:2.6.0
    ```

    You can enable gateway debug logs by
    passing the following environment variable when running the docker
    container:

    ``` java
    -e "LOG4J_PROPERTIES=log4j.logger.org.apache.synapse.transport.http.headers=DEBUG, log4j.logger.org.apache.synapse.transport.http.wire=DEBUG"
    ```

4.  [Test your
    Microgateway](../deploy-the-microgateway/#test-the-deployment).

-   If you create/update an API and publish/re-publish it from API Cloud
    Publisher, it could take up to a maximum of 10 minutes before your
    changes become effective in the Microgateway.
-   If you create/update a throttling tier from API Cloud, it could take
    up to a maximum of 15 minutes before your changes become effective
    in the Microgateway.
-   Statistics of API usage in your Microgateway are published to API
    Cloud every 6 to 6.5 hours.

