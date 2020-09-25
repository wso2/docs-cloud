# Throttling and Rate Limiting Overview

Throttling and rate limiting policies allow you to limit access to your
APIs. Rate limiting allows you to ensure stability of an API when there
are too many requests coming in. Throttling allows you to limit the
number of successful hits to an API during a certain time frame,
typically in situations such as the following:

-   To protect your APIs from common types of security attacks such as
    Denial of Service (DoS) attacks.
-   To regulate traffic according to infrastructure availability.
-   To make an API, application, or a resource available to a consumer
    at different levels of service, usually for monetization purposes.

WSO2 API Cloud allows you to define throttling at the API, application,
resource, and subscription levels by creating required throttling
policies. You can apply one or more throttling policies at different
levels depending on your requirement. Take a look at the following
topics for detailed information on working with various throttling
policies:

-   [Advanced Throttling
    Policies](../advanced-throttling-policies)
-   [Application Throttling
    Policies](../application-throttling-policies)
-   [Subscription Throttling
    Policies](../../monetize-apis/subscription-throttling-policies)
-   [Blacklist Policies](../blacklist-policies)
