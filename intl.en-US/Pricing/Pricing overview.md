# Pricing overview {#concept_isb_scd_5db .concept}

This topic describes the ECS resources that are charged fees and the corresponding billing methods.

## Pricing {#section_lzm_rq2_zdb .section}

For the prices of ECS resources, see the pricing page.

## Billable ECS resources {#section_zpf_wr2_zdb .section}

The following types of Alibaba Cloud resources incur fees:

-   Instance types, images, and cloud disks

    The prices of these resources are set according to the billing method you select. For information about how the billing methods compare with each other, see [Billing method comparison](reseller.en-US/Pricing/Billing method comparison.md#).

    -   Instance types: The instance type determines the number of vCPU cores and the size of memory.

    -   Images

        |Type|Price|
        |:---|:----|
        |Public image|         -   Charges apply only for Windows Server OS images and Red Hat images.
        -   Linux or Unix-like OS images are provided free of charge.
 |
        |Custom image and shared image|If they are created by using an image from Alibaba Cloud Marketplace, the price is determined by the independent software vendor \(ISV\).|
        |Marketplace image|The price is determined by the ISV.|

    -   Cloud disks

-   Cloud disks created along with an ECS instance have the same billing method as the ECS instance.
-   Cloud disks created separately through the [ECS console](https://ecs.console.aliyun.com/?spm=a2c4g.11186623.2.9.FNEORG#/home) are billed according to the [Pay-As-You-Go](reseller.en-US/Pricing/Pay-As-You-Go.md#) billing method. After attaching such a cloud disk to a Pay-As-You-Go instance, you can change its billing method to Subscription to synchronize its lifecycle with the instance. For more information, see [switch from Pay-As-You-Go to Subscription](switch from Pay-As-You-Go to SubscriptionEN-US_TP_9588.dita#PAYGtoSubs_china) or [upgrade the configurations of the instance](../DNECS19100341/EN-US_TP_9643.dita#concept_jl1_2bf_5db).
-   Cloud disks created separately through the [ECS console](https://partners-intl.console.aliyun.com/#/ecs) are billed according to the [Pay-As-You-Go](reseller.en-US/Pricing/Pay-As-You-Go.md#) billing method. After attaching such a cloud disk to a Pay-As-You-Go instance, you can change its billing method to Subscription to synchronize its lifecycle with the instance. For more information, see [switch from Pay-As-You-Go to Subscription](switch from Pay-As-You-Go to SubscriptionEN-US_TP_9588.dita#PAYGtoSubs_china) or [upgrade the configurations of the instance](../DNECS19100341/EN-US_TP_9643.dita#concept_jl1_2bf_5db).
-   Cloud disks created for a Subscription instance are billed according to the [Subscription](reseller.en-US/Pricing/Subscription.md#) billing method and have the same lifecycle as the instance.
-   Public network bandwidth: If a public IP address is assigned to your ECS instance when you create or upgrade it, you must pay for the public network bandwidth. For more information, see [Billing of Internet bandwidth](reseller.en-US/Pricing/Billing of Internet bandwidth.md#).

    **Note:** VPC-connected ECS instances can access the Internet after you attach an Elastic IP \(EIP\) address to them. For more information, see [Billing of EIP](Billing of EIP../../SP_73/DNEIP11831937/EN-US_TP_12818.dita#concept_rcd_sgl_vdb).

-   Snapshots: Currently, snapshots are provided free of charge.


