# Step 3: Verify forwarding configuration in local environment {#concept_um4_k5s_l2b .concept}

Before you switch all business traffic to the Anti-Bot instance, we recommend that you verify that the domain configuration works properly and the Anti-Bot instance forwards requests as expected. The local environment verification process requires to locally simulate access to the Anti-Bot instance. Then, visit the protected website to verify that the Anti-Bot instance forwards the requests properly.

## Locally simulate access to Anti-Bot {#section_hfv_n5s_l2b .section}

Simulate access to the Anti-Bot instance by modifying the hosts file \([What is the hosts file](http://baike.baidu.com/link?url=xM2xPdn2qHt8n_kNP1aAGnCisAMq1y54ewyeGVH7x5lqmZG05Zw2Tr63IiWNs8VAOp-QCRwd9ZWx4wZSiB6QW_KU1GvUr7ojjuXXa3SXYGdfvQhZuB73nzM9zxe6keoSdbOe04Eh1hn2KCNC1lcIo4QyyT7efhbUwpKTe_oh2OW)\) in local environment. Then,  requests to the protected site from the local environment are resolved to the Anti-Bot instance. For example, follow these steps to modify the hosts file in a local Windows operating system based client:

1.  Open the hosts file by using a text editor tool, such as NotePad or Notepad ++. The hosts file is typically located in the `C:\Windows\System32\drivers\etc\` file folder.
2.  Add the following text on the last line in the hosts file: `[IP of the Anti-Bot instance] [Protected domain name]`.

    For example, modify the hosts file for the `www.aliyundemo.cn` domain. Assume that this domain has been configured in the Anti-Bot instance as [Step 1: add domain configuration](intl.en-US/Quick Start/Step 1: Add a domain.md#), and the following CNAME record is assigned for the domain: `xxxxxxxxxxxxxxx.alicloudwaf.com`

    1.  Run the `ping xxxxxxxxxxxxxxx.alicloudwaf.com` command in Command Prompt in your local Windows client to obtain the assigned IP of the Anti-Bot instance. Then, you can get the IP of the Anti-Bot instance that protects your website domain from the response result.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15737/7140_en-US.png)

    2.  Add the following line in the hosts file. In the line, the previous IP address is the IP of the Anti-Bot instance that obtained in the previous step, and the domain name that follows is the website domain name that is protected.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15737/7141_en-US.png)

3.  Save the hosts file. Then, ping the protected website domain locally.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15737/7142_en-US.png)

    Now, the website domain is resolved to the IP address of the Anti-Bot instance that you just added in the hosts file. If it still resolves to the IP address of the origin server, refresh your local DNS cache by running the `ipconfig /flushdns` command in Command Prompt in the Windows client.


## Verify that Anti-Bot forwards requests properly {#section_n1k_lws_l2b .section}

After you confirm that the modification in the hosts file works \(the website domain is resolved to the IP of the Anti-Bot instance locally\), open a web browser and visit the website domain. If the website can be visited as expected, the domain configuration for the website domain in Anti-Bot is correct.

After the above verification process is passed, see [Step 4: Modify the DNS resolution](intl.en-US/Quick Start/Step 4: Modify DNS resolution.md#) to switch business traffic to Anti-Bot.

