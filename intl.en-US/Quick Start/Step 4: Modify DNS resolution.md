# Step 4: Modify DNS resolution {#concept_wbs_qws_l2b .concept}

Switch the DNS resolution of the website to Anti-Bot by modifying the DNS resolution record to finally enable the Anti-Bot protection for your website business.

We strongly recommend that you use the CNAME record to resolve your website domain to Anti-Bot. After you complete the domain configuration process in the Anti-Bot Service console, Anti-Bot assigns a CNAME record to the domain name. Add or modify the CNAME DNS resolution record for the website domain name with the assigned CNAME record to enable the Anti-Bot protection.

**Note:** Obtain the CNAME record, such as `xxxxxxxxxxxxx.alicloudwaf.com`, assigned by the Anti-Bot instance according to [Step 1: Add domain configuration](intl.en-US/Quick Start/Step 1: Add a domain.md#). 

## CNAME access descriptions {#section_ibk_vws_l2b .section}

Anti-Bot uses the CNAME record resolution method to enable protections for website domain. Additionally, the A record resolution method is also supported.

**Note:** We strongly recommended that you use the CNAME record resolution method for Anti-Bot. Using the CNAME record resolution method to access the Anti-Bot instance, in some extreme situations, such as node failure and server room fault,  the automatic switching of Anti-Bot node IPs can be achieved, and even requests can be directly resolved back to the origin server. This mostly guarantees the stability of the website business and offers high availability and disaster recovery.

If you have to access the Anti-Bot instance by using the A record resolution method, \(for example, the @ record conflicts with the MX record\), you can obtain the IP of the Anti-Bot instance by pinging the CNAME record assigned by the Anti-Bot instance. This IP is generally not changed often. Then, you can use the A record resolution method to complete the Anti-Bot access for your website.

## Domain name host record descriptions {#section_avy_1xs_l2b .section}

A domain name has multiple types of the host records. For example, the `abc.com` domain name has the following host records:

-   www: This record is used to accurately match domain name that start with www. For example, www.abc.com, but it does not works for `abc.com`.
-   @: This record is used to match the situation that requests `abc.com` directly.
-   \*: This record is used to match a wildcard domain name. For example, blog.abc.com, www.abc.com, and abc.com.

## Notes when modifying DNS resolution record {#section_kht_2xs_l2b .section}

-   The CNAME record can only be configured for one host record of a website domain. You can modify the value of the DNS to the CNAME record assigned by the Anti-Bot instance to enabled the Anti-Bot protection for the website domain.

-   Since there are conflicts between different DNS resolution record types, the CNAME record conflicts with other records, such as A record, MX record, and TXT record, for one host record. You can delete the other records that conflicted before adding the CNAME resolution record, or modify the original record type to the CNAME record type.

    **Note:** Complete the process of deleting other DNS records and adding the CNAME resolution record as soon as possible. For example, if you do not add a CNAME resolution record long time after you delete the A resolution record for a website domain, the domain fails to be resolved properly.

-   If you have to keep the MX record \(mail exchanger record\), you can use the A record resolution method to resolve your website domain to the IP of your Anti-Bot instance. Get the assigned IP of the Anti-Bot instance by pinging the CNAME record \(This IP is not changed often\). Then, modify the value of the A resolution record of the website domain to the IP of the Anti-Bot instance.

**Note:** Automatic Fault cluster scheduling and fault bypass operations are not supported when using the A record resolution method to access Anti-Bot.


## Procedure {#section_owr_xxs_l2b .section}

The following steps use Alibaba Cloud DNS and Oray DNS as examples to describe the DNS configuration method. For other DNS providers, you can refer to these steps for similar configurations.

**Alibaba Cloud DNS configuration example**

**Note:** Assume that you use [Alibaba Cloud DNS](https://www.alibabacloud.com/product/dns) to manage the resolution of your website domain, and the website domain has the A resolution record configured before you complete the domain configuration process in Anti-Bot according to [Step 1: Add domain configuration](intl.en-US/Quick Start/Step 1: Add a domain.md#).  Additionally, the domain is already filed if it is a domain of Mainland China. Then, you can add the Anti-Bot domain configuration for the website by one-click and the DNS resolution records are automatically updated. Follow these steps when the Anti-Bot domain configuration has been added for the website domain and the DNS resolution status is abnormal.

To modify the CNAME record of the website domain to access the Anti-Bot instance in Alibaba Cloud DNS, follow these steps:

1.  Log on to the [Alibaba Cloud DNS console](https://dns.console.aliyun.com/#/dns/domainList).
2.  Select the website domain in the domain list, and then click **Configure**.
3.  Select the host record, and then click **Edit**.

    **Note:** You can also delete the existing A record, and then click **Add Record** to add a new CNAME DNS record. After deleting the existing resolution record, add the CNAME resolution record as soon as possible. Otherwise, your website domain fails to be resolved.

4.  Change the record type to CNAME, and then add the CNAME record assigned by the Anti-Bot instance as the record value.

    **Note:** The TTL value is recommended to be set to 600 seconds \(10 minutes\). The larger the TTL value, the slower the synchronization and update of DNS records.


**Oray DNS configuration example**

Some DNS provider, such as Oray, may not support to directly modify the existing record type and the host record. In this situation, delete the existing A resolution record, and then add a new CNAME resolution record.

**Note:** After deleting the existing resolution record, add the CNAME resolution record as soon as possible. Otherwise, your website domain fails to be resolved.

## Verify the DNS resolution configuration { .section}

After you switch the DNS resolution of the website domain to the Anti-Bot instance, your website domain is protected by Anti-Bot. After the DNS resolution configuration for your website domain is complete, you can verify the DNS resolution configuration by pinging the website domain or by running some other tools,  such as [17ce](https://www.17ce.com/).

**Note:** As it takes time for the DNS resolution configuration to take effect, wait for about 10 minutes if you cannot visit the website domain.

