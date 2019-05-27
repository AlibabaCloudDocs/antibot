# Overview {#task_m2q_52t_l2b .task}

After you add a domain and set up DNS settings, you can configure custom protection policies to protect the domain from malicious bot traffic.

1.  Log on to the [Anti-Bot Service console](https://yundun.console.aliyun.com/?p=antibot) and select the region where your Anti-Bot instance is located. 
2.  Choose **Protection** \> **Overview** and select the domain that you want to change settings for. 

    **Note:** You can also choose Domain Configuration, select the domain in the domain list, and click **Policies** to open the Overview page.

3.  Select a protection policy and click **Configure** to change configurations. 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15823/15589614747159_en-US.png)

    -   **Black and Whitelist**: You can allow or block bot traffic from specific IP addresses. For more information, see [Blacklist and whitelist](intl.en-US/User Guide/Protection Settings/Blacklist and whitelist.md#).
    -   **Access Control List**: You can create custom protection policies based on common HTTP request fields, such as IP address, URLs, references, UA, and parameters to meet business needs. For more information, see [Access control list](intl.en-US/User Guide/Protection Settings/Access control list.md#).
    -   **Rate Limiting**: You can limit the number of requests to specific URLs based on the IP address, cookie, or header fields of the request. You can also set limits based on response codes. For more information, see [Rate limiting](intl.en-US/User Guide/Protection Settings/Rate limiting.md#).
    -   **App Protection**: Provides secure connectivity and anti-bot protection for native apps. This feature can accurately identify requests from proxy servers, emulators, and requests with invalid signatures. To enable App Protection, you must integrate the Anti-Bot SDK with your app. For more information, see [App Protection](../../../../intl.en-US/User Guide/App protection/Solution overview.md#).
    -   **Allowed Crawlers**: Provides a whitelist of crawlers used by mainstream search engines, such as Google, Bing, Baidu, Sogou, 360, and Yandex. You can allow these search engine crawlers to access the entire site or specific directories. For more information, see [Bot intelligence](intl.en-US/User Guide/Protection Settings/Bot intelligence.md#).
    -   **Threat Intelligence**: Provides information about suspicious IP addresses used by harassing phone calls, data centers, and malicious scanners based on Alibaba Cloud's powerful computing capability. This feature also maintains an IP library of malicious crawlers and can prevent crawlers from accessing your site or specific directories in real time. For more information, see [Bot intelligence](intl.en-US/User Guide/Protection Settings/Bot intelligence.md#).

