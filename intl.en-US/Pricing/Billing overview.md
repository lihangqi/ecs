# Billing overview {#concept_isb_scd_5db .concept}

This topic describes the items related to ECS billing, including billable resources and billing methods.

## Resource pricing {#section_lzm_rq2_zdb .section}

For more information about ECS resource prices, see Pricing.

## Billable resources {#section_zpf_wr2_zdb .section}

The following resources determine the price of an ECS instance:

-   Instance types, images, and disks: The prices of these resources vary based on their billing methods, including subscription and pay-as-you-go. For more information, see [Billing method comparison](reseller.en-US/Pricing/Billing method comparison.md#).
    -   The instance type determines the number of vCPU cores and the size of memory.
    -   Images

        |Type|Price|
        |:---|:----|
        |Public image|         -   Public images of the Windows Server or Red Hat Enterprise Linux operating systems may incur charges. The price is subject to the information displayed at the time of purchase.
        -   Other public images are free of charge.
 |
        |Custom image|If custom images are obtained from the Alibaba Cloud Marketplace, the price is subject to the information provided by image suppliers.|
        |Shared image|If shared images are obtained from the Alibaba Cloud Marketplace, the price is subject to the information provided by image suppliers.|
        |Marketplace image|The price is subject to the information provided by image suppliers.|

    -   Disks
        -   The disks created together with an ECS instance have the same billing method as the ECS instance.
        -   The disks that you separately create on the **Disks** page through the [ECS console](https://partners-intl.console.aliyun.com/#/ecs) only support the pay-as-you-go billing method. After a pay-as-you-go disk is attached to an ECS instance, you can change the billing method of the disk from pay-as-you-go to subscription through the Switch to Subscription operation or instance configuration upgrade. In this way, you can synchronize the lifecycle of the disk with that of the ECS instance. For more information, see [Switch from pay-as-you-go to subscription billing](reseller.en-US/Pricing/Switch from Pay-As-You-Go to Subscription billing.md#) and [Upgrade configurations of Subscription instances](../../../../reseller.en-US/Instances/Change configurations/Upgrade configurations/Upgrade configurations of Subscription instances.md#).
        -   Subscription disks directly created for a subscription instance are billed on a yearly or monthly basis and have the same lifecycle as the instance. For more information, see [Subscription](reseller.en-US/Pricing/Subscription.md#).
-   Internet bandwidth: If a public IP address is assigned to your ECS instance when you create or upgrade the ECS instance, you must pay for the Internet bandwidth. For more information about billing, see [Billing of Internet bandwidth](reseller.en-US/Pricing/Billing of Internet bandwidth.md#).

    **Note:** ECS instances in a VPC can access the Internet by binding an EIP. You need to purchase an EIP. For more information about billing, see [Pay-as-you-go](../../../../reseller.en-US/Pricing/Pay-As-You-Go.md#).

-   Snapshots: You must pay for created snapshots. For more information about billing, see [Billing of snapshots](reseller.en-US/Pricing/Billing of snapshots.md#).

