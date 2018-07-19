# Step 2: Whitelist Anti-Bot Service IPs {#concept_hmc_hts_l2b .concept}

After you complete the domain configuration process for your website in Anti-Bot, all website requests pass through the Anti-Bot instance to filter malicious bot traffic, and then clean requests are forwarded back to the origin server. In this workflow, the traffic being forwarded back to the origin server by the Anti-Bot instance is called the back to origin operation.

Since one Anti-Bot instance has limited numbers of IPs, all requests received by the origin server come from these IPs. From the aspect of some security software deployed on the origin server, this behavior is suspicious, and the security software may block the Anti-Bot instance's IPs. Therefore, after protecting your website by Anti-Bot, whitelist all Anti-Bot Service IPs in other firewall and security software deployed on the origin server.

## Procedure {#section_ibd_kts_l2b .section}

To obtain the latest Anti-Bot Service IPs in the Anti-Bot Service console, follow these steps:

1.  When you add domain configuration in your Anti-Bot instance, you can obtain the Anti-Bot Service IPs.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15736/7139_en-US.png)

2.  In the firewall and security software that deployed on the origin server, whitelist the Anti-Bot Service IPs that obtained in Step 1.

## FAQs {#section_vzn_vts_l2b .section}

**What is the Anti-Bot Service IP?**

Anti-Bot uses the Anti-Bot Service IP to request website server as a proxy. From the aspect of the origin server, all requests are sent by the Anti-Bot Service IP after you enable the Anti-Bot protection for the website, and the real client IPs are added into the X-Forwarded-For \(XFF\) HTTP header field.

After you complete the domain configuration for a website in Anti-Bot, make sure that all requests from the Anti-Bot Service IPs are allowed by the origin server through whitelisting these IPs. Otherwise, the website may not be visited properly.

**Why whitelist the Anti-Bot Service IPs?**

After enabling the Anti-Bot protection for a website, the Anti-Bot instance can be treated as a reverse proxy between clients and the website server. Then, the real IP of the website server is hidden, and the clients can only access the Anti-Bot instance, instead of the origin server.

Therefore, from the aspect of the website server, all requests are sent by the Anti-Bot Service IPs.

Then, the source IPs of the requests gets concentrated, and the frequency of the requests from several IPs gets faster. In this situation, firewall or security software deployed on the website server may treat these IPs as malicious IPs that are launching attacks, and then restrict access from these IPs. Once the Anti-Bot Service IPs are blocked, requests forwarded by the Anti-Bot instance cannot get a normal response from the origin server. Therefore, make sure that requests sent by the Anti-Bot Service IPs are not blocked on the origin server.

