# Increase the limits on the service bandwidth and request rate {#concept_i22_std_n2b .concept}

By default, Anti-Bot Service supports up to 100 Mbit/s bandwidth for Alibaba Cloud-based services and up to 10 Mbit/s for non-Alibaba Cloud-based services. The default maximum service request rate is 500 QPS. You can increase the limits on service bandwidth and request rate based on your needs.

## Service request rate {#section_fpw_lxh_4gb .section}

The service request rate is the number of concurrent requests per second that are sent to all domains protected by an Anti-Bot instance when no attack is in progress. Unit: QPS.

Each Anti-Bot instance supports a maximum request rate of 500 QPS by default.

## Service bandwidth {#section_fsq_std_n2b .section}

The service bandwidth is the peak traffic that is sent to all domains protected by an Anti-Bot instance when no attack is in progress. Unit: Mbit/s.

**Note:** The traffic that flows through Anti-Bot Service is measured independently of the bandwidth limits of other Alibaba Cloud services, such as CDN, SLB, and ECS.

By default, each Anti-Bot instance supports a maximum bandwidth of 100 Mbit/s for Alibaba Cloud-based services and a maximum bandwidth of 10 Mbit/s for non-Alibaba Cloud-based services. A higher bandwidth limit is provided for services that are deployed on Alibaba Cloud servers, such as ECS and SLB instances.

## Increase the limits on service bandwidth and request rate {#section_ksq_std_n2b .section}

If your service expects to receive high-bandwidth traffic or a large number of concurrent requests, you need to purchase additional bandwidth to handle the traffic or requests.

For example, assume that your service is not deployed on Alibaba Cloud services, and your current service bandwidth is 30 Mbit/s and the request rate is 1,500 QPS. For non-Alibaba Cloud-based services, each Anti-Bot instance supports a maximum bandwidth of 10 Mbit/s and a maximum request rate of 500 QPS. To prevent service interruptions, you need to pay additional fees for the exceeding 20 Mbit/s of bandwidth and 1,000 QPS request rate.

To meet your growing needs, you can upgrade your Anti-Bot instance for higher specifications.

**Note:** You can also increase the limits on service bandwidth and request rate when you buy the Anti-Bot instance.

## What if the maximum service bandwidth or request rate is exceeded? {#section_jsq_std_n2b .section}

If your service bandwidth or request rate exceeds the limit of your Anti-Bot instance, you will receive an alert and traffic forwarding may be affected.

When the maximum service bandwidth or request rate is exceeded, bandwidth throttling and random packet losses are likely to occur, which may lead to issues such as service interruptions, slowdowns, and delays.

If you are experiencing these issues, we recommend that you increase the limits on service bandwidth and request rate as soon as possible.

## Do I need to increase the QPS limit? {#section_h51_szh_4gb .section}

To see if you need to increase the QPS limit, you can estimate the combined peak request rate of your services that are protected by Anti-Bot Service. The maximum request rate supported by your Anti-Bot instance must be greater than the combined peak request rate of your services that are protected by the Anti-Bot instance.

**Example**

Assume that you are using an Anti-Bot instance to protect three websites, and the peak request rate of each website is no greater than 500 QPS. The combined peak request rate of the three websites is no greater than 1,500 QPS. In this case, you only need to purchase an Anti-Bot instance that provides a maximum service request rate of 1,500 QPS or above.

## Do I need to increase the bandwidth limit? {#section_hsq_std_n2b .section}

To see if you need to buy more bandwidth, you can estimate the combined peak bandwidth of the inbound and outbound traffic that flows through the services protected by Anti-Bot Service. The maximum service bandwidth supported by your Anti-Bot instance must be greater than the combined peak bandwidth of the inbound and outbound traffic that flows through the services protected by the Anti-Bot instance.

**Note:** Generally, the bandwidth of outbound traffic is greater than that of inbound traffic.

You can estimate the actual bandwidth by viewing the traffic statistics in the ECS console or other monitoring tools on your origin server.

**Note:** The traffic described here refers to the normal traffic that flows through your services.

To use Anti-Bot Service to protect your services, you need to direct all incoming traffic to Anti-Bot Service. When your services are running normally and no attack is in progress, Anti-Bot Service forwards all normal traffic back to the origin server. When your services are experiencing attacks, Anti-Bot Service filters out malicious traffic, and only forwards normal traffic back to the origin server. Therefore, the inbound and outbound traffic in the ECS console is normal traffic. If your services are deployed on multiple origin servers, you need to calculate the combined bandwidth of inbound and outbound traffic that flows through all origin servers.

**Example**

Assume that you are using an Anti-Bot instance to protect three websites, and the peak bandwidth of outbound traffic from each website is no greater than 10 Mbit/s. The combined peak bandwidth of outbound traffic from all three websites is no greater than 30 Mbit/s. In this case, you only need to purchase an Anti-Bot instance that provides a maximum service bandwidth of 30 Mbit/s or above.

