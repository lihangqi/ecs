# Billing {#concept_abd_vlm_cfb .concept}

This topic describes the billing methods of a burstable performance instance. The performance of a burstable performance instance is governed by its CPU credits. Specifically, the CPU credits allow you to control the cost of an instance. If your instance consumes additional CPU credits, additional fees may be incurred. Therefore, the price of a burstable performance instance comprises of the instance purchase fee and additional fees.

## Instance purchase fee {#section_jff_2i1_cse .section}

Burstable performance instances support the Pay-As-You-Go and Subscription billing methods. For information about how the billing methods compare with each other, see [Billing method comparison](../../../../reseller.en-US/Pricing/Billing method comparison.md#).

For the price of a burstable performance instance, see [Pricing](https://www.alibabacloud.com/product/ecs).

A burstable performance instance can be a preemptible instance. For more information, see [Preemptible instances](reseller.en-US/Instances/Instance purchasing options/Preemptible instances/Preemptible instances.md#).

After creating a Pay-As-You-Go instance, you can purchase a Reserved Instance \(RI\) and use it to generate a billing discount. An RI is a discount coupon with specific attributes. For more information, see [RI overview](reseller.en-US/Instances/Instance purchasing options/Reserved Instances/RI overview.md#). The following limitations apply if you use RIs for a burstable performance instance:

-   You can only purchase zonal RIs.
-   You cannot merge, split, or change the scope of RIs.
-   RIs do not match preemptible instances.

## Impact of performance modes on billing {#section_j3k_6ey_zkl .section}

The following table describes how the performance mode affects the billing of a burstable performance instance.

|Performance mode|Instance purchase fee|Additional fee|
|----------------|---------------------|--------------|
|Standard mode|The fee is determined by the billing method, not the performance mode. For more information, see [Instance purchase fee](#section_gm2_2zo_l5b).|None|
|Unlimited mode|The fee is determined by the billing method, not the performance mode. For more information, see [Instance purchase fee](#section_gm2_2zo_l5b).| If your instance consumes additional CPU credits, you may need to pay additional fees:

-   Overdrawn CPU credits are billed by hour.
-   If you use advance CPU credits and switch to the standard mode before the advance CPU credits are cleared, a one-off fee is charged for the advance CPU credits and the current CPU credit balance remains unchanged.
-   If you use advance CPU credits and stop or release the instance before the advance credits are cleared, a one-off fee is charged for the advance CPU credits. Stopping an instance affects the CPU credits. For more information, see [Earn CPU credits](reseller.en-US/Instances/Instance type families/Burstable performance instances/Overview.md#section_n3h_act_eb7).

 |

The following table describes how fees are collected in unlimited mode.

|Region|Windows instance \(USD/CPU credit\)|Linux instance \(USD/CPU credit\)|
|:-----|:----------------------------------|:--------------------------------|
|Mainland China|0.0008|0.0008|
|Outside Mainland China|0.0016|0.0008|

## Price comparison between burstable performance instances and enterprise-level instances {#section_fu4_5tl_2hr .section}

Overdrawn CPU credits only take effect in unlimited mode. If a burstable performance instance uses excess overdrawn CPU credits, the total price of the instance may equal or exceed enterprise-level instances of equivalent configurations. For more information, see [Unlimited mode](reseller.en-US/Instances/Instance type families/Burstable performance instances/Overview.md#section_v1t_6rl_7h3).

**Note:** The following description uses instance prices on April 30th, 2019 for example. For the latest prices, see [Pricing](https://www.alibabacloud.com/product/ecs).

The following figure compares the price of a burstable performance instance ecs.t5-lc1m2.large with an enterprise-level instance ecs.c5.large. Both the instances have two vCPUs and 4 GiB memory. The ecs.t5-lc1m2.large instance uses overdrawn CPU credits.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/161269/156385837646093_en-US.png)

In the preceding figure, the hourly price is calculated based on the purchase fee of ecs.t5-lc1m2.large \(10% baseline performance\) and the fee of overdrawn CPU credits \(Linux instance in China Beijing\). The formula is the same for different instance types but the CPU usage threshold may vary.

The price of the two instances varies according to the following scenarios:

-   If the average CPU usage is lower than 62.08%, ecs.t5-lc1m2.large costs less.
-   If the average CPU usage equals 62.08%, the two instances cost the same.
-   If the average CPU usage is higher than 62.08%, the ecs.c5.large instance costs less.

**Note:** If you can accurately estimate the performance requirements of your instances, you may choose an appropriate instance type based on the CPU usage threshold. This helps you achieve high performance at a low cost.

The following figures show the price change trend of several best-selling burstable performance instances. For the price change trends of other instance types, open a ticket.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/161269/156385837645519_en-US.png)

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/161269/156385837646092_en-US.png)

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/161269/156385837646095_en-US.png)

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/161269/156385837746096_en-US.png)

