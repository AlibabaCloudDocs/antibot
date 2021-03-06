# App端安全SDK方案概述 {#concept_uz3_hvj_n2b .concept}

Anti-Bot针对原生App端提供安全SDK解决方案。为您的App提供可信通信、防机器脚本滥刷等安全防护，有效识别高风险手机、猫池、牧场等特征。

App端安全SDK方案集成了阿里巴巴集团多年来对抗黑灰产、羊毛党的经验和技术积累。将您的App集成Anti-Bot安全SDK后，您的App将获得与天猫、淘宝、支付宝等App端相同的可信通信技术能力，并可共享阿里巴巴集团多年对抗黑灰产、羊毛党所积累的恶意设备指纹库，从根本上帮助您解决App端的安全问题。

Anti-Bot提供的App端安全SDK方案帮助您解决以下**原生App端**的安全问题：

-   恶意注册、撞库、暴力破解
-   针对App的大流量CC攻击
-   短信/验证码接口被刷
-   薅羊毛、抢红包
-   恶意秒杀限时限购商品
-   恶意查票、刷票（例如，机票、酒店等场景）
-   价值资讯爬取（例如，价格、征信、融资、小说等内容）
-   机器批量投票
-   灌水、恶意评论

## 配置App端安全SDK方案 {#section_cfr_glm_n2b .section}

参考以下操作步骤，为您的App配置安全SDK解决方案：

**说明：** 配置App端安全SDK方案，您无需在服务器端进行任何改动。配置完成后，Anti-Bot将自动过滤恶意请求，将合法的请求转发给源站服务器。恶意请求产生的压力将全部由Anti-Bot承担，保障您的服务器端稳定运行。

1.  登录[爬虫风险管理控制台](https://yundun.console.aliyun.com/?p=antibot)，选择您的Anti-Bot实例所在的地区。
2.  定位到域名接入页面，单击**添加域名**，为您App端使用的域名添加域名接入配置。具体操作步骤，参考[添加域名配置](cn.zh-CN/快速入门/步骤1：添加域名.md#)。
3.  在您App使用的域名的DNS解析服务提供商处，添加Anti-Bot实例分配的CNAME记录，将App的域名解析指向Anti-Bot实例。具体操作步骤，参考[修改DNS解析](cn.zh-CN/快速入门/步骤4：修改DNS解析.md#)。
4.  在您的App中集成Anti-Bot提供的[SDK组件](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/62847/cn_zh/1527666392401/WAF-SDK-20180525.zip?spm=a2c4g.11186623.2.7.mnuGFz&file=WAF-SDK-20180525.zip)。

    **说明：** 集成SDK操作一般需要1-2天时间。

    关于集成SDK的详细操作说明，参考：

    -   [iOS SDK集成指南](cn.zh-CN/快速入门/集成App端Anti-Bot SDK/iOS SDK集成指南.md#)
    -   [Android SDK集成指南](cn.zh-CN/快速入门/集成App端Anti-Bot SDK/Android SDK集成指南.md#)
5.  使用钉钉扫描下方二维码，联系Anti-Bot技术支持人员帮您测试已集成SDK的App。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16083/7327_zh-CN.png)

    **说明：** 如果您对SDK解决方案配置有任何疑问，都可以使用钉钉扫描该二维码联系阿里云Anti-Bot技术支持人员（申请时请注明SDK方案咨询）。

6.  测试通过后，打包并发布已集成SDK的新App版本，即可享受App端安全SDK解决方案为您提供的安全防护。

