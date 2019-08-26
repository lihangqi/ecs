# ModifyReservedInstances {#concept_i5h_kgn_cgb .concept}

You can call ModifyReservedInstances to modify Reserved Instances \(RIs\).

## Precautions {#section_llg_xtg_cgb .section}

Before you change RIs, note the following:

-   The region of an RI cannot be changed. You can only change the zone of an RI, change region-level RIs to zone-level RIs, or change zone-level RIs to region-level RIs.
-   The instance type family of an RI cannot be modified. Only the size of an RI can be modified.
-   If the RIs to be merged are region-level RIs, they must be in the same region. If the RIs to be merged are zone-level RIs, they must be in the same zone.
-   The RIs to be merged must have the same expiration date.
-   After an RI is split or multiple RIs are merged, the initial RI or RIs will expire immediately.

## Request parameters {#section_chl_15g_cgb .section}

|Name|Type|Required|Description|
|----|----|--------|-----------|
|Action|String|Yes|A parameter required by the system. Value: ModifyReservedInstances.|
|RegionId|String|Yes|ID of the region to which the RI belongs. You can call [DescribeRegions](reseller.en-US/API Reference/Regions/DescribeRegions.md#) to view the latest region list.|
|ReservedInstanceId.N|String|Yes|ID of the RI. N is an integer from 1 to 20.|
|Configuration.N|Configuration|Yes|Configuration attribute of the target RI|
|DryRun|Boolean|No|Specifies whether to check this request only.-   true: A check request is sent, but no instance is created. The system checks whether the required parameters are set, and also checks the request format, service limits, and available ECS instances. If the request does not pass the check, an error is returned. If the request passes the check, the error code `DryRunOperation` is returned.
-   false: A check request is sent, and an instance is created after the request passes the check.

Default value: false.

|

The following table describes the parameters of the Configuration data type.

|Name|Type|Required|Description|
|----|----|--------|-----------|
|ReservedInstanceName|String|No|Name of the RI. The name must be a string of 2 to 128 characters in length and can contain letters, numbers, colons \(:\), underscores \(\_\), and hyphens. It must start with a letter. It cannot start with http:// or https://.|
|InstanceType|String|Yes|Instance type of the RI. For more information, see [Instance type families](../../../../../reseller.en-US/Instances/Instance type families/Instance type families.md#).|
|Scope|String|Yes|Scope of the RI. Optional values:-   Region: region-level
-   Zone: zone-level

Default value: Region.

|
|ZoneId|String|No|ID of the zone to which the RI belongs. When Scope is set to Zone, this parameter is required. For information about the zone list, see [DescribeZones](reseller.en-US/API Reference/Regions/DescribeRegions.md#).|
|InstanceAmount|Integer|Yes|Number of instances allocated to an RI \(An RI is a coupon that includes one or more allocated instances.\)|

## Response parameters {#section_m5l_fql_cgb .section}

|Name|Type|Description|
|----|----|-----------|
|RequestId|String|Request ID|
|ReservedInstanceIdSets|List|List of RI IDs. The IDs in the list are the unique identities to access the RIs.|

