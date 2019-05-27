# Configure protection for the origin server {#task_p5p_h3c_p2b .task}

If the IP address of your origin server is exposed, an attacker may bypass Anti-Bot Service and launch direct attacks on your origin server. This topic describes how to configure protection for the origin server.

**Note:** Protection of the origin server is not required. Traffic forwarding is not affected when the protection is not configured. However, we recommend that you protect your origin server to eliminate risks arising from IP exposure.

**Verify whether the origin server IP is exposed**

Use Telnet to connect to the public IP of the origin server through its service port from a non-Alibaba Cloud host. If the connection is established, it indicates that the origin server is at risk. If an attacker obtains the public IP of the origin server, they can bypass Anti-Bot Service and access the origin server directly. If the connection fails, it indicates that the origin server is secure.

For example, test whether connections to the origin server IP through port 80 and 8080 can be established after you set up Anti-Bot Service for your domain. If connections are established, it indicates that your origin server is at risk.

**Notes**

Security groups can be difficult to use. Pay attention to the following points before configuring protection for the origin server.

-   Make sure that you have configured Anti-Bot Service for all domains that are attached to the ECS or SLB instance where security groups are created.
-   When failures occur in the Anti-Bot cluster, requests may be forwarded to the origin server to avoid service interruptions. In this situation, if you have configured protection for the origin server, users may not be able to access your origin server through the Internet.
-   When the Anti-Bot cluster scales out, and more back-to-origin CIDR blocks are added, 5xx errors may be frequently returned if you have configured security groups to protect the origin server.

1.  Log on to the [Anti-Bot Service console](https://yundun.console.aliyun.com/?p=antibot), and select the region where your Anti-Bot instance is located.
2.  Choose **Domain Configuration** and select **Back-to-origin CIDR Blocks for Anti-Bot** to view the back-to-origin CIDR blocks used by Anti-Bot Service. 

    **Note:** Back-to-origin CIDR blocks are periodically updated. We recommend that you pay attention to update notifications and add new back-to-origin CIDR blocks to corresponding security group rules in a timely manner to avoid false positives.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/160220/155896142444879_en-US.png)

3.  In the Back-to-origin CIDR Blocks dialog box, click **Copy** to copy all CIDR blocks.
4.  Configure security groups to allow access from back-to-origin CIDR blocks only. 
    -   **If your origin server is an ECS instance** 

        1.  Go to the [Instances](https://ecs.console.aliyun.com/#/server/region/cn-beijing) page, select the ECS instance that you want to configure security groups for, and click **Manage** under the Actions column.
        2.  In the left-side navigation pane, click Security Groups.
        3.  Select the security group that you want to change, and click **Add Rules**.
        4.  Click **Add Security Group Rule** and configure the security group rule as follows:

            **Note:** The Authorization Objects field supports CIDR blocks in the following format: 10.x.x.x/32. You can enter up to 10 comma-separated CIDR blocks.

            -   **NIC**: Internal Network

                **Note:** If your ECS instance is connected to a classic network, you need to set NIC to Public Network.

            -   **Rule Direction**: Ingress
            -   **Action**: Allow
            -   **Protocol Type**: Customized TCP
            -   **Authorization Type**: IPv4 CIDR Block
            -   **Port Range**: 80/443
            -   **Authorization Object**: Paste the back-to-origin CIDR blocks from step 3.
            -   **Priority**: 1
        5.  After you create this security group rule, add another security group rule as follows to block access from the Internet.
            -   **NIC**: Internal Network

                **Note:** If your ECS instance is connected to a classic network, you need to set NIC to Public Network.

            -   **Rule Direction**: Ingress
            -   **Action**: Forbid
            -   **Protocol Type**: Customized TCP
            -   **Port Range**: 80/443
            -   **Authorization Type**: IPv4 CIDR Block
            -   **Authorization Object**: 0.0.0.0/0
            -   **Priority**: 100
        **Note:** If your origin server needs to communicate with other IP addresses or applications, you must add another security group rule to allow access from them. Alternatively, you can add a security group rule to allow access from all ports and set it to the lowest priority.

    -   **If your origin server is an SLB instance** 

        In a similar manner, you need to add the back-to-origin CIDR blocks used by Anti-Bot Service to the whitelist of your SLB instance. For more information, see [Manage access control](../../../../intl.en-US/Archives/User Guide (Old Console)/Access control/Manage access control.md#).

        1.  Log on to the [Server Load Balancer console](http://slbnew.console.aliyun.com/#/list/cn-beijing), choose **Access Control**, and click **Create Access Control List**.
        2.  Specify an access control list name, add the back-to-origin CIDR blocks used by Anti-Bot Service, and click **OK**.
        3.  On the **Server Load Balancer** page, select your SLB instance.
        4.  In the **Listeners** tab, select the listener that you want to change and click **More** \> **Manage Access Control**.
        5.  Create a whitelist, add the access control list that contains the back-to-origin CIDR blocks used by Anti-Bot Service to the whitelist, and click **OK**.

After you configure protection for the origin server, you can test whether the origin server is accessible through port 80 and 8080 to check whether the configuration takes effect. If the origin server cannot be connected through these ports and your service is running normally, it indicates that the protection configuration is in effect.

