# Overview {#concept_n52_3v2_5db .concept}

This topic describes burstable performance instances, including their features, application scenarios, and concepts such as baseline performance, CPU credits, and performance modes. Burstable performance instances are able to burst above baseline CPU performance by using CPU credits.

## Application scenarios {#section_4tj_ovn_xrg .section}

When you use other types of Alibaba Cloud ECS instances, the number and performance metrics of the corresponding vCPUs are fixed, which means that you may be billed for unused computing resources. To resolve this issue, Alibaba Cloud offers burstable performance instances to help you build high-performance servers, at a low cost, for a wide range of scenarios that experience traffic spikes in specific time periods. Examples include stress test applications, light-load applications, microservices, and web application servers.

**Note:** For the types of burstable performance instances provided by Alibaba Cloud, see [t5 instance type family](#section_msp_0mo_a03). If the instance you initially select does not meet performance requirements, you can [change the instance type](#section_al8_1f0_syn).

## Features {#section_a4q_kz4_req .section}

A burstable performance instance continuously accrues CPU credits. In this way, when higher CPU performance is required, the accrued CPU credits can be used without affecting the resource usage of applications deployed on the instance. For more information, see [Baseline performance](#section_thj_iuv_7jz), [Earn CPU credits](#section_n3h_act_eb7), and [CPU credit consumption](#section_7w3_4ok_d60).

CPU credits allow you to allocate computing resources according to the overall service landscape. The computing capability during off-peak hours can be reserved for peak hours, to make full use of CPU resources. If your network experiences traffic spikes, you can choose to enable the unlimited mode to ensure high performance. In the unlimited mode, if CPU credits are used in advance or overdrawn, additional fees may be charged. In the standard mode, if the instance has no remaining CPU credits, its CPU usage will not burst above the baseline performance. For more information, see [Standard mode](#section_n0v_2ot_yvc) and [Unlimited mode](#section_v1t_6rl_7h3).

## t5 instance type family {#section_msp_0mo_a03 .section}

-   Equipped with 2.5 GHz Intel Xeon processors
-   The latest DDR4 memory
-   No fixed ratio of vCPU to memory
-   Baseline CPU performance, burstable, but restricted by accumulated CPU credits
-   Resource balance among compute, memory, and networks
-   Supports VPC network only
-   Suitable for the following scenarios:
    -   Web application servers
    -   Lightweight web servers
    -   Development and testing environments

|Instance types|vCPU|Memory \(GiB\)|Avg baseline CPU performance|CPU credits/hour|Max CPU credit balance|Local disks \(GiB\)[ \* ](reseller.en-US/Instances/Instance type families.md#)|Bandwidth \(Gbit/s\)[ \*\* ](reseller.en-US/Instances/Instance type families.md#)|Packet forwarding rate \(Thousand pps\)[ \*\*\* ](reseller.en-US/Instances/Instance type families.md#)|NIC queues[ \*\*\*\* ](reseller.en-US/Instances/Instance type families.md#)|ENIs[ \*\*\*\* ](reseller.en-US/Instances/Instance type families.md#)|Private IP address of a single ENI|
|:-------------|:---|--------------|:---------------------------|:---------------|:---------------------|--------------------------------------------|-----------------------------------------------|--------------------------------------------------------------------|-----------------------------------------|:----------------------------------|----------------------------------|
|ecs.t5-lc2m1.nano|1|0.5|10%|6|144|N/A|0.1|40|1|1|2|
|ecs.t5-lc1m1.small|1|1.0|10%|6|144|N/A|0.2|60|1|1|2|
|ecs.t5-lc1m2.small|1|2.0|10%|6|144|N/A|0.2|60|1|1|2|
|ecs.t5-lc1m2.large|2|4.0|10%|12|288|N/A|0.4|100|1|1|2|
|ecs.t5-lc1m4.large|2|8.0|10%|12|288|N/A|0.4|100|1|1|2|
|ecs.t5-c1m1.large|2|2.0|15%|18|432|N/A|0.5|100|1|1|2|
|ecs.t5-c1m2.large|2|4.0|15%|18|432|N/A|0.5|100|1|1|2|
|ecs.t5-c1m4.large|2|8.0|15%|18|432|N/A|0.5|100|1|1|2|
|ecs.t5-c1m1.xlarge|4|4.0|15%|36|864|N/A|0.8|200|1|2|6|
|ecs.t5-c1m2.xlarge|4|8.0|15%|36|864|N/A|0.8|200|1|2|6|
|ecs.t5-c1m4.xlarge|4|16.0|15%|36|864|N/A|0.8|200|1|2|6|
|ecs.t5-c1m1.2xlarge|8|8.0|15%|72|1728|N/A|1.2|400|1|2|6|
|ecs.t5-c1m2.2xlarge|8|16.0|15%|72|1728|N/A|1.2|400|1|2|6|
|ecs.t5-c1m4.2xlarge|8|32.0|15%|72|1728|N/A|1.2|400|1|2|6|
|ecs.t5-c1m1.4xlarge|16|16.0|15%|144|3456|N/A|1.2|600|1|2|6|
|ecs.t5-c1m2.4xlarge|16|32.0|15%|144|3456|N/A|1.2|600|1|2|6|

## Baseline performance {#section_thj_iuv_7jz .section}

Baseline performance enables a burstable performance instance to maintain steady CPU performance according to the selected instance type. That is, when the CPU usage equals the baseline performance, the instance earns the same CPU credits as it consumes. For more information, see the Avg baseline CPU performance column in [t5 instance type family](#section_msp_0mo_a03).

## Earn CPU credits {#section_n3h_act_eb7 .section}

CPU credits can be applied to adjust the computing capability of a burstable performance instance. The more credits that a burstable performance instance accrues, the more time it can burst beyond its baseline performance when higher performance is needed.

To ensure that you have sufficient CPU credits for running an instance, each vCPU is allocated 30 CPU credits after you create a burstable performance instance \(called launch CPU credit\). For example, an ecs.t5-lc1m2.large instance that is configured with two vCPUs receives 60 launch CPU credits after being created.

Each burstable performance instance continuously earns a fixed number of CPU credits per hour, depending on the instance type. The number of CPU credits that an instance earns per hour per vCPU corresponds to its baseline performance. For more information, see the CPU credit/hour column in [t5 instance type family](#section_msp_0mo_a03).

**Note:** For example, an ecs.t5-c1m1.large instance with a baseline performance of 15% means that the CPU credits the instance can earn per hour per vCPU allow the instance to run at 15% usage for one hour or run at 100% usage for nine minutes \(60 × 15%\). Therefore, based on the baseline performance, each vCPU can earn nine CPU credits per hour. In this case, an ecs.t5-c1m1.large instance that is configured with two vCPUs earns 18 CPU credits per hour.

If a burstable performance instance earns more CPU credits than it consumes, the unused CPU credits are accrued in the CPU credit balance. The CPU credit balance can be retained for up to 24 hours to achieve a dynamic balance, which has an upper limit. For more information, see the Max. CPU credit balance column in [t5 instance type family](#section_msp_0mo_a03). For example, an ecs.t5-c1m1.large instance can earn 18 CPU credits per hour. Its maximum CPU credit balance is 432 \(18 × 24 hours\).

Stopping an instance affects CPU credits in the following ways:

-   If an instance is stopped but the **No fees for stopped instances \(VPC-Connected\)** feature is not enabled, the current CPU credit balance is unaffected and CPU credits continue to accrue.
-   If an instance is stopped and the **No fees for stopped instances \(VPC-Connected\)** feature is enabled, the accrued CPU credits are lost and the instance stops accruing CPU credits until you restart the instance.
-   If a Subscription instance expires, the current CPU credit balance is unaffected but the instance stops accruing CPU credits until you reactivate the instance.
-   If the payment of a Pay-As-You-Go instance is overdue, the current CPU credit balance is unaffected but the instance stops accruing CPU credits until you clear the overdue payment.

## CPU credit consumption {#section_7w3_4ok_d60 .section}

The number of CPU credits that a burstable performance instance consumes per hour corresponds to the number of vCPUs, CPU usage, and running time of the instance. One CPU credit is consumed in the following scenarios:

-   One vCPU running at 100% usage for one minute
-   One vCPU running at 50% usage for two minutes
-   Two vCPUs running at 25% usage for two minutes

A burstable performance instance starts to consume CPU credits after being started. Launch CPU credits are consumed first and cannot be accrued in the process of being used up. The instance then uses CPU credits that it has accrued in its CPU credit balance.

-   If the CPU usage is lower than the baseline performance, the unused CPU credits are accrued in the CPU credit balance.
-   If the CPU usage equals the baseline performance, the CPU credit balance remains unchanged.
-   If the CPU usage is higher than the baseline performance, the instance consumes the accrued CPU credits.

## Standard mode {#section_n0v_2ot_yvc .section}

In the standard mode, the performance of a burstable performance instance is governed by the CPU credits it has accrued. If the instance consumes all the credits it has accrued, it cannot burst above the baseline performance. If the CPU credits are insufficient, performance is gradually lowered to the baseline performance level within 15 minutes, so that the instance does not experience reduced performance when its CPU credit balance is used up.

**Note:** For the relationship between instance performance and CPU credits in the standard mode, see [t5 standard instances](reseller.en-US/Instances/Instance type families/Burstable performance instances/t5 standard instances.md#).

A burstable performance instance running in the standard mode is suitable for scenarios where you do not usually, but occasionally require high CPU performance, such as lightweight web servers, development and testing environments, and low or mid-performance databases.

## Unlimited mode {#section_v1t_6rl_7h3 .section}

In the unlimited mode, a burstable performance instance can use advance CPU credits or overdrawn CPU credits to maintain high CPU performance whenever required, without being limited to the baseline CPU performance.

-   Advance CPU credit: CPU credits that are used in advance but should be obtained within the next 24 hours. Advance CPU credits may incur fees. When an unlimited instance runs out of its CPU credit balance, advance CPU credits are used to deliver high CPU performance. When the CPU usage is lower than the baseline performance, the earned CPU credits are used to pay down \(offset\) the advance credits. For more information, see [Impact of performance modes on billing](Impact of performance modes on billingEN-US_TP_21235.dita#concept_abd_vlm_cfb).
-   Overdrawn CPU credit: Additional CPU credits that are used to sustain high CPU usage after advance CPU credits are used up. Overdrawn CPU credits incur additional fees. For more information, see [Impact of performance modes on billing](Impact of performance modes on billingEN-US_TP_21235.dita#concept_abd_vlm_cfb).

The following figure illustrates how the unlimited mode works.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9554/156385392449273_en-US.png)

**Note:** For the relationship between instance performance and CPU credits in the unlimited mode, see [t5 standard instances](reseller.en-US/Instances/Instance type families/Burstable performance instances/t5 standard instances.md#).

The unlimited mode is suitable for the following scenarios:

-   Heavy-load occasions such as launch of new product functions or large-scale promotion on e-commerce platforms. You can enable the unlimited mode in peak hours and disable it in off-peak hours to reduce costs.
-   Some websites experience traffic peaks in specific time periods, but the average CPU usage over a 24-hour period is lower than the baseline performance. You can keep the unlimited mode enabled to ensure use experience in peak hours. If CPU credits accrued in off-peak hours can pay down advance CPU credits, the overall website access experience can be guaranteed without incurring additional fees.

**Note:** By default, the standard mode is used. For information about how to switch to the unlimited mode, see [Manage performance modes of a burstable performance instance](reseller.en-US/Instances/Instance type families/Burstable performance instances/Manage performance modes of a burstable performance instance.md#).

## Create a burstable performance instance {#section_zb0_dkv_xvy .section}

For information about how to create a burstable performance instance, see [ECS instance creation overview](reseller.en-US/Instances/Create an instance/ECS instance creation overview.md#). Note the following setting items when you create a burstable performance instance:

-   Instance type
    1.  Select **x86-Architecture** and **Entry-Level \(Shared\)**.
    2.  Select an appropriate [type of burstable performance instance](#section_mq2_x7y_0jl).
    3.  Select **Enable Unlimited Mode for T5 Instances**. You can also [enable the unlimited mode](reseller.en-US/Instances/Instance type families/Burstable performance instances/Manage performance modes of a burstable performance instance.md#section_cds_zh0_eh7) after instance creation.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9554/156385392446099_en-US.png)

-   Image type: The smallest t5 instance ecs.t5-lc2m1.nano has a memory of 0.5 GiB. It supports only Linux variants or the Windows Server Version 1809 operating system. For more information, see [Select an image](../../../../reseller.en-US/Images/Select an image.md#).
-   Network type: Only **VPC** is supported.

## Change the instance type {#section_al8_1f0_syn .section}

You can replace your current burstable performance instance with other types of burstable performance instances or enterprise-level instances at any time. For more information, see [Instance type families that support instance type upgrades](reseller.en-US/Instances/Change configurations/Instance type families that support instance type upgrades.md#).

The change operations vary according to the billing method:

-   For information about how to change the configuration of a Subscription instance, see [Overview of configuration changes](reseller.en-US/Instances/Change configurations/Overview of configuration changes.md#).
-   For information about how to change the configuration of a Pay-As-You-Go instance, see [Change configurations of Pay-As-You-Go instances](reseller.en-US/Instances/Change configurations/Change configurations of Pay-As-You-Go instances/Change configurations of Pay-As-You-Go instances.md#).

## Basic concepts related to CPU credits {#section_63z_vgu_wsd .section}

|Basic concept|Description|Reference|
|-------------|-----------|---------|
|Launch CPU credit|Each burstable performance instance is allocated 30 launch CPU credits for each vCPU after you create a burstable performance instance.|For more information, see [Earn CPU credits](#section_n3h_act_eb7).|
|CPU credit balance|If a burstable performance instance earns more CPU credits than it consumes, the unused CPU credits are accrued in the CPU credit balance. If a burstable performance instance needs to burst above the baseline performance, it consumes the accrued credits.|For more information, see [Earn CPU credits](#section_n3h_act_eb7).|
|Max. CPU credit balance|The maximum number of credits that an instance can accrue within 24 hours. The CPU credit balance is retained for up to 24 hours to achieve a dynamic balance.|For more information, see [Earn CPU credits](#section_n3h_act_eb7).|
|Advance CPU credit|CPU credits that are used in advance but should be obtained within the next 24 hours. Advance CPU credits can be used only in the unlimited mode.|For more information, see [Unlimited mode](#section_v1t_6rl_7h3).|
|Overdrawn CPU credit|Additional credits required to maintain high performance after the advance CPU credits are used up. Overdrawn CPU credits incur fees and can be used only in the unlimited mode.|For more information, see [Unlimited mode](#section_v1t_6rl_7h3).|

