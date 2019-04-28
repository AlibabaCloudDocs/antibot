# Blacklist and whitelist {#task_umw_rft_l2b .task}

You can set an IP address blacklist and whitelist for the specified domain name to directly allow or block the bot traffic from the IP addresses in the blacklist or whitelist.

Blacklist and whitelist policies take precedence over other protection policies. That is, requests from the IP addresses in the blacklist or whitelist are directly blocked or allowed. The whitelist policy takes precedence over the blacklist policy. That is, if an IP address is added in both the blacklist and whitelist, the whitelist policy for the IP address takes effect, allowing requests from the IP address.

1.  Log on to the [Anti-Bot console](https://yundun.console.aliyun.com/?p=antibot), and select the region where your Anti-Bot instance is located. 
2.  Choose **Protection** \> **Blacklist and Whitelist**. Select the protected domain name. 
3.  Turn on **Enable**![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15835/155644636535020_en-US.png) to enable the blacklist and whitelist policies. 
4.  In the **IP Blacklist** or **IP Whitelist** field, enter the IP address or CIDR block to be directly allowed or blocked, and click **Save**. 

    **Note:** You can enter IP addresses or a CIDR block \(IP address/mask\). Separate multiple IP addresses with commas \(,\).

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15831/15564463667160_en-US.png)

    The IP address blacklist or whitelist takes effect once it is saved.


