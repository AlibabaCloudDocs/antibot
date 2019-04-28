# Access control list {#task_umw_rft_l2c .task}

Through access control list \(ACL\) policies, you can configure custom access control rules based on your service scenarios. Combine common HTTP fields \(such as IP, URL, Referer, UA, and other parameters\) to formulate filter conditions, filter the access requests initiated to the website domain name, and set Monitor, Block, Slider Captcha, or Allow for the access requests that match the filter conditions.

**Rule description**

An ACL rule consists of **Rule Condition** and **Rule Action**. When creating a rule, define a filter condition by setting Filter Field, Operator, and Filter Pattern, and define Rule Action for the access requests that match the filter condition.

-   **Rule Condition** 

    Rule Condition consists of Filter Field, Operator, and Filter Pattern.

    |Filter Field|Field description|Applicable operator|
    |------------|-----------------|-------------------|
    |URL|The URL in the access request.|     -   Is Part Of
    -   Does Not Contain
    -   Equals
    -   Does Not Equal
 |
    |IP|The source IP address of the access request.|     -   Belongs To
    -   Does Not Belong To
 |
    |Referer|The source URL of the access request, that is, the page from which the access request is redirected.|     -   Is Part Of
    -   Does Not Contain
    -   Equals
    -   Does Not Equal
    -   Is Shorter Than
    -   Has a Length Of
    -   Is Longer Than
    -   Is Not Part Of
 |
    |User-Agent|The web browser information about the client initiating the access request, including the web browser identifier, rendering engine identifier, and version.|     -   Is Part Of
    -   Does Not Contain
    -   Equals
    -   Does Not Equal
    -   Is Shorter Than
    -   Has a Length Of
    -   Is Longer Than
 |
    |Params|The parameter part of the URL in the access request, which is typically the part following the question mark \(?\) in the URL. For example, in `www.abc.com/index.html? action=login`, `action=login` is the parameter part.|     -   Is Part Of
    -   Does Not Contain
    -   Equals
    -   Does Not Equal
    -   Is Shorter Than
    -   Has a Length Of
    -   Is Longer Than
 |
    |Cookie|The cookie information in the access request.|     -   Is Part Of
    -   Does Not Contain
    -   Equals
    -   Does Not Equal
    -   Is Shorter Than
    -   Has a Length Of
    -   Is Longer Than
    -   Is Not Part Of
 |
    |Content-Type|The HTTP content type of the response specified by the access request, that is, MIME type information.|     -   Is Part Of
    -   Does Not Contain
    -   Equals
    -   Does Not Equal
    -   Is Shorter Than
    -   Has a Length Of
    -   Is Longer Than
 |
    |Content-Length|The number of bytes in the response to the access request.|     -   Is Smaller Than
    -   Has a Value Of
    -   Is Larger Than
 |
    |X-Forwarded-For|The actual client IP address in the access request. **Note:** X-Forwarded-For \(XFF\) is used to identify the HTTP request header field of the initial IP address of the client initiating the access request that is forwarded through HTTP proxy or load balancing. XFF is only included in the access requests that are forwarded by the HTTP proxy or SLB.

 |     -   Is Part Of
    -   Does Not Contain
    -   Equals
    -   Does Not Equal
    -   Is Shorter Than
    -   Has a Length Of
    -   Is Longer Than
    -   Is Not Part Of
 |
    |Post-Body|The content of the response to the access request.|     -   Is Part Of
    -   Does Not Contain
    -   Equals
    -   Does Not Equal
 |
    |Http-Method|The method of the access request, such as GET and POST.|     -   Equals
    -   Does Not Equal
 |
    |Header|The header of the access request, which is used to customize the HTTP header field.|     -   Is Part Of
    -   Does Not Contain
    -   Equals
    -   Does Not Equal
    -   Is Shorter Than
    -   Has a Length Of
    -   Is Longer Than
    -   Is Not Part Of
 |

-   **Rule Action** 

    An ACL rule supports the following rule actions:

    -   **Block**: blocks the access requests that match the filter condition.
    -   **Allow**: allows the access requests that match the filter condition.
    -   **Monitor**: allows the access requests that match the filter condition. Meanwhile, you can view the requests that match the filter rule in a data report to check the effect of the access control list rule.
    -   **Slider Captcha**: sends a slide-to-verify request to the client whose access request matches the filter condition to perform secondary bot recognition. The access user must drag the slider to complete verification in order to continue service operation. Service operation will be terminated when the verification fails \(the access user does not drag the slider or the operation is not human-initiated\).
-   **Rule matching order** 

    If you configure multiple ACL rules, the rules are matched in order. That is, access requests are matched with rules in the specified order. Rules on top are matched first. When an access request matches the filter condition of a rule, the request is processed based on the action specified by the rule, and matching stops.

    You can sort all the ACL rules by using the rule sorting function to obtain optimal protection.


**Default rule description**

An ACL contains a default rule.

-   **Rule Condition**: All the requests that do not match the preceding rules. After the ACL policy is enabled, all the access requests that do not match the configured ACL rules are processed based on the action specified by the default rule.
-   **Rule Action**: The default action is that the system allows all the access requests that do not match the configured ACL rules and continues to execute other protection policies \(rate limiting and app protection\).

**Note:** The default rule cannot be deleted, and its filter condition cannot be modified. The default rule is always the last to be matched, and its order cannot be changed.

1.  Log on to the [Anti-Bot console](https://yundun.console.aliyun.com/?p=antibot), and select the region where your Anti-Bot instance is located.
2.  Choose **Protection** \> **Access Control List**. Select the protected domain name.
3.  Turn on **Enable**![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15835/155644685835020_en-US.png) to enable the ACL policy.
4.  Click **Add**. Set the filter condition and action of the rule. Then, click **OK**. 

    **Note:** When you select Header as the filter field, you need to set the Key field of the customer header. For example, if the service-indicating field in the Header field is `userid=xxxxxx`, enter `userid` in the custom Header field to use the userid field as the filter condition.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15835/15564468587163_en-US.png)

    When the rule is added, you can **modify** or **delete** it. If multiple rules are added, you can go to the Access Control List page and click **Sort**. Then, click **Move Up**, **Move Down**, **Stick to Top**, or **Stick to Bottom** to adjust the rule matching order. The rules on top are matched first. After adjusting the rule matching order, click **Save Order** to make the order effective.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15835/15564468587164_en-US.png)


