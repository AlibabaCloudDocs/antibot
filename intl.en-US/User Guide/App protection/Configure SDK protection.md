# Configure SDK protection {#concept_g3x_vmx_tfb .concept}

After the SDK is configured in your app, configure SDK protection in the Anti-Bot console to specify the path and version of the app that you want to protect.

Perform the following steps to integrate the SDK:

1.  Integrate the SDK into the app. For more information, see the [iOS SDK integration guide](intl.en-US/User Guide/App protection/iOS SDK integration guide.md#) and the [Android SDK integration guide](intl.en-US/User Guide/App protection/Android SDK integration guide.md#).
2.  Configure the path of the app to be protected in the Anti-Bot console. For more information, see [Configure path protection](#).
3.  Send a test request by using the SDK-integrated app, and analyze the debugging errors and exceptions based on the response and log until SDK integration is verified to be correct.
4.  Publish the new version of the app integrated with the SDK, and enable protection in the Anti-Bot console. For more information, see [Enable app protection](#).

    **Note:** We recommend that you perform an upgrade when publishing the new app version. Otherwise, the previous app version still contains security threats.


## Configure path protection {#interface .section}

Configure path protection to specify the address that you want to protect, and generate protection rules for the address.

**Procedure**

1.  Log on to the [Anti-Bot console](https://yundun.console.aliyun.com/?p=antibot).
2.  Choose **Protection** \> **App Protection**. Select the domain name that you want to configure.
3.  Click **Add** under **Interface Protection**.
4.  In the Add Path Rule dialog box, configure the following settings.

    **Note:** We recommend that you set full-path protection \(prefix matching "/"\) and set Rule Action to Monitor \(or set to Intercept during domain name testing\). This allows debugging without affecting online services.

    |Configuration item|Description|
    |------------------|-----------|
    |**Rule Name**|\(Required\) The name of the rule.|
    |**Protected path configuration**|     -   **Path**: \(Required\) The path that you want to protect. Use a slash \(/\) to indicate a full path.

**Note:** Signature verification may fail when the body length of a POST request exceeds 8 KB. We recommend that you disable SDK protection for APIs that do not require protection \(such as the APIs used to upload large images\). If you do need to enable SDK protection, contact Alibaba Cloud engineers through DingTalk.

    -   **Matching**: The options**Prefix Match** and **Exact** are supported.

In prefix match mode, all the APIs in the specified path are matched. In exact match mode, only the specified path is matched.

    -   **Parameter**: This specifies the parameter content to be matched when the protected path contains invariable parameters, to locate APIs more accurately. The parameter content follows the question mark in the requested address.

Example: Assume that the protected URL contains `domain name/? action=login&name=test`. You can set **Path** to "/" and **Matching** to "Prefix Match", and enter "name", "login", "name=test", or "action=login" in **Parameter**.

 |
    |**Protection policy**|     -   **Invalid Signature**: This is selected by default and cannot be cleared. The system checks whether the request signature of the request sent to the specified path is correct. This policy is matched if the signature is incorrect.
    -   **Simulator**: If this is selected, the system checks whether users initiate requests to the specified path by using a simulator. We recommend that you select this option. This policy is matched if a simulator is used.
    -   **Proxy**: If this is selected, the system checks whether users initiate requests to the specified path by using a proxy tool. We recommend that you select this option. This policy is matched if a proxy tool is used.
 |
    |**Rule Action**|The action to be taken for users who hit the protection policy.    -   **Monitor**: The system only records logs, but does not block requests.
    -   **Block**: The system blocks requests and returns Status Code 405.
|

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/62065/155644700934522_en-US.png)

5.  Click **OK** to add the protection rule.

    You can **modify** and **delete** the added rules.


## \(Optional\) Configure version protection {#section_bp4_fyx_dgb .section}

You can configure version protection to intercept requests from non-official apps. You can configure a version protection policy to verify app validity.

**Note:** A version protection policy is required only when you need to verify app validity.

**Procedure**

1.  Log on to the [Anti-Bot console](https://yundun.console.aliyun.com/?p=antibot).
2.  Choose **Protection** \> **App Protection**. Select the domain name that you want to configure.
3.  Select **Allow Specified Version Requests** under **Version Protection**.

    **Note:** To disable version protection, turn off **Allow Specified Version Requests**.

4.  In the Add Version Rule dialog box, configure the following settings.

    |Configuration item|Description|
    |------------------|-----------|
    |**Rule Name**|The name of the rule.|
    |**Valid Version**|     -   **Valid Package Name**: \(Required\) The valid app package name, such as com.aliyundemo.example.
    -   **Package Signature**: For this value, contact the related security technical engineer of Alibaba Cloud.

**Note:** Do not enter the app certificate signature here.

**Note:** Set Package Signature only when you need to verify the corresponding app package signature. In this case, the system only verifies the configured valid app package name.

 Click **Add Valid Version** to add up to five version records. The package names must be different. Currently, the system does not distinguish between iOS and Android. You can enter valid records to match multiple package names.

 |
    |**Invalid version processing**|     -   **Monitor**: The system only records logs, but does not block requests.
    -   **Block**: The system blocks requests and returns Status Code 405.
 |

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/62065/155644700934523_en-US.png)

5.  Click **OK** to add the rule.

    You can **modify** the added rules.


## Enable app protection {#enable .section}

After verifying through debugging that the app is correctly integrated with the SDK and that the new app version is published, you need to enable app protection to put the protection configuration into effect.

1.  Log on to the [Anti-Bot console](https://yundun.console.aliyun.com/?p=antibot).
2.  Choose **Protection** \> **App Protection**. Select the domain name that you want to configure.
3.  Turn on **Enable**.

    **Note:** Do not enable the Block mode for the domain names in the production environment before the SDK is integrated or debugging is completed. Otherwise, valid requests may be intercepted because the SDK is not correctly integrated. You can enable the Monitor mode during access testing to debug SDK integration based on logs.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/62065/155644700934521_en-US.png)


## More information {#section_h5t_myx_dgb .section}

Scan the QR code through DingTalk to join the technical support group. Consult a security expert in the group if you have any technical or urgent problems when using Anti-Bot.

**Note:** Visit the [DingTalk website](https://www.dingtalk.com), and download and install DingTalk.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/62065/155644700934524_en-US.png)

