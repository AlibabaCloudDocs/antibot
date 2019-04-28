# Rate limiting {#task_ihz_lmt_l2b .task}

A rate limiting policy is used to limit the rate at which request objects access specified URLs to intercept malicious bot traffic. In addition to rate limiting, you can add other limitations, such as the number or proportion of specific response codes to limit the access requests of request objects.

**Rate limiting rule**

A rate limiting rule consists of the following parameters:

|Parameter|Description|
|---------|-----------|
|Rule Name|The name of the rule. We recommend that you set a name that reflects the meaning of the rule.|
|URL|The URL to which the rule is applied, such as `/login.com`.**Note:** This field cannot be empty.

URL setting supports the following match rules:-   **Full match**: is also referred to as exact match. The rule collects statistics only on those client-requested URLs that are exactly the same as the configured URL, which must start with a `slash (/)`.
-   **Prefix match**: is also referred to as left-include match. The rule collects statistics only on those rules that start with the configured URL prefix. The configured URL must start with a `slash (/)`. For example, if the configured URL is `/login`, then the requested URL `/login.html` is counted by the rule.
-   **Regular match**: Matching is based on a regular expression. Enter a complete regular expression in the URL text box. Then, the rule collects statistics on the client access with requested URLs that are compliant with the regular expression.

**Note:** You can enter a parameter-carrying URL, such as `/user? action=login`.

|
|Request Object|The entity that is counted by the rule. The request object can be an IP address, default cookie, custom header, parameter, or a field in the cookie.**Note:** 

-   The default cookie is the automatically added cookie when a normal user request reaches the engine. It typically starts with `acw_tc`.
-   **Example of statistics based on a custom field**: A service identifies users by using `token: 123456` in the HTTP header. You can configure the custom header or token as a request object for rate statistics.

|
|Duration|The period when the rule counts request times.|
|Requests|The maximum number of request times accumulated by a single request object during the configured statistical period.**Note:** In addition to the request times limit, you can add a **response code** limit condition, such as a maximum of 300 accumulated request times with Response Code 503 and 70% of request times with Response Code 503. The action specified by the rule is triggered only when the counted request times exceed the maximum number and the number or proportion of request times meets the response code limit condition.

|
|Rule Action|The action triggered when the rule condition is met.-   **Monitor**: The system does not trigger any action on the request, but only records the statistical results in the rule-matched data report for the purpose of checking the actual effect of the rule.
-   **Block**: The system disconnects the request object.
-   **JavaScript**: The system sends a verification request message to the client through redirection. The client must pass verification before continuing service operation.
-   **Slider Captcha**: The system sends a slide captcha verification request message to the client for secondary bot recognition. The access user must drag the slider to complete verification in order to continue service operation. Service operation will be terminated when the verification fails \(the access user does not drag the slider or the operation is not human-initiated\).

**Note:** 

-   When Rule Action is set to Block, you can set a block duration \(**blacklisting duration**\) for request objects. For example, if the block duration is set to 30 minutes, all the IP address access requests that meet the condition are blocked within 30 minutes.
-   You can configure Rule Action to take effect for the global requests of the domain name or only the requests that match the rule-specified URL.

|

**Note:** The statistical process may encounter a delay because the data of multiple servers in the cluster must be summarized for statistics. Therefore, the actual effective time of the rate limiting condition may be delayed.

1.  Log on to the [Anti-Bot console](https://yundun.console.aliyun.com/?p=antibot), and select the region where your Anti-Bot instance is located. 
2.  Choose **Protection** \> **Rate Limiting**. Select the domain name of the protected website. 
3.  Turn on **Enable**![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15835/155644687435020_en-US.png) to enable the rate limiting policy. 
4.  Click **Add** to configure a rate limiting rule. Then, click **OK**. For example, you can configure the Block action to be triggered when a single source IP address initiates more than 1,000 access requests to `1.test.com/login.html` within 5 minutes \(300 seconds\) and the proportion of accumulated requests with Response Code 404 exceeds 80%, and block the IP address for 30 minutes. This configuration only takes effect for the rule-specified URL 1.test.com/login.html. 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15873/15564468747165_en-US.png)


