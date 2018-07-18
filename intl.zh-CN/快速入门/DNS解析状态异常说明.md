# DNS解析状态异常说明 {#concept_z5t_mpd_n2b .concept}

当网站域名接入Anti-Bot后，您可以在[爬虫风险管理控制台](https://yundun.console.aliyun.com/?p=antibot)的域名接入页面查看网站域名的接入状态，即DNS解析状态。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16059/7296_zh-CN.png)

如果域名的DNS解析状态显示异常，则该网站域名可能没有正确接入Anti-Bot，请检查域名接入配置是否正确。

如果您确认已将该网站域名解析到Anti-Bot实例分配的CNAME记录，并且网站可以正常访问，请咨询阿里云技术支持团队。

## DNS解析状态判定条件说明 {#section_slh_nz2_n2b .section}

Anti-Bot根据以下条件判定已接入域名的DNS解析状态：

**说明：** 满足其中一个条件即判定为DNS解析状态正常，已接入Anti-Bot防护。

-   **条件1**：接入的域名已通过CNAME记录解析至Anti-Bot实例。
-   **条件2**：接入的域名已有一定流量经过Anti-Bot实例。其中，在五秒内至少有大于10个请求才判定为有一定流量。如果每分钟只有两、三个请求，由于流量过低仍将判定为无流量。

    **说明：** 您可以在**数据报表** \> **风险监控**报表中查看网站域名的历史流量信息。


## 常见DNS解析状态异常说明 {#section_gck_r1f_n2b .section}

-   **使用精确域名（即不包含“\*”的域名，例如`3.test.com`）接入Anti-Bot**

    如果即没有通过CNAME记录解析至Anti-Bot，又没有一定流量经过Anti-Bot实例，则DNS解析状态显示以下异常说明：

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16059/7297_zh-CN.png)

-   **使用泛域名（例如`*.test.com`）接入Anti-Bot**

    如果DNS解析状态异常，仅可能显示以下异常说明：

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16059/7298_zh-CN.png)

-   **Anti-Bot前部署其它七层代理（例如CDN）**

    假设部署的接入方式为CDN-\>Anti-Bot，网站域名将被解析至CDN，因此Anti-Bot不会检测到CNAME接入。同时，CDN转发至Anti-Bot的流量比较低，可能出现由于请求量太小无法达到DNS解析状态检测条件，导致DNS解析状态显示为异常。在这种场景中，DNS解析状态异常不一定表明域名未正确接入Anti-Bot，只要您确认域名接入配置正确且网站能正常访问即可。


