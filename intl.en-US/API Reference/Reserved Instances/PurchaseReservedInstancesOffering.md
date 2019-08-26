# PurchaseReservedInstancesOffering {#concept_gtw_ygg_cgb .concept}

After you purchase Pay-As-You-Go instances, you can use PurchaseReservedInstancesOffering to purchase Reserved Instances \(RIs\) so that you can benefit from billing discounts.

## Description {#section_llg_xtg_cgb .section}

Before you purchase RIs, you can call [DescribeAvailableResource](reseller.en-US/API Reference/Regions/DescribeAvailableResource.md#) to query available instance resources.

We recommend that you read [Reserved Instance billing methods](../../../../../reseller.en-US/Pricing/Reserved Instance billing.md#) before you purchase RIs to learn more about the billing methods applied.

## Request parameters {#section_chl_15g_cgb .section}

|Name|Type|Required|Description|
|----|----|--------|-----------|
|Action|String|Yes|A parameter required by the system. Value: PurchaseReservedInstancesOffering.|
|RegionId|String|Yes|ID of the region to which the RI belongs. You can call [DescribeRegions](reseller.en-US/API Reference/Regions/DescribeRegions.md#) to view the latest region list.|
|Scope|String|Yes|Scope of the RI. Optional values:-   Region: region-level
-   Zone: zone-level

Default value: Region.

|
|ZoneId|String|No|ID of the zone to which the RI belongs. When Scope is set to Zone, this parameter is required. For information about the zone list, see [DescribeZones](reseller.en-US/API Reference/Regions/DescribeZones.md#).|
|ReservedInstanceName|String|No|Name of the RI. The name must be a string of 2 to 128 characters in length and can contain letters, numbers, colons \(:\), underscores \(\_\), and hyphens. It must start with a letter. It cannot start with http:// or https://.|
|InstanceType|String|Yes|Instance type of the RI. For more information, see [Instance type families](../../../../../reseller.en-US/Instances/Instance type families/Instance type families.md#).|
|InstanceAmount|Integer|Yes|Number of instances allocated to an RI \(An RI is a coupon that includes one or more allocated instances.\)|
|OfferingType|String|Yes|Payment type of the RI. Optional values:-   No Upfront: No upfront payment is required.
-   Partial Upfront: A portion of upfront payment is required.
-   All Upfront: Full upfront payment is required.

|
|Period|Integer|Yes|Term of the RI. Unit: years. Optional values: 1 and 3.|
|PeriodUnit|String|Yes|Term unit. Optional value: Year.|

## Response parameters {#section_m5l_fql_cgb .section}

|Name|Type|Description|
|----|----|-----------|
|ReservedInstanceId|String|ID of the RI. The ID is the unique identity to access the RI.|

## Examples {#section_gfv_hbm_cgb .section}

Request example

```
https://ecs.aliyuncs.com/?Action=PurchaseReservedInstancesOffering
&RegionId=cn-hangzhou
&Scope=Zone
&ZoneId=cn-hangzhou-a
&ReservedInstanceName=test
&InstanceType=ecs.g5.2xlarge
&InstanceAmount=1
&OfferingType=All Upfront
&Period=1
&PeriodUnit=Year
&<Common request parameters>
```

Response example

`XML` format

```
<PurchaseReservedInstancesOfferingResponse>
    <RequestId>51AB7717-6E1A-4D1D-A44D-54CBxxxxxxxx</RequestId>
    <ReservedInstanceId>ri-instance</InstanceId>
</PurchaseReservedInstancesOfferingResponse>
```

`JSON` format

```
{
    "RequestId": "51AB7717-6E1A-4D1D-A44D-54CBxxxxxxxx",
    "ReservedInstanceId":"ri-instance"
}
```

