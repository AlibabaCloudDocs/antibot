# Log field description {#concept_sgs_sc5_cgb .concept}

Log Service for Anti-Bot Service \(Anti-Bot\) records the access logs and attack and defense logs of protected website domain names in detail. A log contains dozens of fields. You can select specific fields for query analysis as needed.

|Field|Description|Example|
|:----|:----------|:------|
|\_\_topic\_\_|The log topic. This field is invariably set to antibot\_access\_log.|antibot\_access\_log|
|antibot|The type of the triggered Anti-Bot protection policy, including: -   ratelimit: rate limiting
-   sdk: app protection
-   algorithm: algorithm pattern
-   intelligence: bot intelligence
-   acl: access control list
-   blacklist: blacklist

 |ratelimit|
|antibot\_action|The operation specified by the Anti-Bot protection policy, including: -   challenge: Deliver a JavaScript script for verification
-   drop: Intercept
-   captcha: Verify by dragging a slider
-   report: Monitor only

 |drop|
|antibot\_rule|The ID of the triggered Anti-Bot protection rule.|5472|
|antibot\_verify|The result of the verification performed by Anti-Bot. **Note:** This value is recorded when the antibot\_action field is set to challenge or captcha.

 -   challenge\_fail: JavaScript verification fails.
-   challenge\_pass: JavaScript verification is passed.
-   captcha\_fail: Slide captcha verification fails.
-   captcha\_pass: Slide captcha verification is passed.

 |challenge\_fail|
|block\_action|The type of the bot protection that is triggered. The value is invariably set to antibot.|antibot|
|body\_bytes\_sent|The size of HTTP body \(in byte\) sent to the client.|2|
|content\_type|The content type of the access request.|application/x-www-form-urlencoded|
|host|The source website.|api.aliyun.com|
|http\_cookie|The cookie information about the access client, which is included in the access request header.|k1=v1;k2=v2|
|http\_referer|The source URL of the access request, which is included in the access request header. `-` is displayed if no source URL is available.|http://xyz.com|
|http\_user\_agent|The User Agent field in the access request header, which typically includes the web browser identifier and operating system identifier of the source client.|Dalvik/2.1.0 \(Linux; U; Android 7.0; EDI-AL10 Build/HUAWEIEDISON-AL10\)|
|http\_x\_forwarded\_for|The XFF header information in the access request header, which is used to identify the original IP addresses of the clients connected to a web server through the HTTP proxy or SLB.|-|
|https|Whether the access request is an HTTPS request. Valid values: -   true: The access request is an HTTPS request.
-   false: The access request is an HTTP request.

 |true|
|matched\_host|The matched domain name configured with Anti-Bot, which may be a wildcard domain name. `-` is displayed if no related domain name configuration is matched.|\*.aliyun.com|
|real\_client\_ip|The actual IP address of the access client. `-` is displayed if no actual IP address is retrieved.|1.2.3.4|
|region|The information about the region where the Anti-Bot instance is located.|cn|
|remote\_addr|The IP address of the client that initiates the access request.|1.2.3.4|
|remote\_port|The port of the client that initiates the access request.|23713|
|request\_length|The length of the access request. Unit: bytes.|123|
|request\_method|The HTTP request method of the access request.|GET|
|request\_path|The relative path of the request \(excluding the query string\).|/news/search.php|
|request\_time\_msec|The duration of the access request. Unit: milliseconds.|44|
|request\_traceid|The unique ID of the access request.|7837b11715410386943437009ea1f0|
|server\_protocol|The protocol and version of the response returned by the origin server.|HTTP/1.1|
|status|The status of the HTTP response that Anti-Bot returns to the client.|200|
|time|The occurrence time of the access request.|2018-05-02T16:03:59+08:00|
|ua\_browser|The information about the web browser that initiates the access request.|ie9|
|ua\_browser\_family|The family of the web browser that initiates the access request.|internet explorer|
|ua\_browser\_type|The type of the web browser that initiates the access request.|web\_browser|
|ua\_browser\_version|The version of the web browser that initiates the access request.|9.0|
|ua\_device\_type|The device type of the client that initiates the access request.|computer|
|ua\_os|The operating system of the client that initiates the access request.|windows\_7|
|ua\_os\_family|The operating system family of the client that initiates the access request.|windows|
|upstream\_addr|The origin address list of Anti-Bot in the format of `IP address:Port`. Separate multiple IP addresses with commas \(,\).|1.2.3.4:443|
|upstream\_ip|The origin IP address corresponding to the access request. For example, if Anti-Bot forwards the access request to an ECS instance, this parameter returns the IP address of the back-to-origin ECS instance.|1.2.3.4|
|upstream\_response\_time|The time for the origin server to respond to an Anti-Bot request. Unit: seconds. The response times out if "-" is returned.|0.044|
|upstream\_status|The status of the response that the origin server returns to Anti-Bot. No response is available if "-" is returned. For example, the request is intercepted by Anti-Bot, or the response returned by the origin server times out.|200|
|user\_id|AliUID of the Alibaba Cloud account.|12345678|
|wxbb\_action|If the protection type of Anti-Bot is app protection, the following actions are supported: -   close: intercepts requests. That is, the antibot\_action field is set to drop.
-   test: only monitors requests. That is, the antibot\_action field is set to report.
-   pass: allows requests.

 **Note:** This field is set to - if SDK protection is not configured.

 |close|
|wxbb\_invalid\_wua|For more information about app protection, consult your technical engineer.|valid wua|
|wxbb\_vmp\_verify|Whether the VMP signature is valid. -   true: valid
-   false: invalid

 |true|

