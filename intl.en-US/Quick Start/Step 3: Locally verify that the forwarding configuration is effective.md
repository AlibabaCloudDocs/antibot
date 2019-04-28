# Step 3: Locally verify that the forwarding configuration is effective {#concept_um4_k5s_l2b .concept}

We recommend that you locally verify that both the configuration and Anti-Bot forwarding are normal before switching service traffic to the Anti-Bot instance. During local verification, simulate Anti-Bot configuration locally, and access the protected website to verify that the Anti-Bot instance forwards access requests properly.

## Access Anti-Bot locally {#section_hfv_n5s_l2b .section}

Simulate Anti-Bot configuration by modifying the local hosts file \(see [What is the hosts file](http://baike.baidu.com/link?url=xM2xPdn2qHt8n_kNP1aAGnCisAMq1y54ewyeGVH7x5lqmZG05Zw2Tr63IiWNs8VAOp-QCRwd9ZWx4wZSiB6QW_KU1GvUr7ojjuXXa3SXYGdfvQhZuB73nzM9zxe6keoSdbOe04Eh1hn2KCNC1lcIo4QyyT7efhbUwpKTe_oh2OW)\) to locally access the Anti-Bot instance that forwards the requests sent to the protected website. Here, the Windows operating system is used as an example.

1.  Open the hosts file by using Notepad or Notepad++. The hosts file is typically located in the `C:\Windows\System32\drivers\etc\hosts` path.
2.  Append the `protected domain name corresponding to the IP address of the Anti-Bot instance` to the end of the hosts file.

    Here, the domain name `www.aliyundemo.cn` is used as an example. This domain name was added to the Anti-Bot instance during [Step 1: Add a domain name](intl.en-US/Quick Start/Step 1: Add a domain name.md#), and Anti-Bot allocated the domain name with the CNAME value `xxxxxxxxxxxxxxx.alicloudwaf.com`.

    1.  Open the Windows command-line interface \(CLI\), and run `ping xxxxxxxxxxxxxxx.alicloudwaf.com` to retrieve the IP address of the Anti-Bot instance. As shown in the following figure, the response contains the IP address of the Anti-Bot instance that protects your domain name.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15737/15564489757140_en-US.png)

    2.  Append the following content to the end of the hosts file. The IP address indicates the IP address of the Anti-Bot instance retrieved in the preceding step, while the domain name indicates the protected domain name.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15737/15564489777141_en-US.png)

3.  Save the updated hosts file. Then, run `ping` on the protected domain name.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15737/15564489777142_en-US.png)

    For the running result, the resolved IP address is expected to be the bound IP address of the Anti-Bot instance. If the resolved IP address remains that of the origin server, refresh the local DNS cache \(by running `ipconfig /flushdns` on the Windows CLI\) and try again.


## Verify that Anti-Bot forwards access requests properly {#section_n1k_lws_l2b .section}

Enter the domain name in the address bar of the web browser after verifying that the hosts file binding is effective \(namely, the domain name can be locally resolved to the IP address of the Anti-Bot instance\). If Anti-Bot is correctly configured for the domain name, the website can be properly accessed.

If the preceding verification succeeds, switch service traffic to Anti-Bot based on [Step 4: Modify DNS resolution](intl.en-US/Quick Start/Step 4: Modify DNS resolution.md#).

