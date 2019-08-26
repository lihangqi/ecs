# DescribeAvailableResource {#DescribeAvailableResource .reference}

Describes a list of the resources available in a certain zone. For example, you can retrieve the resource list in a zone before creating an ECS instance \([RunInstances](intl.en-US/API Reference/Instances/RunInstances.md#)\) in the zone.

## Description {#section_av1_byg_ydb .section}

When you call this interface, consider the following:

-   If you do not specify the `ZondId`parameter, the system returns resources that match the other criteria in all zones in the \(`RegionId`\) region.
-   You can specify the `DestinationResource` parameter to retrieve different types of resource lists, and specify other parameters to refine your search. Options for the DestinationResource `DestinationResource` parameter have dependencies. When you select an option, the options to the left of the option in the chain are also required.
    -   Sequence: \(`Zone`\) \> `IoOptimized` \> `InstanceType` \> `SystemDisk` \> `Datadisk`
    -   **Samples of parameter values in the sequence**:
        -   If you set `DestinationResource` to  `SystemDisk`, you must specify the `IoOptimized` and `InstanceType`.
        -   If you set `DestinationResource` to `InstanceType`, you must specify the `IoOptimized`.
        -   If you set `DestinationResource` to `DataDisk`, you must specify the `IoOptimized`, `InstanceType`, and `SystemDiskCategory`.

## Request parameters {#RequestParameter .section}

|Name|Type|Required|Description |
|:---|:---|:-------|:-----------|
|Action|String|Yes|The name of this interface. Value: DescribeAvailableResource.|
|RegionId|String|Yes|ID of the target region. You can call [DescribeRegions](intl.en-US/API Reference/Regions/DescribeRegions.md#) to obtain the latest region list.|
|DestinationResource|String|Yes|Resource type to query.  Optional values:-   Zone: Zone.
-   IoOptimized: Whether the instance is I/O optimized or not.
-   InstanceType: Instance type.
-   SystemDisk: System disk of an instance.
-   DataDisk: Data disk of an instance.
-   Network: Network type of an instance.

|
|ZoneId|String|No|Zone ID. If you do not specify `ZoneId`, the system returns resources that match the other criteria in all zones throughout the current region.|
|InstanceChargeType |String|No|Billing method of resources. For more information, see [Pricing overview](../../../../intl.en-US/Pricing/Pricing overview.md#). Optional values:-   PrePaid: Subscription.
-   PostPaid: Pay-As-You-Go.

Default value: PostPaid.|
|SpotStrategy|String|No|Sets your expected spot price for preemptible instances. Optional values:-   NoSpot: Bids as a normal Pay-As-You-Go instance.
-   SpotWithPriceLimit: Sets a bidding price threshold for the preemptible instance.
-   SpotAsPriceGo: Sets a highest Pay-As-You-Go price by the bidding system automatically.

Default: NoSpot. The `InstanceChargeType` must be set to `PostPaid` to make `SpotStrategy` valid.|
|IoOptimized|String|No|Whether it is an I/O-optimized instance or not. Optional values:-   none: Non-I/O optimized instance.
-   optimized: I/O optimized instance.

If you set `DestinationResource` to  `InstanceType`, `SystemDisk` or `DataDisk`, you must specify `IoOptimized` as well.|
|InstanceType|String|No|Instance type. For more information, see [Instance Type Family](../../../../intl.en-US/Product Introduction/Instance type families.md#), or call [DescribeInstanceTypes](intl.en-US/API Reference/Instances/DescribeInstanceTypes.md#) to obtain the latest type list. If you set `DestinationResource` to `SystemDisk` or `DataDisk`, you must specify the `InstanceType`.|
|Systemdiskcategory|String|No|System disk category. Optional values:-   Cloud: Basic cloud disk.
-   cloud\_efficiency: Ultra cloud disk.
-   cloud\_ssd: Cloud SSD.
-   ephemeral\_ssd: Ephemeral SSD

|
|Datadiskcategory|String|No|Data disk category. Optional values:-   Cloud: Basic cloud disk.
-   cloud\_efficiency: Ultra cloud disk.
-   cloud\_ssd: Cloud SSD.
-   ephemeral\_ssd: Ephemeral SSD

|
|NetworkCategory|String|No|Network type of an ECS instance. Optional values:-   Vpc: Virtual Private Cloud.
-   Classic: Classic network.

|

## Response parameters {#ResponseParameter .section}

|Name|Type|Description|
|:---|:---|:----------|
|AvailableZones|Array of [AvailableZoneType](#AvailableZoneType)|A collection of zone types|

**AvailableZoneType**

|Name|Type|Description|
|:---|:---|:----------|
|RegionId|String|Region ID.|
|ZoneId|String|Zone ID.|
|Status|String|Resource status. Possible values:-   Available: Resources are available.
-   SoldOut: Resources are unavailable.

|
|AvailableResources|Array of [AvailableResourcesType](#AvailableResourcesType)|A collection of available resource types.|

**AvailableResourcesType**

|Name|Type|Description|
|:---|:---|:----------|
|Type|String|The type of the ECS resource. Possible values:-   Zone: Zone.
-   IoOptimized: Whether the instance is I/O optimized or not.
-   InstanceType: Instance type.
-   SystemDisk: System disk.
-   DataDisk: Data disk of an instance.
-   Network: Network type of an instance.

|
|SupportedResources|Array of [SupportedResourcesType](#SupportedResourcesType)|A collection of supported available resource types.|

**SupportedResourcesType**

|Name|Type|Description|
|:---|:---|:----------|
|Value|String|Name of the Resource.|
|Status|String|Resource status. Possible values:-   Available: Resources are available.
-   SoldOut: Resources are unavailable.

|
|Min|Integer|Minimum limit of a resource type. No value is returned if the parameter is null.|
|Max|Integer|Maximum limit of a resource type. No value is returned if the parameter is null.|
|Unit|Integer|Resource type unit. No value is returned if the parameter is null.|

## Examples { .section}

**Request example** 

```
https://ecs.aliyuncs.com/?Action=DescribeAvailableResource
&RegionId=cn-hangzhou
&<Common Request Parameters>
```

**Response example** 

**XML format**

```
<DescribeAvailableResourceResponse>
    <AvailableZones>
        <AvailableZone>
            <ZoneId>cn-hangzhou-d</ZoneId>
            <RegionId>cn-hangzhou</RegionId>
            <Status>Available</Status>
            <AvailableResources>
                <AvailableResource>
                    <Type>instanceType</Type>
                    <SupportedResources>
                        <SupportedResource>
                            <Value>ecs.d1ne.xlarge</Value>
                            <Status>Available</Status>
                        </SupportedResource>
                        <SupportedResource>
                            <Value>ecs.d1ne. 2xlarge</Value>
                            <Status>Available</Status>
                        </SupportedResource>
                    </SupportedResources>
                </AvailableResource>
            </AvailableResources>
        </AvailableZone>
        <AvailableZone>
            <ZoneId>cn-hangzhou-e</ZoneId>
            <RegionId>cn-hangzhou</RegionId>
            <Status>Available</Status>
            <AvailableResources>
                <AvailableResource>
                    <Type>instanceType</Type>
                    <SupportedResources>
                        <SupportedResource>
                            <Value>ecs.d1ne.xlarge</Value>
                            <Status>Available</Status>
                        </SupportedResource>
                         <SupportedResource>
                            <Value>ecs.d1ne. 2xlarge</Value>
                            <Status>Available</Status>
                        </SupportedResource>
                    </SupportedResources>
                </AvailableResource>
            </AvailableResources>
        </AvailableZone>
    </AvailableZones>
    <RequestId>6DB97BCC-92BA-424D-A7C8-3F6486612BAE</RequestId>
</DescribeAvailableResourceResponse>
```

 **JSON format** 

```
{
    "RequestId": "D0233A65-7F00-4B50-8023-101427229D4F",
    "AvailableZones": {
        "AvailableZone": [
            {
                "Status": "available",
                "RegionId": "cn-hangzhou",
                "AvailableResources": {
                    "AvailableResource": [
                        {
                            "Type": "instanceType",
                            "SupportedResources": {
                                "SupportedResource": [
                                    {
                                        "Status": "available",
                                        "Value": "ecs.sn1ne.xlarge"
                                    },
                                    {
                                        "Status": "available",
                                        "Value": "ecs.sn2ne.xlarge"
                                    }
                                ]
                            }
                        }
                    ]
                },
                "ZoneId": "cn-hangzhou-e",
            }
        ]
    }
}
```

## Error codes {#ErrorCode .section}

Error codes specific to this interface are as follows. For more information, see [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

|Error code|Error messages|HTTP status code |Meaning|
|:---------|:-------------|:----------------|:------|
|Invalid.Param|The input parameter DestinationResource that is mandatory for processing this request is not supplied.|400|You must specify the `DestinationResource`.|
|Invalid.InstanceChargeType|The specified InstanceChargeType is not valid.|400|The specified `InstanceChargeType` does not exist.|
|Invalid.IoOptimized|The specified IoOptimized is not valid.|404|The specified parameter `IoOptimized` is invalid.|
|Invalid.NetworkCategory|The specified NetworkCategory is not valid.|404|The specified NetworkCategory is invalid.|
|InvalidRegionId.NotFound|The specified RegionId does not exist.|404|The specified `RegionId` does not exist.|
|Unavailable.Regions|The available regions does not exists.|404|You are not allowed to access the specified `RegionId`.|

