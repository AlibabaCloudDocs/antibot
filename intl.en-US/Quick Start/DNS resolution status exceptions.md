# DNS resolution status exceptions {#concept_z5t_mpd_n2b .concept}

After you complete the Anti-Bot access configuration for your website domain, you can view the Anti-Bot access status \(DNS Resolution Status\) of the website domain on the Domain Configuration page in the [Anti-Bot Service console](https://yundun.console.aliyun.com/?p=antibot).

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16059/7296_en-US.png)

If the DNS resolution status of the website domain name is abnormal, then the website domain may not be properly accessed to Anti-Bot. Please check the domain access configuration.

If you confirm that the website domain is resolved to the CNAME record assigned by the Anti-Bot instance and the website can be visited properly, please consult Alibaba Cloud Technical Support team.

## Description of DNS resolution status detection criteria {#section_slh_nz2_n2b .section}

Anti-Bot determines the DNS resolution status of the accessed domain according to the following conditions:

**Note:** The DNS resolution status is displayed as normal if one of the conditions is met. 

-   **Condition 1**: The accessed domain is resolved to the Anti-Bot instance through the CNAME record.
-   **Condition 2**: The accessed domain has a certain amount of traffic passing through the Anti-Bot instance. At least 10 requests within five seconds are considered to have a certain amount of traffic. If there are only two or three requests per minute, it is still considered as no traffic due to low traffic.

    **Note:** You can view the history traffic information for the website domain in the **Report** \> **Risk Monitoring** report.


## Description of common DNS resolution status exceptions {#section_gck_r1f_n2b .section}

-   **Access Anti-Bot by using an exact domain name \(domain name  does not contain "\*", for example, `3.test.com`\)**

    If the CNAME record is not used for the website domain to  access Anti-Bot and no certain traffic passes through the Anti-Bot instance, the DNS resolution status displays the following exception:

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16059/7297_en-US.png)

-   **Access Anti-Bot by using a wildcard domain name \(for example, `* .test.com`\)**

    In this situation, if the DNS resolution status is abnormal, only the following exception description is  displayed:

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16059/7298_en-US.png)

-   **CDN or other layer 7 proxies deployed before Anti-Bot**

    Assume that the access deployment mode is CDN-\>Anti-Bot. As the website domain is resolved to CDN, no CNAME access can be detected in Anti-Bot. Meanwhile, CDN may forward relatively low traffic to Anti-Bot.  Then, the DNS resolution status displays as abnormal as the request volume cannot met the detection criteria. In this situation, the abnormal DNS resolution status does not indicate that the website domain name is not properly connected to Anti-Bot, if you confirm that the domain access configuration is correct and the website domain can be visited properly.


