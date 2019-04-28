# Deploy both Anti-Bot and Anti-DDoS Pro {#task_tpk_dfj_p2b .task}

Anti-Bot Service \(Anti-Bot\) is fully compatible with Anti-DDoS Pro. You can deploy both Anti-Bot and Anti-DDoS Pro for your origin server in this schema: Anti-DDoS Pro \(ingress to DDoS protection\) \> Anti-Bot \(intermediate layer for application-layer protection\) \> origin server.

1.  Add website configuration in the Anti-Bot console. 

    -   **Server Address**: Select **IP** and enter the public IP address of an SLB instance, the public IP address of an ECS instance, or the IP address of a server in an IDC.
    -   **Layer-7 gateways are in use, such as Alibaba Cloud Anti-DDoS Pro or CDN**: Select **Yes**.
    For more information, see [Add domain name configuration](../intl.en-US/Quick Start/Step 1: Add a domain.md#).

2.  Add website configuration in the Anti-DDoS Pro console. Procedure: 
    1.  Select **Access** \> **Website**. Click **Add Domain**.
    2.  In the Specify Domain Information task, configure the following settings:

        -   **Domain**: Enter the domain name of the website you want to protect.
        -   **Protocol**: Select the protocol supported by the origin server.
        -   **Origin Site IP/Domain**: Select **Origin Site Domain**, and enter the CNAME address generated by Anti-Bot.

            **Note:** For how to check the CNAME address generated by Anti-Bot, see [Check the CNAME address allocated by Anti-Bot](../intl.en-US/Quick Start/Step 1: Add a domain.md#section_uvb_gnv_fgb).

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15557/155644627133576_en-US.png)

    3.  Click **Next**.
    4.  Select an **instance** for the task.
3.  Modify the DNS resolution of the domain name. Log on to the DNS system. Add a CNAME record to direct the resolved address of the website domain name to the CNAME address generated by Anti-DDoS Pro. 

    For more information, see [Configure a CNAME in Anti-DDoS Pro](https://www.alibabacloud.com/help/doc-detail/40532.htm).


After the preceding configuration, website traffic passes through Anti-DDoS Pro and then is forwarded to Anti-Bot for protection.
