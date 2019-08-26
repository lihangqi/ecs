# Billing of Internet bandwidth {#publicIP_china .concept}

Alibaba Cloud only supports the Pay-As-You-Go billing method for ECS instance Internet bandwidth usage, known as PayByTraffic. Alibaba Cloud calculates the fees on an hourly basis according to actual traffic usage, regardless of ECS instance billing methods and network types. Network bandwidth pricing may vary according to the region. For more information about pricing, see Pricing of ECS instances.

**Note:** Alibaba Cloud does not charge any fee on intranet traffic.

## Internet bandwidth types {#section_kkc_xtk_zdb .section}

The following table lists Internet bandwidth types and related information for ECS instances.

|Internet bandwidth types|Definition|Bandwidth limit|
|:-----------------------|:---------|:--------------|
|Outbound bandwidth|The bandwidth for outbound traffic from ECS instances, for example, when your ECS instances provide external access or you want to download internal resources from the ECS instances by using an FTP client.| -   Subscription instance: up to 200 Mbit/s
-   Pay-As-You-Go instance: up to 100 Mbit/s

 |
|Inbound bandwidth|The bandwidth for inbound traffic to ECS instances, for example, when you want to download resources from the Internet to your ECS instances, or upload resources to the ECS instances by using an FTP client.|Up to 200 Mbit/s|

Alibaba Cloud only charges fees for outbound traffic usage. The fee is calculated on an hourly basis and the billing unit is USD/GiB. When creating an instance, you can set a peak value for the outbound bandwidth to avoid incurring excessive fees due to traffic bursts.

**Note:** No fee is charged for the traffic between ECS instances in the same LAN.

## Purchase Internet bandwidth {#section_okc_xtk_zdb .section}

Different methods apply when you are purchasing Internet bandwidth for different Internet access modes:

-   If an ECS instance needs to access the Internet by using its own Internet address, you must purchase Internet bandwidth while creating the instance.

    **How to purchase**: When [creating an ECS instance](../../../../reseller.en-US/Quick Start for Entry-Level Users/Step 2. Create an instance.md#), in the **Network Billing Method** part, select **Assign public IP** and set a peak value.

-   If your ECS instance is in a VPC network and you want to use an Elastic IP address \(EIP\) to access the Internet, you only need to purchase the EIP service. For more information about the EIP service, see [EIP address related documentation](../../../../reseller.en-US/Product Introduction/What is Elastic IP Address?.md#).

    **Note:** If your ECS instances access the Internet by using an EIP address, you must not select **Assign public IP** when you create an instance.


## Bill calculation example {#section_tkc_xtk_zdb .section}

Assume that the average bandwidth of your ECS instance in an hour is 0.5 Mbit/s and the bandwidth price is USD 0.081 per GiB. You must pay the following amount for the hourly traffic:

\[\(0.5 × 60 × 60\) /1024/8\] GiB × 0.081 USD/GiB = 0.018 USD

**Note:** In this example, it is assumed that the outbound traffic is 0.5 Mbit/s \(the average bandwidth of the ECS instance\). For actual calculations, you can go to **Billing Management** \> **Usage Records** to download the usage history of ECS.

