# DNS resolution status exceptions {#concept_z5t_mpd_n2b .concept}

After configuring Anti-Bot for your website domain name, you can check the access status of the domain name \(namely, the DNS resolution status\) on the Domain Names page of the [Anti-Bot console](https://yundun.console.aliyun.com/?p=antibot).

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16059/15564440117296_en-US.png)

If the DNS resolution status of the website domain name is abnormal, the website domain name may not have been properly configured with Anti-Bot. In this case, check the domain access configuration.

If the website domain name has resolved to the CNAME record assigned by the Anti-Bot instance and the website can be properly visited, contact the Alibaba Cloud Customer Services.

## DNS resolution status detection criteria {#section_slh_nz2_n2b .section}

Anti-Bot determines the DNS resolution status of the accessed domain name according to the following conditions:

**Note:** The DNS resolution status is normal if one of the following conditions is met.

-   **Condition 1**: The accessed domain name has resolved to the Anti-Bot instance via the CNAME record.
-   **Condition 2**: The accessed domain name has a certain amount of traffic passing through the Anti-Bot instance. A certain amount of traffic passing means there are at least 10 requests within 5 seconds. If only two or three requests occur per minute, this is considered as no traffic due to the low request quantity.

    **Note:** Choose **Reports** \> **Risk Monitoring** to check the traffic history of the website domain name in a report.


## Common DNS resolution status exceptions {#section_gck_r1f_n2b .section}

-   **Access Anti-Bot by using an exact domain name \(a domain name that does not contain the wildcard "\*", for example, `3.test.com`\)** 

    If the CNAME record is not used for configuring Anti-Bot for the website domain name and no traffic passes through the Anti-Bot instance, the DNS resolution status displays the following exception:

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16059/15564440127297_en-US.png)

-   **Access Anti-Bot by using a wildcard domain name \(for example, `* .test.com`\)** 

    In this case, if the DNS resolution status is abnormal, only the following exception appears:

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16059/15564440127298_en-US.png)

-   **Layer-7 gateways are in use, such as Alibaba Cloud CDN** 

    Assume that the Anti-Bot deployment mode is CDN -\> Anti-Bot. No CNAME access can be detected in Anti-Bot because the website domain name is resolved to CDN. Meanwhile, CDN may forward a relatively low traffic to Anti-Bot, and the DNS resolution status is displayed as abnormal because the request volume does not meet the detection criteria. In this case, if you confirm that the domain access configuration is correct and the website can be properly visited, the abnormal DNS resolution status does not necessarily indicate that Anti-Bot was improperly configured for the website domain name.


