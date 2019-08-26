# Auto provisioning overview {#concept_287169 .concept}

Auto provisioning is a service to quickly deploy an instance cluster comprised of preemptible and pay-as-you-go instances. Auto provisioning supports one-click deployment of instance clusters with specified billing methods, zones, and instance families. Auto provisioning uses auto provisioning groups to schedule and maintain computing resources. You can use auto provisioning groups to provide stable computing power. This alleviates the instability caused by the reclaiming of preemptible instances, and avoids the repeated cumbersome process of manually creating instances.

## Introduction to auto provisioning groups {#section_94r_j3i_wpq .section}

[Preemptible instances](intl.en-US/Instances/Instance purchasing options/Preemptible instances/Preemptible instances.md#) are low-cost computing resources that are subject to a protection period of one hour. After the protection period expires, preemptible instances and their resources may be reclaimed. You need to pay attention to the availability of preemptible instances in the next hour after the protection period. If they are unavailable, you need to create new ones. As the number of preemptible instances increases, the maintenance time also increases. In this scenario, you can use auto provisioning groups to deploy instance clusters based on a configured target capacity and scheduling policy.

Similar to preemptible instances, auto provisioning groups are applicable to stateless application scenarios such as scalable website services, image rendering, big data analytics, and parallel computing. Auto provisioning groups support flexible policy combinations to alleviate the impact of reclaimed preemptible instances. In addition, the delivery of instance clusters is convenient.

Auto provisioning automatically selects instance types and creates the instance cluster. You do not need to calculate the cost of instances individually. If you select **Continuous Delivery and Maintain Capacity**, the auto provisioning group automatically compares real-time and target capacities. When preemptible instances are reclaimed, the auto provisioning group selects instance types and then creates new instances to maintain the target capacity that meets business needs at the largest extent and meet your computing power needs at the lowest cost.

Auto provisioning groups can create instance clusters to meet computing power needs based on configured instances types and scheduling policies.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/236159/156173410248772_en-US.png)

## Features {#section_cl8_rql_ybf .section}

-   Cross billing methods

    Preemptible instances provide computing resources at a low cost, but are restricted by the reclaim mechanism and available inventory in a region. Pay-as-you-go instances can be created and released at any time. These instances have a guaranteed inventory, but are much more costly compared to preemptible instances. Auto provisioning groups allow you to create both preemptible instances and pay-as-you-go instances. You can use both billing methods to reduce costs and meet your computing power needs.

-   Cross zones

    Deploying an instance cluster in the same zone reduces network latency between instances, while deploying an instance cluster across zones improves the disaster recovery capabilities of applications. Auto provisioning groups support deployment of instance clusters across zones. You can set zone options as needed.

-   Cross instance families

    Auto provisioning groups allow you to specify alternative instance types across multiple families to provide a range of instance types to select from. Additionally, you can specify the weight and priority for each instance type to improve task scheduling while ensuring controllability.

-   Flexible policy combinations

    Auto provisioning groups can meet various dynamic business needs through combinations of target capacities and scale-out policies. Auto provisioning groups allow you to set the target capacities of clusters, preemptible instances, and pay-as-you-go instances, and to specify scaling policies for preemptible instances and pay-as-you-go instances. Additionally, you can specify solutions to fulfill the target capacity of the cluster when preemptible and pay-as-you-go instances are insufficient.

-   Complete cost control

    Auto provisioning groups allow you to set a maximum price for global and individual instance types to ensure costs remain within your expectations.

-   Practical protection mechanism

    Auto provisioning groups provide the shutdown option. You can enable this option when an auto provisioning group expires or when instances exceed the target capacity. Routine health checks are performed on instances in an auto provisioning group to ensure instances are available.


## Billing {#section_azd_6d0_ot4 .section}

Auto provisioning is free to use. However, instance resources created through auto provisioning will incur charges. For more information on billing, see [Preemptible instance](intl.en-US/Instances/Instance purchasing options/Preemptible instances/Preemptible instances.md#section_mdc_jt5_ydb) and [Pay-as-you-go](../../../../intl.en-US/Pricing/Pay-As-You-Go.md#).

## Limits {#section_86p_9iz_my1 .section}

-   Auto provisioning groups cannot schedule resources across regions.
-   A maximum of 1,000 instances can be created under each auto provisioning group.
-   Only one launch template can be specified for each auto provisioning group. However, you can extend the launch template to implement more configurations. For more information, see [Template configurations](intl.en-US/Instances/Manage auto provisioning groups/Create an auto provisioning group.md#table_8v9_xkp_gha).

