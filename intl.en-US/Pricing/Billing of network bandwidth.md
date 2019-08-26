# Billing of network bandwidth {#publicIP_china .concept}

Alibaba Cloud only supports postpaid billing for ECS instance Internet bandwidth, which is called **PayByTraffic**. Alibaba Cloud collects the fees on an hourly basis according to actual traffic usage, regardless of ECS instance billing methods and network types. Network bandwidth prices vary among regions. For more information about pricing, see Pricing of Elastic Cloud Server.

**Note:** Alibaba Cloud does not charge any fee on intranet traffic.

## Internet bandwidth types {#section_kkc_xtk_zdb .section}

The following table lists Internet bandwidth types and related information for ECS instances.

|Internet bandwidth types|Definition|Bandwidth limit|Increase bandwidth limit|
|:-----------------------|:---------|:--------------|:-----------------------|
|Outbound bandwidth|The bandwidth for outbound traffic from ECS instances. For example, your ECS instances provide external access or you want to download internal resources from the ECS instances by using an FTP client.| -   For Subscription instances, the maximum speed is 200 Mbit/s.
-   For Pay-As-You-Go instances, the maximum speed is 100 Mbit/s.

 | Open a ticket to increase the bandwidth limit to 200 Mbit/s for a Pay-As-You-Go instance.

 |
|Inbound bandwidth|The bandwidth for inbound traffic to ECS instances. For example, you want to download resources for external networks from inside the ECS instance, or upload resources to ECS instances by using an FTP client.|The maximum speed is 200 Mbit/s.|The limit cannot be increased.|

Alibaba Cloud only charges fees for outbound traffic usage. The fee is calculated on an hourly basis and the billing unit is USD/GB. To prevent high charges because of sudden traffic spikes, you can set a peak value for outbound bandwidth while creating an instance.

**Note:** Traffic between ECS instances on the same LAN is free of charge.

## Purchase Internet bandwidth {#section_okc_xtk_zdb .section}

You can use different methods to purchase Internet bandwidth for different Internet access modes:

-   If an ECS instance needs to access the Internet by using its own Internet IP address, you must purchase Internet bandwidth while creating the instance.

    **How to purchase**: When [creating an ECS instance](../../../../reseller.en-US/Quick Start for Entry-Level Users/Step 2. Create an instance.md#), in the **Network Billing Method** section, select **Assign public IP**.

-   If your ECS instance is in a VPC network and you want to use an EIP \(Elastic IP address\) to access the Internet, you only need to purchase the EIP service. For more information about the EIP service, see [EIP address related documentation](../../../../reseller.en-US/Product Introduction/What is Elastic IP Address?.md#).

    **Note:** If your ECS instances access the Internet by using an EIP address, you must not select **Assign public IP** when you create an instance.


## Payment options {#section_s3c_v5x_kfb .section}

Credits are used to pay for the network bandwidth.

## Bill calculation example {#section_tkc_xtk_zdb .section}

Suppose that the average bandwidth of your ECS instance in an hour is 0.5 Mbit/s and the bandwidth price is USB 0.081 per GB. You must pay the following amount for the hourly traffic:

\[\(0.5 \* 60 \* 60\) /1024/8\] GB \* 0.081 USD/GB = 0.018 USD

**Note:** In this example, for simplicity, it is assumed that the outbound traffic each second is 0.5 Mbit \(the average bandwidth of the ECS instance\). For actual calculations, you can go to **Billing Management** \> **Usage Records** to download the usage history of Elastic Compute Service \(ECS\) - Pay-As-You-Go.

