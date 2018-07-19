# Step 1: Add a domain {#concept_gt2_q4s_l2b .concept}

After purchasing Alibaba Cloud Anti-Bot Service, complete domain configuration for your website to realize malicious bot traffic protection.

**Note:** Since Anti-Bot uses the same forwarding configuration as the Web Application Firewall \(WAF\), you do not need to add domain configurations for a website domain that has been configured in WAF again if you have purchased Alibaba Cloud Security WAF. The website domains that have been configured in the WAF console are synchronized automatically to the Anti-Bot Service console, and the sources of the domain configuration records are **Auto Synchronized**.

## Prerequisites {#section_p3r_v4s_l2b .section}

Before you configure your website's domain in the Anti-Bot Service console, complete the following preparations:

-   Domain name of the website to be defended against malicious bot traffic.

    **Note:** For Anti-Bot instances in the Mainland China region, all website domains to be configured must have been filed in the Ministry of Industry and Information Technology \(MIIT\) while Alibaba Cloud ICP filing is not required. For Anti-Bot instances in the  International region, there is no filing requirement for website domains.

-   IP address of the origin server for the website domain.

    **Note:** For one website domain, up to 20 origin server IPs are supported to be configured in Anti-Bot.

-   For websites that support the HTTPS protocol, prepare the corresponding certificate and private key information that are bound with the website.
-   Edit permissions for DNS resolution records of the website domain.  This means that you can modify the DNS resolution records for the website domain in the DNS resolution management portal provided by the DNS service provider.

## Procedure {#section_tx4_1ps_l2b .section}

1.  Log on to the [Anti-Bot Service console](https://yundun.console.aliyun.com/?p=antibot), select the region where your Anti-Bot instance belongs to.
2.  Go to the Domain Configuration page, and then click **Add Domain**.
3.  Complete the forwarding configuration for your website domain, and then click **Next**.

    |Parameter|Description|Remark|
    |---------|-----------|------|
    |Domain|The domain name of the website.|Wildcard domain names \(for example, \* .aliyundemo.cn\) are supported, and Anti-Bot automatically matches all second-level domain names of the wildcard domain name.**Note:** If you configure both a wildcard domain name and its exact domain name \(for example,  \*.aliyundemo.cn and abc.aliyundemo.cn\), Anti-Bot gives priority in the use of the forwarding rules and protection policies configured for the exact domain name.

|
    |Protocol|The type of protocols supported by the website. If your website supports HTTPS encrypted authentication, check the HTTPS protocol, and [upload the certificate and private key](#section_hvz_3rs_l2b) after the domain configuration.|If you check the HTTPS protocol, you can enable HTTPS Redirection or SSL Offloading functions by click Advanced Settings, to ensure smooth access.|
    |Origin Address|The address of the origin server for the website domain.|After your website is configured in the Anti-Bot instance for protection, Anti-Bot forwards filtered requests to the origin server address.|
    |\(Recommended\) Select **IP**, and then fill in IP addresses of the origin server \(for example, IP of an ECS instance, IP of an SLB instance, or IP of a local server\). Anti-Bot forwards clean requests to the origin IP after the domain configuration is completed.|You may enter up to 20 origin IP addresses. If multiple origin IPs are configured, Anti-Bot automatically enables the Health Check and Load Balancing features for the website domain.|
    |Select **Other Address**, and then fill in a domain name for origin fetching \(for example, CNAME record of an OSS bucket\). Anti-Bot forwards clean requests to the domain after the domain configuration is completed.|The domain name for origin fetching must not be the same as the website domain name to be protected.|
    |Origin Port|The origin port of the website domain. After your website is configured in the Anti-Bot instance for protection, Anti-Bot forwards filtered requests to the origin port.|By default, the HTTP port is 80 and the HTTPS port is 443. If you want to use a customized port, click **Customize** to add the port.|
    |Is there any layer 7 proxies such as CND and Anti-DDoS Pro before Anti-Bot|Select Yes or No according to your website business deployment.|If the website has other layer 7 proxies deployed to do the forwarding in front of Anti-Bot, select **Yes**. Otherwise, Anti-Bot cannot obtain real client IP information of the website.|
    |Load Balancing Algorithm|If multiple origin IPs are configured, select **IP hash** or **Round-robin**. Anti-Bot distributes access requests by using the selected algorithm to achieve load balancing.|-|

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15735/7135_en-US.png)

4.  Select DNS resolution method \(Manual or CDN\) for the website domain, and then click **Next**, to complete the  domain configuration process.

    **Note:** Before you [change the DNS resolution](intl.en-US/Quick Start/Step 4: Modify DNS resolution.md#) for the website domain, we recommended that you [add the Anti-Bot Service IP segments to the whitelist on the website origin server](intl.en-US/Quick Start/Step 2: Whitelist Anti-Bot Service IPs.md#) and then [verify that the domain forwarding configuration is effective in the local environment](intl.en-US/Quick Start/Step 3: Verify forwarding configuration in local environment.md#), to ensure that all requests to the website are properly forwarded back to the origin server.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15735/7136_en-US.png)


After the website domain configuration process is completed, Anti-Bot automatically assigns a CNAME record to the domain. By resolving website requests to the CNAME record, all requests can pass through the Anti-Bot instance and then be forward to the origin server, to implement security protection.

**Note:** You can obtain the IP that assigned to the website domain by the Anti-Bot instance by Ping the CNAME record.  Generally, the assigned IP of the Anti-Bot instance does not change frequently.

Log on to the [Anti-Bot Service console](https://yundun.console.aliyun.com/?p=antibot), on the Domain Configuration page, hover your mouse over the added website domain and then over the displayed **Copy CNAME** button to view the CNAME record that assigned to the website domain.

**Note:** Click **Copy CNAME** to copy the CNAME record to the clipboard.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15735/7137_en-US.png)

## Upload HTTPS certificate and private key \(for HTTPS websites only\) {#section_hvz_3rs_l2b .section}

If the added website domain supports HTTPS encrypted authentication, and you select the HTTPS protocol during the domain configuration process, upload the corresponding certificate and private key in the [Anti-Bot Service console](https://yundun.console.aliyun.com/?p=antibot) after the domain configuration. Otherwise, the HTTPS protocol cannot work properly for the website.

After your add the domain configuration, the status of the HTTPS protocol is displayed as Abnormal on the Domain Configuration page. This means that the current certificate is configured incorrectly.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15735/7138_en-US.png)

To upload the certificate and private key for the website domain, follow these steps:

1.  Log on to the [Anti-Bot Service console](https://yundun.console.aliyun.com/?p=antibot), go to the Domain Configuration page, and then select a domain. 
2.  Click the Upload Certificate button on the right side of the HTTPS protocol status.
3.  In the Upload Certificate dialog box, select a **Upload Method**.
    -   Select **Manually Upload**, fill in the Certificate Name, copy text contents from the certificate file and the private key file that the website domain is bound with and paste into the **Certificate File** and **Private Key File** text boxes.

        **Note:** For certificates in general formats, such as PEM, CER, and CRT, you can open the certificate file directly by using a text editor tool to copy the text contents. For certificates in other formats, such as PFX and P7B, convert the certificate file to the PEM format, and then copy the text contents from the converted certificate file. For more information about the conversion between different certificate formats, see [How to convert HTTPS certificates to the PEM format](../../../../intl.en-US/FAQ/What formats are used for mainstream digital certificates.md#section_hf5_mbv_ydb).

        **Note:** If the HTTPS certificate has multiple certificate files, such as a certificate chain file, merge the text contents from the multiple certificate files and then paste the contents into the **Certificate File** text box.

        **Certificate file content example**

        ```
        -----BEGIN CERTIFICATE-----
        xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx8ixZJ4krc+1M+j2kcubVpsE2
        CgHdj4v8H6jUz9Ji4mr7vMNS6dXv8PUkl/qoDeNGCNdyTS5NIL5ir + g92cL8IGOkjgvhlqt9vc
        65Cgb4mL+n5+DV9uOyTZTW/MojmlgfUekC2xiXa54nxJf17Y1TADGSbyJbsC0Q9nIrHsPl8YKk
        vRWvIAqYxXZ7wRwWWmv4TMxFhWRiNY7yZIo2ZUhl02SIDNggIEeg==
        -----END CERTIFICATE-----
        ```

        **Private key file content example**

        ```
        -----BEGIN RSA PRIVATE KEY-----
        DADTPZoOHd9WtZ3UKHJTRgNQmioPQn2bqdKHop+B/dn/4VZL7Jt8zSDGM9sTMThLyvsmLQKBgQ
        Cr+ujntC1kN6pGBj2Fw2l/EA/W3rYEce2tyhjgmG7rZ+A/jVE9fld5sQra6ZdwBcQJaiygoIYo
        aMF2EjRwc0qwHaluq0C15f6ujSoHh2e+D5zdmkTg/3NKNjqNv6xA2gYpinVDzFdZ9Zujxvuh9o
        4Vqf0YF8bv5UK5G04RtKadOw==
        -----END RSA PRIVATE KEY-----
        ```

    -   Select **Select Existing Certificates** and choose the certificate directly, if the HTTPS certificate that the website domain is bound with has been managed in the Alibaba Cloud Security SSL Certificate service with the same Alibaba Cloud account.
4.  Click **Confirm**, and the certificate and private key that the domain name is bound with are uploaded. Then, the HTTPS protocol status becomes **Normal**.

