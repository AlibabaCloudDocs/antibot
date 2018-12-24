# 步骤2：配置放行Anti-Bot回源IP段 {#concept_hmc_hts_l2b .concept}

您的网站域名成功接入Anti-Bot防护后，访问您网站的所有请求将先流转到Anti-Bot实例，经Anti-Bot实例过滤恶意Bot流量后再返回到源站服务器。其中，流量经Anti-Bot实例返回源站的操作称为回源。

由于Anti-Bot实例的IP数量有限，源站服务器收到的所有请求都将来自这些IP，在源站服务器上的安全软件（如安全狗、云锁）看来，这种情况是很可疑的，且可能会屏蔽Anti-Bot实例的回源IP。因此，在接入Anti-Bot防护后，您需要在源站服务器的其它防火墙、安全软件上设置放行所有Anti-Bot回源IP。

## 操作步骤 {#section_ibd_kts_l2b .section}

防爬风险管理控制台提供了最新的回源IP段列表，您可以参照以下步骤进行操作：

1.  在您将域名信息添加至Anti-Bot实例时，您会看到Anti-Bot实例的回源IP端。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15736/7139_zh-CN.png)

2.  在源站服务器的防火墙、安全软件上，将步骤1中的IP段添加到白名单中。

## 常见问题 {#section_vzn_vts_l2b .section}

**什么是回源IP？**

回源IP是Anti-Bot用来代理客户端请求服务器时用的源IP，在服务器看来，接入Anti-Bot防护后所有源IP都会变成Anti-Bot实例的回源IP，而真实的客户端地址会被加在HTTP头部的XFF字段中。

在接入Anti-Bot实例后，您应确保源站已将Anti-Bot的全部回源IP放行（加入白名单），不然可能会出现网站打不开或打开极其缓慢等情况。

**为何要放行回源IP段？**

接入Anti-Bot实例后，Anti-Bot作为一个反向代理存在于客户端和服务器之间，服务器的真实IP被隐藏起来，客户端只能看到Anti-Bot实例，而看不到源站服务器。

因此，在源站（真实服务器）看来，所有的请求源IP都会变成Anti-Bot实例的回源IP段。

由于来源的IP变得更加集中，频率会变得更快，源站服务器上的防火墙或安全软件很容易认为这些IP在发起攻击，从而限制来自这些IP的访问。一旦Anti-Bot实例的回源IP被封禁，由Anti-Bot实例转发的请求将无法得到源站的正常响应，故务必确保Anti-Bot的回源IP在源站上不会被拦截。

