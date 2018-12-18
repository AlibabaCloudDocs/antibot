# Fields in the log entry {#concept_sgs_sc5_cgb .concept}

Anti-Bot Service keeps detailed log entries for your domains, including access requests and attack logs. Each log entry contains dozens of fields. You can perform query and analysis based on specific fields.

|Field|Descriptions|Example|
|:----|:-----------|:------|
|\_\_topic\_\_|The topic of the log entry. The value of this field is antibot\_access\_log, which cannot be changed.|antibot\_access\_log|
|antibot|The type of the Anti-Bot Service protection strategy that applies, which includes:-   ratelimit: Frequency control
-   sdk: APP protection
-   intelligence: Crawler intelligence
-   acl: HTTP ACL policy
-   blacklist: Blacklist

|ratelimit|
|antibot\_action|The action performed by the Anti-Bot Service protection strategy, which includes:-   challenge: Verifying using an embedded JavaScript script
-   drop: Blocking
-   captcha: Verifying using a slider captcha
-   report: Logging the access event

|drop|
|antibot\_rule|The rule ID of the Anti-Bot Service protection that was triggered.|5472|
|antibot\_verify|The results of the verification methods used in the Anti-Bot Service.**Note:** When the value of the antibot\_action field is challenge or captcha, this value is logged.

-   challenge\_fail: JS verification failed
-   challenge\_pass: JS verification passed
-   captcha\_fail: slider validation failed
-   captcha\_pass: slider validation passed

|challenge\_fail|
|block\_action|The interception type of the Anti-Bot Service that was triggered. The value is fixed to antibot.|antibot|
|body\_bytes\_sent|The size of the body in the access request, which is measured in Bytes.|2|
|content\_type|The content type of the access request.|application/x-www-form-urlencoded|
|host|The source website.|api.aliyun.com|
|http\_cookie|The client-side cookie, which is included in the request header.|k1=v1;k2=v2|
|http\_referer|The URL information of the request source, which is included in the request header. `-` indicates no URL information.|http://xyz.com|
|http\_user\_agent|The User Agent field in the request header, which contains information such as the client browser and the operating system.|Dalvik/2.1.0 \(Linux; U; Android 7.0; EDI-AL10 Build/HUAWEIEDISON-AL10\)|
|http\_x\_forwarded\_for|The X-Forwarded-For \(XFF\) information in the request header, which identifies the original IP address of the client that connects to the web server using a HTTP proxy or load balancing.|-|
|https|Indicates whether the request is an HTTPS request.-   true: the request is an HTTPS request.
-   false: the request is an HTTP request.

|true|
|matched\_host|The matched domain name \(extensive domain name\) that is protected by Anti-Bot Service. If no domain has been matched, the value is `-`.|\*.aliyun.com|
|real\_client\_ip|The real IP address of the client. If the system cannot get the real IP address, the value is `-`.|1.2.3.4|
|region|The information of the region where the Anti-Bot instance is located.|cn|
|remote\_addr|The IP address of the client that sends the access request.|1.2.3.4|
|remote\_port|The port of the client that sends the access request.|23713|
|request\_length|The size of the request, measured in Bytes.|123|
|request\_method|The HTTP request method used in the access request.|GET|
|request\_path|The relative path of the request. The query string is not included.|/news/search.php|
|request\_time\_msec|The request time, which is measured in microseconds.|44|
|request\_traceid|The unique ID of the access request.|7837b11715410386943437009ea1f0|
|server\_protocol|The response protocol and the version number of the origin server.|HTTP/1.1|
|status|The status of the HTTP response to the client returned by Anti-Bot Service.|200|
|time|The time when the access request occurs.|2018-05-02T16:03:59+08:00|
|ua\_browser|The information of the browser that sends the request.|ie9|
|ua\_browser\_family|The family of the browser that the sent the request.|internet explorer|
|ua\_browser\_type|The type of the browser that the sent the request.|web\_browser|
|ua\_browser\_version|The version of the browser that sends the request.|9.0|
|ua\_device\_type|The type of the client device that sends the request.|computer|
|ua\_os|The operating system used by the client that sends the request.|windows\_7|
|ua\_os\_family|The family of the operating system used by the client.|windows|
|upstream\_addr|A list of back-to-origin IP addresses, separated by commas. The format of an address is `IP:Port`.|1.2.3.4:443|
|upstream\_ip|The origin IP address that corresponds to the access request. For example, if the origin server is an ECS instance, the value of this field is the IP address of the ECS instance.|1.2.3.4|
|upstream\_response\_time|The time that the origin site takes to respond to the Anti-Bot request, which is measured in seconds. "-" indicates the timeout of the request.|0.044|
|upstream\_status|The response status that Anti-Bot receives from the origin server. "-" indicates that no response is received. The reason can be the response timeout, or the request being blocked by Anti-Bot.|200|
|user\_id|Alibaba Cloud account ID.|12345678|
|wxbb\_action|The action performed when the Anti-Bot Service protection type is APP Enhanced protection:-   close: Blocking, the same as the drop value in the antibot\_action filed.
-   test: Logging the access event, the same as the report value in the antibot\_action field.
-   pass: Passing

**Note:** If the SDK protection is not integrated, the value is -.

|close|
|wxbb\_invalid\_wua|APP Enhanced protection strategy type. For details, contact technical support.|valid wua|
|wxbb\_vmp\_verify|The result of whether the vmp signature is valid.-   true: Valid
-   false: Invalid

|true|

