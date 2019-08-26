# RI overview {#concept_tc4_zhq_dgb .concept}

A Reserved Instance \(RI\) is a discount coupon with specific attributes. It can automatically match one or more Pay-As-You-Go instances \(excluding preemptible instances\) in your account to provide a billing discount. Compared with Subscription instances, the combination of RIs and Pay-As-You-Go instances provides higher flexibility and cost-effectiveness.

## Feature release {#section_sfs_frg_vgb .section}

## Comparison of RIs against Subscription and Pay-As-You-Go instances {#section_qv2_nlq_dgb .section}

The following table compares RIs with Subscription and Pay-As-You-Go instances.

|Item|RI|Pay-As-You-Go instance|Subscription instance|
|----|--|----------------------|---------------------|
|Definition|A type of discount coupon.|An instance with the [Pay-As-You-Go](../../../../reseller.en-US/Pricing/Pay-As-You-Go.md#) billing method, equivalent to a virtual machine.|An instance with the [Subscription](../../../../reseller.en-US/Pricing/Subscription.md#) billing method, equivalent to a virtual machine.|
|Usage|RIs cannot be used alone. Instead, they must match instances with specific attributes to generate a billing discount.|Pay-As-You-Go instances can be managed independently. They can be used as simple Web servers, or be combined with other Alibaba Cloud products to deliver powerful solutions.|Subscription instances can be managed independently. They can be used as simple Web servers, or be combined with other Alibaba Cloud products to deliver powerful solutions.|

## Payment methods, term, and instance count {#section_mrf_33q_dgb .section}

When you purchase an RI, you can specify the payment method, term, and instance count based on your budget.

-   Three payment methods are available:

    All Upfront, Partial Upfront, and No Upfront. For more information, see [Reserved Instance billing](../../../../reseller.en-US/Pricing/Billing of Reserved Instances.md#).

    **Note:** Whether you can use the No Upfront payment method is determined by your ECS instance resource usage.

-   Two terms are available:

    1 year and 3 years.

    **Note:** After an RI expires, the matched Pay-As-You-Go instances will still operate normally, but they will be billed without a discount.

-   Instance count:

    The instance count refers to the number of Pay-As-You-Go instances that can be matched by an RI at the same time.


## Attributes {#section_b3l_w3q_dgb .section}

An RI has specific attributes that automatically match the corresponding Pay-As-You-Go instances. You can also split an RI, merge multiple RIs, or change the scope of an RI. In this way, your RIs can flexibly match your Pay-As-You-Go instances. The attributes include:

-   Operating system: Currently, RIs can only match Pay-As-You-Go Linux instances.
-   Instance type: The type of an RI, which indicates the instance type family and the instance size. This attribute is used to match the corresponding Pay-As-You-Go instances.
-   Scope: This attribute indicates the matching scope of an RI. Depending on the matching scope, RIs can be classified into regional RIs and zonal RIs.

    **Note:** We recommend that you purchase both zonal RIs and regional RIs to meet all of your requirements. In detail, zonal RIs apply when you are certain of the zone in which you want to use it. If you are uncertain about the specific use of your RI, we recommend that you use a regional RI to meet your wider needs.

-   Computational power: This attribute indicates the upper limit of computational resources that an RI matches. The computational power is determined by the instance type and the instance count.

## Limits {#section_iym_jpq_dgb .section}

Currently, RIs have the following limits:

-   Number of RIs

    -   Number of regional RIs: Each account can have up to 20 regional RIs in all regions.
    -   Number of zonal RIs: Each account can have up to 20 zonal RIs in each zone.
    For example, in China \(Hangzhou\) and China \(Qingdao\), you can purchase 10 regional RIs respectively because the upper limit of regional RIs is 20 per account. In zones B and H of China \(Hangzhou\), you can purchase up to 20 zonal RIs respectively. If you need more RIs, you can open a ticket.

-   Matchable instances: RIs only match Pay-As-You-Go instances \(excluding [preemptible instances](../../../../reseller.en-US/Instances/Instance purchasing options/Preemptible instances/Preemptible instances.md#)\).
-   Instance type family: Currently, RIs support the following instance type families: sn1ne, sn2ne, se1ne, ic5, c5, g5, r5, hfc5, hfg5, and t5. For more information, see [Instance type families](reseller.en-US/Instances/Instance type families.md#).

    **Note:** The RIs of [burstable performance instances](../../../../reseller.en-US/Instances/Instance type families/Burstable performance instances/Basic concepts.md#) are only available at the zonal level. Additionally, they do not support merging, splitting, or scope changing.


## Fees {#section_exj_yvw_dhb .section}

For more information about RI billing, see [Reserved Instance billing](../../../../reseller.en-US/Pricing/Billing of Reserved Instances.md#).

## References {#section_aj4_hc2_ggb .section}

For the matching rules, see [Matching rules of Reserved Instances](reseller.en-US/Instances/Instance purchasing options/Reserved Instances/Matching rules of Reserved Instances.md#).

For purchasing operations, see [Purchase a Reserved Instance](reseller.en-US/Instances/Instance purchasing options/Reserved Instances/Purchase a Reserved Instance.md#).

For managing operations, see [Manage Reserved Instances flexibly](reseller.en-US/Instances/Instance purchasing options/Reserved Instances/Manage Reserved Instances.md#).

For information on how to use an API to purchase an RI, see [PurchaseReservedInstancesOffering](reseller.en-US/API Reference/Reserved Instances/PurchaseReservedInstancesOffering.md#).

For information on how to use an API to query RIs, see [DescribeReservedInstances](reseller.en-US/API Reference/Reserved Instances/DescribeReservedInstances.md#).

For information on how to use an API to manage RIs, see [ModifyReservedInstances](reseller.en-US/API Reference/Reserved Instances/ModifyReservedInstances.md#).

## Contact us {#section_xfs_sdz_3hb .section}

If you have any questions when you use RIs, you can scan the following QR code to join the [DingTalk](https://tms.dingtalk.com/markets/dingtalk/download) Reserved Instances Service Group for technical support.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/80437/156375925043499_en-US.png)

