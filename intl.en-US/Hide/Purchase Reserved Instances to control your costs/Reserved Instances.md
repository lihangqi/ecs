# Reserved Instances {#concept_tc4_zhq_dgb .concept}

A Reserved Instance \(RI\) is a reservation of specific instance resources. It provides a billing discount to the use of relevant Pay-As-You-Go instances \(excluding preemptible instances\) in your account. Compared with Subscription instances, the combination of Reserved Instances and Pay-As-You-Go instances allows for flexibility and cost-effectiveness.

## RIs vs. Subscription and Pay-As-You-Go instances {#section_qv2_nlq_dgb .section}

The following table compares Reserved Instances with Subscription and Pay-As-You-Go instances.

|Item|Reserved Instance|Pay-As-You-Go instance|Subscription instance|
|----|-----------------|----------------------|---------------------|
|Definition|A reservation of instance resources.|An instance with the [Pay-As-You-Go](../../../../../reseller.en-US/Pricing/Pay-As-You-Go.md#) billing method.|An instance with the [Subscription](../../../../../reseller.en-US/Pricing/Subscription.md#) billing method.|
|Usage|Cannot be used alone. RIs need to match instances with relevant attributes to generate a billing discount.|Can be managed independently. You can use it as a simple Web server, or combine it with other Alibaba Cloud products to deliver powerful solutions.|Can be managed independently. You can use it as a simple Web server, or combine it with other Alibaba Cloud products to deliver powerful solutions.|

## Payment options, reservation term, and the number of instances whose attributes are matched {#section_mrf_33q_dgb .section}

When you purchase Reserved Instances, you can determine the payment options, reservation terms, and the number of instances whose attributes are matched according to your budget.

-   Three payment options are available:

    All Upfront, Partial Upfront, and No Upfront. For more information, see [Reserved Instance Billing](../../../../../reseller.en-US/Hide/Purchase Reserved Instances to control your costs/Reserved Instance billing.md#).

-   Two reservation terms are available:

    One-year and three-year.

    **Note:** After a Reserved Instance expires, you can continue using the relevant instances without interruption, but you are charged Pay-As-You-Go rates. In other words, billing discount is no longer available.

-   Number of matching instances:

    The number of Pay-As-You-Go instances whose attributes are matched by a Reserved Instance.


## Attributes {#section_b3l_w3q_dgb .section}

A Reserved Instance has specific attributes that automatically match the corresponding Pay-As-You-Go instances. You can also manage the existing Reserved Instances by splitting or merging them, or adjusting their scope. In this way, they can flexibly match the attributes of Pay-As-You-Go instances of other types. The attributes include:

-   Operating system: Currently, Reserved Instances only match the attributes of Pay-As-You-Go Linux instances.
-   Instance type: This is composed of the instance type family and the instance size \(large or small\), and is used to match the attributes of corresponding Pay-As-You-Go instances.
-   Scope: This determines whether the Reserved Instances apply to a region or zone.

    **Note:** We recommend that you select zonal Reserved Instances based on your demands, coupled with regional Reserved Instances to meet any temporary needs.

-   Computational power: The upper limit of computational resources of the instances with the attributes that a Reserved Instance matches. It is determined by the instance type and the number of instances whose attributes are matched.

## Limitations {#section_iym_jpq_dgb .section}

Currently, the Reserved Instance has the following limitations:

-   Number of Reserved Instances: Each account can have up to 20 valid Reserved Instances. You can combine regional and zonal Reserved Instances, but the total number of them must not exceed 20.

    For example, in China East 1 \(Hangzhou\), you can purchase 10 regional Reserved Instances, and then in both zones B and H you can purchase five zonal Reserved Instances, but the total must not exceed 20. If you need more Reserved Instances, you can open a ticket.

-   Instance type: Reserved Instances only match Pay-As-You-Go instances \(excluding [preemptible instances](../../../../../reseller.en-US/Product Introduction/Instances/Preemptible instance.md#)\).
-   Instance type family: Currently, Reserved Instances support the following instance type families: sn1ne, sn2ne, se1ne, ic5, c5, g5, r5, hfc5, hfg5, and t5. For more information, see [Instance type family](reseller.en-US/Product Introduction/Instance type families.md#).

    **Note:** Of them, the Reserved Instances of [burstable instances](../../../../../reseller.en-US/Product Introduction/Instances/Burstable instances/Basic concepts.md#) \(t5\) are only available at the zonal level, and do not support merging, splitting or adjusting the scope.


## References {#section_aj4_hc2_ggb .section}

For billing information, see [Reserved Instance billing](../../../../../reseller.en-US/Hide/Purchase Reserved Instances to control your costs/Reserved Instance billing.md#).

For the matching rules and common operations, see [Overview of Reserved Instances](../../../../../reseller.en-US/Hide/Purchase Reserved Instances to control your costs/Overview of Reserved Instances.md#).

For purchasing operations, see [Purchase a Reserved Instance](reseller.en-US/Hide/Purchase Reserved Instances to control your costs/Purchase a Reserved Instance.md#).

For managing operations, see [Manage Reserved Instances flexibly](reseller.en-US/Hide/Purchase Reserved Instances to control your costs/Manage Reserved Instances flexibly.md#).

For information on how to use an API to purchase a Reserved Instance, see [PurchaseReservedInstancesOffering](reseller.en-US/Hide/Purchase Reserved Instances to control your costs/PurchaseReservedInstancesOffering.md#).

For information on how to use an API to query Reserved Instances, see [DescribeReservedInstances](reseller.en-US/Hide/Purchase Reserved Instances to control your costs/DescribeReservedInstances.md#).

For information on how to use an API to modify Reserved Instances, see [ModifyReservedInstances](reseller.en-US/Hide/Purchase Reserved Instances to control your costs/ModifyReservedInstances.md#).

