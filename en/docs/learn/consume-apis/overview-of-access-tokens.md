# Overview of Access Tokens

When an application developer registers an application on the API Store, the application is given a consumer-key and a consumer-secret, which represent the credentials of the application that is registered. The consumer-key becomes the unique identifier of the application, similar to a user's username, which is used to authenticate the user. When an access token is issued for an application, it is issued against the consumer-key.

API consumers generate access tokens and pass the tokens in the incoming API requests. The API key (i.e., the generated access token) is a simple string that you need to pass as an HTTP header. For example, `"Authorization: Bearer NtBQkXoKElu0H1a1fQ0DWfo6IX4a."` This works equally well for SOAP and REST calls.

Authorizing requests, which come to published APIs, The use of access tokens to authorize requests that come to published APIs help you **prevent certain types of denial-of-service (DoS) attacks**. If the token that is passed with a request is invalid, WSO2 API Cloud discards such requests in the first stage of processing.

WSO2 API Cloud supports two types of access tokens for authentication:

-   **Application Access Tokens** : Tokens to identify and authenticate an entire application. An application is a logical collection of many APIs. You can use a single application access token to invoke all APIs of an application.
-   **User Access Tokens** : Tokens to identify the final user of an application. For example, the final user of a mobile application deployed on different devices.

!!! note
        In WSO2 API-M the access token must be unique for the following combinations - `CONSUMER_KEY, AUTHZ_USER, USER_TYPE, TOKEN_STATE, TOKEN_STATE_ID` and `TOKEN_SCOPE`. The latter mentioned constraint is defined in the `IDN_OAUTH2_ACCESS_TOKEN` table. Therefore, it is not possible to have more than one Access Token for any of the above combinations.