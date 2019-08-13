# Bot intelligence {#task_rvz_xmp_tgb .task}

The bot intelligence rule is backed with the Alibaba Cloud Bot Intelligence Library and helps you allow requests from valid crawlers and inspect suspicious requests from known threatening source IPs.

The Alibaba Cloud Bot Intelligence Library is calculated based on Alibaba Cloud's network-wide traffic and is updated in real time. It covers the following source IP characteristics:

-   Valid crawlers: Dynamically updated source IP library of crawlers of mainstream search engines, including Google, Bing, Baidu, sogou, 360, and yandex.

    You can enable the default valid crawler rule to allow requests from the specified search engines. The Blacklist and Whitelist, and Access Control List features still apply to the valid crawler requests.

-   Threat intelligence: Malicious crawler IP library calculated in real time based on Alibaba Cloud's network-wide threat intelligence, and dynamically updated public cloud/IDC IP libraries.

    You can customize the threat intelligence rule to trigger different protection actions against requests from different types of blacklist IP addresses. Options are monitoring, interception, JavaScript verification, and slider verification. In addition, you can configure protection for some key interfaces against specific blacklisted IP addresses to avoid impact on other business logic.


1.  Log on to the [Anti-Bot Service management console](https://yundun.console.aliyun.com/?p=antibot). 
2.  In the left-side navigation pane, select **Protection** \> **Bot Intelligence**. 
3.   In the domain name drop-down box, select the domain name to be configured.![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/123806/156569185738754_en-US.png)

 
4.  Complete the following configuration respectively on the Allowed Crawlers and Threat Intelligence tab pages. 
    -   Allow valid crawlers
        1.  On the Allowed Crawler tab page, turn on the **Enable** switch.

            **Note:** If you no longer need this feature, turn off the **Enable** switch on this page.

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/123806/156569185738738_en-US.jpg)

        2.  In the rule list, locate to a valid crawler according to the **Intelligence Name**, and turn on the corresponding **Status** switch to allow requests from it. Currently, crawling requests from the following search engines can be configured: GoogleBot, BingBot, BaiduSpider, SogouSpider, 360 Spider, and YandexBot.

            **Note:** Alternatively, you can only enable rule 106 \(**Legit Crawling Bots**\) to allow all supported search engine bots.

    -   Add a threat intelligence rule
        1.  On the Threat Intelligence tab page, turn on the **Enable** switch.

            **Note:** If you no longer need this feature, turn off the **Enable** switch on this page.

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/123806/156569185738753_en-US.png)

        2.  In the rule list, locate to an IP blacklist according to the **Intelligence Name**, and turn on the corresponding **Status** switch. The optional IP blacklists are as follows:

            |IP Blacklist|Description|
            |------------|-----------|
            |**Malicious Scanner Fingerprint Blacklist**|The common scanners.|
            |**Malicious Scanner IP Blacklist**|A dynamic IP library that is obtained by analyzing the source IP addresses of malicious scanning behaviors detected by Alibaba Cloud in real time.|
            |**Credential Stuffing IP Blacklist**|A dynamic IP library that is obtained by analyzing the source IP addresses of credential stuffing and brute-force cracking behaviors detected by Alibaba Cloud in real time.|
            |**Fake Crawler Blacklist**|Invalid crawlers that forge the user-agent of legitimate search engines \(such as baiduspider\) to avoid detection.**Note:** Before enabling this rule, make sure that you have allowed valid crawler requests. Otherwise, false positives may occur.

|
            |**Malicious Crawler IP Blacklist**|A dynamic IP library that is obtained by analyzing the source IP addresses of malicious crawling behaviors detected by Alibaba Cloud in real time.This IP blacklist has three levels: Low, Medium, and High. The higher the level, the more IP addresses are included and the higher the possibility of false positives.

We recommend that you enable two-step verification for the high-level blacklist. Options are using slider verification or JS verification. For interfaces that do not apply to two-step verification \(such as APIs\), you can enable the low-level blacklist rule.

|
            |**IDC IP List**|The following IDC IP lists are covered: Alibaba Cloud, Tencent Cloud, Meituan Cloud, 21 Vianet, and Others. These IP segments are often used by crawlers to deploy crawling programs or act as proxies, and are seldom used by normal users.|

            After the default threat intelligence rule is enabled, when the source IP address in the specified blacklist initiates an access request to any path under the domain name, the monitoring operation is triggered. That is, the request is allowed and recorded.

            If you want to modify the default rules \(for example, specify the key interfaces to be protected or change the disposal action\), follow these steps to customize threat intelligence rules.

        3.  \(Optional\) Select the default rule to be configured and click **Edit**.
        4.  \(Optional\) In the Edit Intelligence dialog box, complete the following configuration:

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/123806/156569185838755_en-US.png)

            |Configuration|Description|
            |-------------|-----------|
            |**Protected URL**|Enter the specific **URL** to inspect \(for example, "/ABC", "/login/ABC". "/" indicates all paths\) and select the **Matching** method:            -   **Exact Match**: Hit when the requested URL exactly matches the specified URL.
            -   **Prefix Match**: Hit when the requested URL's prefix matches the specified URL.
            -   **RegExp Match**: Hit when the requested URL meets the regular expression of the specified URL.
**Note:** Click **Add Protected URL** to add up to 10 URLs.

|
            |**Disposal method**|Specify the action to perform when the rule is triggered.            -   **Monitor**: Allow and record the request.
            -   **Block**: Block the request.
            -   **JavaScript Validation**: Verify the request data through JavaScript and allow the request after the verification is passed.
            -   **Slider Captcha**: Start a slider verification page on the client and allow the request after the verification is completed.

**Note:** Slider Captcha is applicable to synchronous requests. For asynchronous requests \(such as Ajax\) protection, contact Alibaba Cloud security team. If you are not sure whether the interface you want to protect can use slider verification, we recommend that you use a test IP and URL to perform a test with the Access Control List rule.

|

            **Examples of custom threat intelligence rules**

            -   Rule description: Use this rule to protect the URLs starting with "/login.do" under the current domain name. When the request source IP address matches the Credential Stuffing IP Blacklist, require the client to complete slider verification.

                Rule configuration:

                ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/123806/156569185838739_en-US.jpg)

            -   Rule description: Use this rule to protect the URLs starting with "/houselist" under the current domain name. When the request source IP address matches the Malicious Crawler IP Blacklist \(High\), perform JavaScript verification on the request.

                Rule configuration:

                ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/123806/156569185838740_en-US.jpg)

        5.  \(Optional\) Click**OK** to finish the configuration.

