# Retrieve the actual IP addresses of access users {#concept_l4w_fkc_p2b .concept}

In most service scenarios, access requests to a website are not directly sent from access users to the website's origin server. Instead, the access requests may pass through intermediate proxy servers, such as CDN, Anti-DDoS Service Pro, WAF, and Anti-Bot. For example, a website may be deployed in this schema: user \> CDN, Anti-DDoS Service Pro, or Anti-Bot \> origin server. After an access request is forwarded through multiple layers of acceleration or proxy, how does the origin server retrieve the actual client IP address that initiates the request?

In normal cases, before forwarding a user's access request to the next-hop server, the transparent proxy server adds an **X-Forwarded-For** record to the HTTP request header to record the user's actual IP address. The record format is `X-Forwarded-For:user IP address`. If the access request passes through multiple intermediate proxy servers, **X-Forwarded-For** records the user's actual IP address and the intermediate proxy servers' IP addresses in the following format: `X-Forwarded-For:user's IP address, proxy server 1-IP address, proxy server 2-IP address, proxy server 3-IP address, …`.

**Note:** Anti-Bot and WAF adopt the same forwarding configuration and device. If your website domain name is configured with WAF and Anti-Bot to implement application-layer protection and intercept bot traffic, **X-Forwarded-For** records the IP addresses of only one proxy server.

Therefore, common application servers can **use X-Forwarded-For to retrieve access users' actual IP addresses**.

You can select a suitable X-Forwarded-For configuration scheme to retrieve access users' actual IP addresses based on your application server.

**Note:** Before configuration, be sure to back up the existing environment, including the ECS instance snapshot and the configuration file of the web application server.

## Nginx configuration scheme {#section_msy_zkc_p2b .section}

**1. Ensure that the http\_realip\_module module is installed.**

To implement load balancing, Nginx uses **http\_realip\_module** for retrieving actual IP addresses.

Run `# nginx -V | grep http_realip_module` to check whether the module is installed. If the module is not installed, recompile Nginx and load the module.

**Note:** In normal cases, the module is not installed by default if Nginx was installed by using a one-click installation package.

Install **http\_realip\_module** by using the following method:

```
wget http://nginx.org/download/nginx-1.12.2.tar.gz
tar zxvf nginx-1.12.2.tar.gz
cd nginx-1.12.2
./configure --user=www --group=www --prefix=/alidata/server/nginx --with-http_stub_status_module --without-http-cache --with-http_ssl_module --with-http_realip_module
make
make install
kill -USR2 `cat /alidata/server/nginx/logs/nginx.pid`
kill -QUIT `cat /alidata/server/nginx/logs/ nginx.pid.oldbin`
```

**2. Modify the configuration of the server for Nginx.**

Open the `default.conf` configuration file and add the following content in `location / {}`:

**Note:** 

`ip_range1, 2, ..., x` indicates the origin CIDR block of Anti-Bot. The IP addresses must be added one by one.

```
set_real_ip_from ip_range1;
set_real_ip_from ip_range2;
...
set_real_ip_from ip_rangex;
real_ip_header    X-Forwarded-For;
```

**3. Modify the log format \(log\_format\).**

log\_format is typically located in the HTTP configuration of the `nginx.conf` configuration file. In log\_format, replace the remote-address field with the x-forwarded-for field. That is, modify log\_format as follows:

```
log_format  main  '$http_x_forwarded_for - $remote_user [$time_local] "$request" ' '$status $body_bytes_sent "$http_referer" ' '"$http_user_agent" ';
```

After the preceding operation, run `nginx -s reload` to restart Nginx. After the configuration takes effect, the Nginx server can record access users' actual IP addresses by using X-Forwarded-For.

## IIS 6 configuration scheme {#section_w4f_gkc_p2b .section}

You can install the [F5XForwardedFor.dll](https://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/cn/slb/0.0.121/assets/F5XForwardedFor2008.zip) plug-in to retrieve access users' actual IP addresses from the access log recorded by the IIS 6 server.

1.  Based on the operating system version of your server, copy the F5XForwardedFor.dll file from the x86\\Release or x64\\Release directory to the specified directory, such as C:\\ISAPIFilters. Ensure that the IIS process has read and write permissions on the directory.
2.  Open IIS Manager, locate the currently activated website, right-click it, and choose **Attributes**.
3.  On the Attributes page, switch to **ISAPI Filters** and click **Add**.
4.  In the Add window, set the following parameters and click **Add**.
    -   **Filter Name**: F5XForwardedFor
    -   **Executable**: Full path of F5XForwardedFor.dll, for example, C:\\ISAPIFilters\\F5XForwardedFor.dll
5.  Restart the IIS server and wait for the configuration to take effect.

## IIS 7 configuration scheme {#section_apf_gkc_p2b .section}

You can install the [F5XForwardedFor](https://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/cn/slb/0.0.121/assets/x_forwarded_for.rar) module to retrieve access users' actual IP addresses.

1.  Based on the operating system version of the server, copy the F5XFFHttpModule.dll and F5XFFHttpModule.ini files from the x86\\Release or x64\\Release directory to the specified directory, such as C:\\x\_forwarded\_for\\x86 or C:\\x\_forwarded\_for\\x64. Ensure that the IIS process has read and write permissions on the directory.
2.  In **IIS Server**, double-click **Module**.

    ![](../../SP_197/DNwaf1822307/images/7620_en-US.png)

3.  Click **Configure Local Module**.

    ![](../../SP_197/DNwaf1822307/images/7621_en-US.png)

4.  In the **Configure Local Module** dialog box, click **Register** to register the downloaded DLL file.

    -   Register the x\_forwarded\_for\_x86 module
        -   **Name**: x\_forwarded\_for\_x86
        -   **Path**: C:\\x\_forwarded\_for\\x86\\F5XFFHttpModule.dll
    -   Register the x\_forwarded\_for\_x64 module
        -   **Name**: x\_forwarded\_for\_x64
        -   **Path**: C:\\x\_forwarded\_for\\x64\\F5XFFHttpModule.dll
    ![](../../SP_197/DNwaf1822307/images/7622_en-US.png)

5.  After registration, select the newly registered modules x\_forwarded\_for\_x86 and x\_forwarded\_for\_x64, and click **OK**.

    ![](../../SP_197/DNwaf1822307/images/7624_en-US.png)

6.  In API and CGI Restrictions, add the registered DLL file, and change **Restriction** to **Allow**.

    ![](../../SP_197/DNwaf1822307/images/7625_en-US.png)

7.  Restart the IIS server and wait for the configuration to take effect.

## Apache configuration scheme {#section_dtm_vnc_p2b .section}

**For Windows operating systems**

The installation packages of Apache 2.4 and later provide the remoteip\_module module file \(mod\_remoteip.so\). You can retrieve access users' actual IP addresses by using this module.

1.  Create a configuration file named httpd-remoteip.conf in the extra configuration folder \(conf/extra/\) of Apache.

    **Note:** Load the related configuration by introducing the remoteip.conf configuration file. This reduces the number of times of direct modification of the httpd.conf file, and avoids service exceptions due to misoperation.

2.  In the httpd-remoteip.conf configuration file, add the following rule of retrieving access users' actual IP addresses.

    ```
    # Load the mod_remoteip.so module
    LoadModule remoteip_module modules/mod_remoteip.so
    # Set the RemoteIPHeader header
    RemoteIPHeader X-Forwarded-For
    # Set the origin CIDR block
    RemoteIPInternalProxy 112.124.159.0/24 118.178.15.0/24 120.27.173.0/24 203.107.20.0/24 203.107.21.0/24 203.107.22.0/24 203.107.23.0/24 47.97.128.0/24 47.97.129.0/24 47.97.130.0/24 47.97.131.0/24
    ```

3.  Modify the conf/httpd.conf configuration file and include the httpd-remoteip.conf configuration file.

    ```
    Include conf/extra/httpd-remoteip.conf
    ```

4.  Modify the log format in the httpd.conf configuration file.

    ```
    LogFormat "%a %l %u %t \"%r\" %>s %b \"%{Referer}i\" \"%{User-Agent}i\"" combined
    LogFormat "%a %l %u %t \"%r\" %>s %b" common
    ```

5.  Restart Apache to make the configuration effective.

**For Linux operating systems**

You can retrieve access users' actual IP addresses by installing the [mod\_rpaf](http://stderr.net/apache/rpaf/) third-party module of Apache.

1.  Run the following commands to install the mod\_rpaf module:

    ```
    wget http://stderr.net/apache/rpaf/download/mod_rpaf-0.6.tar.gz
    tar zxvf mod_rpaf-0.6.tar.gz
    cd mod_rpaf-0.6
    /alidata/server/httpd/bin/apxs -i -c -n mod_rpaf-2.0.so mod_rpaf-2.0.c
    ```

2.  Modify the Apache configuration file /alidata/server/httpd/conf/httpd.conf and append the following content to the end of the file:

    **Note:** `RPAFproxy_ips IP address` is not the public IP address provided by SLB. For the specific IP addresses, see the Apache log. Typically, you can find two IP addresses.

    ```
    LoadModule rpaf_module modules/mod_rpaf-2.0.so
    RPAFenable On
    RPAFsethostname On
    RPAFproxy_ips IP address
    RPAFheader X-Forwarded-For
    ```

3.  After appending the preceding content, run the following command to restart Apache to make the configuration effective:

    ```
    /alidata/server/httpd/bin/apachectl restart
    ```


**mod\_rpaf module configuration example**

```

LoadModule rpaf_module modules/mod_rpaf-2.0.so
RPAFenable On
RPAFsethostname On
RPAFproxy_ips 10.242.230.65 10.242.230.131
RPAFheader X-Forwarded-For
```

## Tomcat configuration scheme {#section_tpf_gkc_p2b .section}

Retrieve access users' actual IP addresses by enabling the X-Forwarded-For function of Tomcat.

Open the tomcat/conf/server.xml configuration file and modify the AccessLogValve log recording function as follows:

```
<Valve className="org.apache.catalina.valves.AccessLogValve" directory="logs"
prefix="localhost_access_log." suffix=".txt"
pattern="%{X-FORWARDED-FOR}i %l %u %t %r %s %b %D %q %{User-Agent}i %T" resolveHosts="false"/>
```

