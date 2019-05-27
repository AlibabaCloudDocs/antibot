# Billing method {#concept_ihb_t4d_n2b .concept}

Anti-Bot Service employs a subscription-based billing method.

## Billing method {#section_ewx_54d_n2b .section}

**Billing item**: Depends on the subscription package.

**Payment method**: Subscription.

**Billing period**: The service is billed monthly or annually based on your order. A bill is generated each time you place an order.

**Subscription period**: Depends on the purchase date and subscription duration. You can select one of the following subscription durations: one month, three months, six months, one year, two years, and three years.

**Expiration**: The service stops automatically when the subscription period ends.

-   You will receive reminder emails or texts seven days before the expiration date. If you do not renew your subscription before the expiration date, Anti-Bot Service will stop protecting your site when the subscription period ends.
-   After the subscription period ends, your Anti-Bot Service configurations will be retained for seven days. If you renew your subscription within these seven days, you can continue to use the previous configurations. If you do not renew your subscription within these seven days, you must buy a new Anti-Bot instance and configure the instance from scratch to use Anti-Bot Service again.

## Pricing {#section_s4t_1zz_ngb .section}

The prices of Anti-Bot instances depend on the region and protection module.

|Required|Protection module|Feature|Default specification|Pricing|
|Chinese mainland|International|
|USD/Year|USD/Month|USD/Year|USD/Month|
|--------|-----------------|-------|---------------------|-------|
|----------------|-------------|
|--------|---------|--------|---------|
|Yes|Basic Defense|Provides basic protection against bot attacks for Web pages, HTML5, mobile apps, and API services.-   You can create custom rules to filter requests based on specific parameters.
-   You can limit the number of requests to specific URLs based on the IP address, cookie, or header fields of the request.
-   You can use multiple actions to handle suspicious requests, such as JavaScript validation, slider captcha, block, and monitoring.
-   You can use data risk control to protect service APIs from exploitation and misuse.
-   You can view protection reports and risk monitoring results.

| -   Supports HTTP, HTTPS, HTTP/2, and WebSocket.
-   Supports ports 80/8080 and 443/8443, and more than 50 [non-standard ports](intl.en-US/Pricing/Support for non-standard ports.md#).
-   Domains: You can only add one TLD and up to 10 subdomains or wildcard domains.

**Note:** If you add more TLDs, you are charged additional fees. For each [additional TLD](intl.en-US/Pricing/Increase the limit on domains.md#), Anti-Bot Service charges USD 236 per month.

-   Service request rate: 500 QPS

**Note:** If your service request rate exceeds the default limit, Anti-Bot Service charges USD 126 per month for [each 100 QPS](intl.en-US/Pricing/Increase the limits on the service bandwidth and request rate.md#section_h51_szh_4gb).

-   Service bandwidth: 100 Mbit/s for Alibaba Cloud-based services. 10 Mbit/s for non-Alibaba Cloud-based services.

**Note:** If your service bandwidth exceeds the default limit, Anti-Bot Service charges USD 126 per month for [each 10 Mbit/s](intl.en-US/Pricing/Increase the limits on the service bandwidth and request rate.md#section_hsq_std_n2b).


 |8,490.57|707.55|12,735.85|1,061.32|
|No|Bot Intelligence|Provides large amounts of cyber threat intelligence and updates protection policies against mass attacks. Intelligence sources:-   The malicious IP library and fingerprint database maintained by Alibaba Group, which has years of experience in network security.
-   Threat intelligence such as information about data centers, Web crawler libraries, and harassing phone calls
-   Intelligence about bot attacks in the security industry.

|-|8,490.57|707.55|12,735.85|1,061.32|
|No|App Protection|Provides your app with enhanced protection against bot traffic through SDK integration.-   You can integrate your app with the Anti-Bot SDK by following the integration guide.
-   You can establish secure connections between your app and the server, and ensure that only requests from legitimate devices are forwarded to the server.
-   You can access the fingerprint database maintained by Alibaba Group, which contains over 1 billion records of malicious devices.
-   You can easily identify more than 10 types of dangerous devices, such as emulators and high-risk devices.

|This feature supports only one app by default.If you add more apps for protection, you are charged additional fees. Anti-Bot Service charges USD XXX per month for each additional app.

**Note:** The Android and iOS version of an app count as one app.

|11,320.80|943.40|16,981.20|1,415.10|
|No|Customized algorithms|You can create a machine learning algorithm to analyze your business patterns and detect bot traffic accurately.You can customize your algorithm through deep learning and combine the algorithm with other protection modules to detect and handle bot traffic with more granularity. This helps improve protection capabilities.

|-|188,679.24|15,723.27|283,018.86|23,584.91|
|No|Managed Security Service|You can directly talk to our technical support professionals about anti-bot protection by joining an exclusive DingTalk group.-   **Basic service**: Provides consultation and technical support to help you configure Anti-Bot instances, including configurations of domains and related products.
-   **Value-added service**: Helps you analyze traffic patterns of bot attacks and customize protection policies to minimize negative effects on your business.

**Note:** Service availability: 8 hours/5 days. Guaranteed response within 30 minutes.


|-|56,603.76|4,716.98|84,905.64|7,075.47|

**Recommended configurations**

We recommend that you choose one of the following configurations based on your business type.

-   **Websites**: Basic Defense + Bot Intelligence.
-   **Apps**: Basic defense + App Protection
-   **Websites and apps**: Basic defense + Bot Intelligence + App Protection

**Note:** If your business requires a complex bot protection solution, we recommend that you use customized algorithms or Managed Security Service.

