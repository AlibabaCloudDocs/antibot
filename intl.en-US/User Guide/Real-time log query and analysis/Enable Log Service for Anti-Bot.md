# Enable Log Service for Anti-Bot {#concept_obb_qxt_cgb .concept}

Log Service can collect access logs and protection logs from the websites protected by Anti-Bot in real time. Also, it can retrieve and analyze the collected log data in real time.

You can analyze the website access and attack behaviors based on the website logs collected in the Anti-Bot console in real time. This further allows you to assist your security management personnel in developing protection policies.

## Procedure {#section_v2q_zxt_cgb .section}

1.  Log on to the [Anti-Bot console](https://yundun.console.aliyun.com/?p=antibot).
2.  Choose **Reports** \> **Log Service**. Select the region where your instance is located.

    **Note:** If you are using Log Service for Anti-Bot for the first time, click **Authorize** to authorize Anti-Bot to store all the recorded logs in your logstore as instructed.

    ![](images/34260_en-US.png)

3.  From the Website Domain drop-down list, select the website domain name for which you want to enable Log Service. Then, click Enable.

    **Note:** The Website Domain drop-down list displays all the website domain names configured with Anti-Bot.

    ![](images/34261_en-US.png)


Now, Log Service has been enabled for the website domain name. Log Service automatically creates a dedicated logstore for your Alibaba Cloud account. Anti-Bot automatically imports the logs of all the website domain names enabled with Log Service to the dedicated logstore in real time.

Then, you can retrieve and analyze the access logs of the website domain names enabled with Log Service.

![](images/34262_en-US.png)

## Restrictions and instructions {#section_fzx_gzt_cgb .section}

-   Other data cannot be written to the dedicated logstore.

    **Note:** The website logs recorded by Anti-Bot are stored in the dedicated logstore, where you cannot write other data through APIs and SDKs.

-   Currently, the basic settings \(such as the storage period\) of the dedicated logstore cannot be modified.
-   Do not delete or modify the default settings created by Log Service, such as the default project, logstore, index, and dashboard.
-   Log Service updates and upgrades the log query analysis function from time to time. The indexes and default reports of the dedicated logstore will be automatically updated.
-   If the RAM user requires the log query analysis function, grant the related Log Service permissions to the RAM user through RAM.

