# Solution overview {#concept_uz3_hvj_n2b .concept}

Anti-Bot Service \(Anti-Bot\) provides a security solution, Anti-Bot SDK, for native apps. It provides your apps with enhanced protection against bot traffic, supports secure communication, and can accurately identify suspicious IP addresses and modem pools.

The Anti-Bot SDK was developed based on years of experience in protecting against frauds and bargain speculators in their online business. After your app is integrated with the Anti-Bot SDK, your app will gain the same trusted channel as Tmall, Taobao, Alipay, and other apps. It will have access to a library of malicious devices accumulated by Alibaba Group against frauds and bargain speculators in their online business, helping you to solve your app's security problems.

The Anti-Bot SDK helps you to solve the following security problems that can threaten **native apps**:

-   Malicious registration, credential stuffing, and brute-force attacks
-   HTTP flood attacks against apps
-   Malicious attacks against SMS and CAPTCHA interfaces
-   Bargain speculation and red envelope snatching
-   Seckill and time-and-purchase-limited goods
-   Malicious ticket checking and brushing \(such as air tickets or hotel bookings\)
-   Valuable information crawling \(such as price, credit information, financing, and fiction\)
-   Machine batch voting
-   Spams and malicious comments

## Configure the Anti-Bot SDK for your app {#section_cfr_glm_n2b .section}

Perform the following steps to configure the Anti-Bot SDK for your app:

**Note:** You do not need to make any modifications on the server to configure the Anti-Bot SDK for your app. After the configuration is complete, Anti-Bot automatically filters out malicious traffic and forwards valid requests to the origin server. Anti-Bot handles all pressure from malicious traffic to ensure the stability of your server.

1.  Log on to the [Anti-Bot console](https://yundun.console.aliyun.com/?p=antibot), and select the region where your Anti-Bot instance is located.
2.  Go to the Domain Names page and click **Add Domain** to configure domain access to the domain name used by your app. For more information, see [Add domain name configuration](intl.en-US/Quick Start/Step 1: Add a domain name.md#).
3.  At the DNS resolution service provider of the domain name used by your app, add the CNAME allocated by your Anti-Bot instance, and point the domain name resolution of your app to the Anti-Bot instance. For more information, see [Update DNS settings](intl.en-US/Quick Start/Step 4: Modify DNS resolution.md#).
4.  Integrate the Anti-Bot SDK into your app.

    **Note:** This may take one to two days to complete.

    For more information about how to integrate the Anti-Bot SDK into your app, see the following documents:

    -   [iOS SDK integration guide](intl.en-US/User Guide/App protection/iOS SDK integration guide.md#)
    -   [Android SDK integration guide](intl.en-US/User Guide/App protection/Android SDK integration guide.md#)
5.  After verifying that the configuration is successful, package and publish the new app version integrated with the Anti-Bot SDK for security protection.

