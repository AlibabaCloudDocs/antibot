# 同时部署Anti-Bot和CDN {#concept_ig2_xfj_p2b .concept}

爬虫风险管理（Anti-Bot Service，简称Anti-Bot）可以与CDN（如网宿、加速乐、七牛、又拍、阿里云CDN等）结合使用，为开启内容加速的域名提供恶意爬虫防御功能。您可以参照以下架构为源站同时部署Anti-Bot和CDN：CDN（入口层，内容加速）\> Anti-Bot（中间层，实现应用层爬虫风险管理防护）\> 源站。

## 使用阿里云CDN {#section_qnf_dhj_p2b .section}

以阿里云CDN为例。参照以下步骤，为您的网站同时部署爬虫风险管理和CDN：

1.  参考[CDN快速入门](../../cn.zh-CN/快速入门/快速入门.md#)，将要防护的域名（即加速域名）接入CDN。
2.  在爬虫风险管理控制台中创建网站配置。

    -   **域名**：填写要防护的域名。
    -   **服务器地址**：填写SLB公网IP、ECS公网IP，或云外机房服务器的IP。
    -   **Anti-Bot前是否有七层代理（高防/CDN等）**：勾选**是**。
    具体操作请参考[添加域名配置](../cn.zh-CN/快速入门/步骤1：添加域名.md#)。

3.  成功创建网站配置后，爬虫风险管理为该域名生成一个专用的CNAME地址。

    **说明：** 关于如何查看Anti-Bot生成的CNAME地址，请参考[查看爬虫风险管理分配的CNAME地址](../cn.zh-CN/快速入门/步骤1：添加域名.md#section_uvb_gnv_fgb)。

4.  将CDN配置中的源站修改为爬虫风险管理分配的CNAME地址，操作步骤如下：
    1.  登录[阿里云CDN控制台](https://cdn.console.aliyun.com/#/DomainList/list)。
    2.  在域名管理页面，选择要操作的域名，单击**配置**。
    3.  在**源站设置**下，单击**修改配置**。
    4.  修改源站信息。

        -   **类型**：选择**源站域名**。
        -   **源站地址 域名**：填写Anti-Bot生成的CNAME地址。
        -   **协议跟随回源**：开启。
        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15558/15483264547706_zh-CN.jpg)

    5.  在**回源设置**下，确认**回源host**未开启。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15558/15483264547707_zh-CN.jpg)


完成上述配置后，流量经过CDN，其中动态内容将继续通过爬虫风险管理进行安全检测防护。

## 使用非阿里云CDN {#section_jv2_ghj_p2b .section}

1.  配置CDN，将域名接入CDN。
2.  在爬虫风险管理控制台中创建网站配置。具体请参考[添加域名配置](../cn.zh-CN/快速入门/步骤1：添加域名.md#)。
3.  [查看爬虫风险管理分配的CNAME地址](../cn.zh-CN/快速入门/步骤1：添加域名.md#section_uvb_gnv_fgb)。
4.  将CDN配置的源站改为Anti-Bot所分配的CNAME地址。

