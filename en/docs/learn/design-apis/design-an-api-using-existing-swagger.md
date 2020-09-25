# Design an API Using Existing Swagger Definition

A Swagger definition is a format that describes REST APIs. 
Follow the instructions below to design a REST API using the swagger definition of an existing API.

## Create an API using basic flow
1. Sign in to WSO2 API Cloud by providing your username and password. This opens the API Publisher portal.

2. Close the interactive tutorial that starts automatically if you are
    a first-time user, and then click **ADD NEW API**.


3. Select **I Have an Existing API** and then click **Start Creating**.

4. Select **OpenAPI URL** and provide `http://petstore.swagger.io/v2/swagger.json` as the URL. Click **NEXT**.

5.  Edit the information as given below and then click **CREATE**.

    | Field   | Sample value |
    |---------|--------------|
    | Name    | Petstore     |
    | Context | /petstore    |
    | Version | 1.0.0        |


    This redirects you to the overview page of the Petstore API.


## Resources
   Navigate to **Resources** tab and notice that all the **API resources** are created automatically when the Swagger URL is specified.
   

## API Definition
1. Navigate to **API Definition** and Click **Edit** to remove the security headers. This is required to invoke the API in the developer portal using the Swagger UI.


2. Remove the security tag from the `/pet` POST resource given below.

    **Swagger - Post resource**

    ``` java
        //remove the following code snippet
        security:
                - petstore_auth:
                    - 'write:pets'
                    - 'read:pets'
    ```

3.  Remove the security `pet/{petId}` GET resource given below:

    **Swagger - Get resource**

    ``` java
            //remove the following code snippet
    security:
            - api_key: []
    ```
4.  After removing the security tags, click **Update Contents** to save the changes.

## Endpoints

- Navigate to the **Endpoints** page, enter the information given below, and then click **SAVE**.

    | Field               | Sample value                                          |
    |---------------------|-------------------------------------------------------|
    | Endpoint type       | HTTP/REST endpoint                                    |
    | Production endpoint | http://petstore.swagger.io/v2/                        |
    | Sandbox endpoint    | Providing only the production endpoint is sufficient. |


## Runtime Configuration
  Navigate to **Runtime Configuration** page. 
  Transport Level Security  defines the transport protocol on which the API is exposed.

  <html><div class="admonition note">
     <p class="admonition-title">Note</p>
     <p> Both HTTP and HTTPS transports are selected by default. If you want to limit the API availability to only one transport (e.g., HTTPS), be sure to clear the checkbox of the other transport.</p>
     </div>
     </html>

## Subscriptions
   Navigate to **Subscriptions** page and select **Gold** and **Silver** as the Bussiness plans. After Click **SAVE**

   <html><div class="admonition note">
     <p class="admonition-title">Note</p>
     <p> The API can be available at different levels of service and allows you to limit the number of successful hits to an API during a given period of time.</p>
     </div>
     </html>


Now, you have successfully designed a REST API from an existing swagger definition. Next you can go ahead and publish the API.
       