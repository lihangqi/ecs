# DescribeAvailableResource {#doc_api_Ecs_DescribeAvailableResource .reference}

You can call this operation to query resources in a zone. For example, you can query resources before creating an ECS instance \(RunInstances\) or modifying instance specifications \(ModifyInstanceSpec\) in a zone.

## Description {#description .section}

When you call this operation, note that:

-   When the ZoneId parameter is not specified, the system returns the resources that match the other criteria of all zones within the region.
-   You can specify the DestinationResource parameter to retrieve different types of resources, and specify other parameters to refine your search. Options for the DestinationResource parameter have dependencies. When you select an option in the following chain, the options to the left of this option are all required.
    -   Sequence: \(Zone\) \> IoOptimized \> InstanceType \> SystemDisk \> DataDisk
    -   For example:
        -   If you set the DestinationResource parameter to SystemDisk, you must specify the IoOptimized and InstanceType parameters.
        -   If you set the DestinationResource parameter to InstanceType, you must specify the IoOptimized parameter.
        -   If you set the DestinationResource parameter to DataDisk, you must specify the IoOptimized, InstanceType, and SystemDiskCategory parameters.

## Debugging {#apiExplorer .section}

Alibaba Cloud provides [OpenAPI Explorer](https://api.aliyun.com/#product=Ecs&api=DescribeAvailableResource) to simplify API usage. You can use OpenAPI Explorer to search for APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|DestinationResource|String|Yes|InstanceType|The resource types to be queried. Valid values:

 -   Zone
-   IoOptimized
-   InstanceType
-   SystemDisk
-   DataDisk
-   Network

 |
|RegionId|String|Yes|cn-hangzhou|The ID of the region for which to query resources. You can call the [DescribeRegions](~~25609~~) operation to query the latest region list.

 |
|Action|String|No|DescribeAvailableResource|The operation that you want to perform. For API requests using the HTTP and HTTPS methods, `Action` is required. Set the value to DescribeAvailableResource.

 |
|Cores|Integer|No|2|The number of vCPU cores of the instance type. For more information, see [Instance type families](~~25378~~).

 The Cores parameter is valid only when the DestinationResource parameter is set to InstanceType.

 |
|DataDiskCategory|String|No|cloud\_ssd|The category of the data disk. Valid values:

 -   cloud
-   cloud\_efficiency: ultra disk
-   cloud\_ssd: standard SSD
-   ephemeral\_ssd: local SSD
-   cloud\_essd: enhanced SSD

 |
|DedicatedHostId|String|No|dh-dedicatedhostid|The ID of the DDH.

 |
|InstanceChargeType|String|No|PrePaid|The billing method of resources. For more information, see [Billing overview](~~25398~~). Valid values:

 -   PrePaid: subscription
-   PostPaid: pay-as-you-go

 Default value: PostPaid

 |
|InstanceType|String|No|ecs.g5.large|The type of the instance. For more information, see [Instance type families](~~25378~~) or call the [DescribeInstanceTypes](~~25620~~) operation to query the latest instance type list.

 When the DestinationResource parameter is set to SystemDisk or DataDisk, the InstanceType parameter is required.

 |
|IoOptimized|String|No|optimized|Specifies whether the instance is I/O optimized. Valid values:

 -   none
-   optimized

 When the DestinationResource parameter is set to InstanceType, SystemDisk, or DataDisk, the IoOptimized parameter is required. Default value: optimized.

 |
|Memory|Float|No|8.0|The memory size of the instance type. Unit: GiB. For more information, see [Instance type families](~~25378~~).

 The Memory parameter is valid only when the DestinationResource parameter is set to InstanceType.

 |
|NetworkCategory|String|No|vpc|The type of the network. Valid values:

 -   vpc
-   classic

 |
|ResourceType|String|No|Instance|The type of the resource. Valid values:

 -   instance
-   disk
-   reservedinstance
-   ddh

 |
|SpotStrategy|String|No|NoSpot|The bidding policy for the pay-as-you-go instance. Valid values:

 -   NoSpot: pay-as-you-go instance
-   SpotWithPriceLimit: preemptible instance with the maximum price
-   SpotAsPriceGo: price automatically provided by the system with the pay-as-you-go instance price as the maximum value

 Default value: NoSpot

 The SpotStrategy parameter is valid only when the InstanceChargeType parameter is set to PostPaid.

 |
|SystemDiskCategory|String|No|cloud\_ssd|The category of the system disk. Valid values:

 -   cloud
-   cloud\_efficiency: ultra disk
-   cloud\_ssd: standard SSD
-   ephemeral\_ssd: local SSD
-   cloud\_essd: enhanced SSD

 When the DestinationResource parameter is set to SystemDisk, InstanceType, or DataDisk, the SystemDiskCategory parameter is optional. Default value: cloud\_efficiency.

 |
|ZoneId|String|No|cn-hangzhou-e|The ID of the zone for which to query resources.

 When the ZoneId parameter is not specified, the system returns resources that match the other criteria of all zones within the region.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|AvailableZones| | |An array of zone types.

 |
|└AvailableResources| | |An array of available resource types.

 |
|└SupportedResources| | |An array of supported resource types.

 |
|└Max|Integer|2|The maximum number of resources of a specific type that can be created. No value is returned when this parameter is null.

 |
|└Min|Integer|1|The minimum value of resources of a specific type that can be created. No value is returned when the parameter is null.

 |
|└Status|String|Available|The type of the resource. Valid values:

 -   Available
-   SoldOut

 |
|└StatusCategory|String|WithStock|The resource category based on the stock. Valid values:

 -   WithStock: sufficient stock
-   ClosedWithStock: insufficient stock
-   WithoutStock: running out of stock

 |
|└Unit|String|null|The unit of the resource type. No value is returned when the parameter is null.

 |
|└Value|String|ecs.d1ne.xlarge|The value of the resource.

 |
|└Type|String|InstanceType|The type of the resource. Valid values:

 -   Zone
-   IoOptimized
-   InstanceType
-   SystemDisk
-   DataDisk
-   Network

 |
|└RegionId|String|cn-hangzhou|The ID of the region.

 |
|└Status|String|Available|The type of the resource. Valid values:

 -   Available
-   SoldOut

 |
|└StatusCategory|String|WithStock|The resource category based on the stock. Valid values:

 -   WithStock: sufficient stock
-   ClosedWithStock: insufficient stock
-   WithoutStock: running out of stock

 |
|└ZoneId|String|cn-hangzhou-e|The ID of the zone.

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=DescribeAvailableResource
&DestinationResource=InstanceType
&RegionId=cn-hangzhou
&InstanceChargeType=PrePaid
&SpotStrategy=NoSpot
&ZoneId=cn-hangzhou-e
&IoOptimized=optimized
&DedicatedHostId=dh-dedicatedhostid
&InstanceType="ecs.g5.large"
&SystemDiskCategory=cloud_ssd
&DataDiskCategory=cloud_ssd
&NetworkCategory=vpc
&Cores=2
&Memory=8.0
&ResourceType=Instance
&<Common request parameters>
```

Sample success responses

`XML` format

``` {#xml_return_success_demo}
<DescribeAvailableResourceResponse>
  <RequestId>5272B7D8-F366-4781-AF7B-63E735FBC09A</RequestId>
  <AvailableZones>
    <AvailableZone>
      <Status>Available</Status>
      <RegionId>cn-hangzhou</RegionId>
      <ZoneId>cn-hangzhou-h</ZoneId>
    </AvailableZone>
    <AvailableZone>
      <Status>Available</Status>
      <RegionId>cn-hangzhou</RegionId>
      <ZoneId>cn-hangzhou-g</ZoneId>
    </AvailableZone>
    <AvailableZone>
      <Status>Available</Status>
      <RegionId>cn-hangzhou</RegionId>
      <ZoneId>cn-hangzhou-f</ZoneId>
    </AvailableZone>
    <AvailableZone>
      <Status>Available</Status>
      <RegionId>cn-hangzhou</RegionId>
      <ZoneId>cn-hangzhou-b</ZoneId>
    </AvailableZone>
    <AvailableZone>
      <Status>Available</Status>
      <RegionId>cn-hangzhou</RegionId>
      <ZoneId>cn-hangzhou-e</ZoneId>
    </AvailableZone>
  </AvailableZones>
</DescribeAvailableResourceResponse>

```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"5272B7D8-F366-4781-AF7B-63E735FBC09A",
	"AvailableZones":{
		"AvailableZone":[
			{
				"Status":"Available",
				"RegionId":"cn-hangzhou",
				"ZoneId":"cn-hangzhou-h"
			},
			{
				"Status":"Available",
				"RegionId":"cn-hangzhou",
				"ZoneId":"cn-hangzhou-g"
			},
			{
				"Status":"Available",
				"RegionId":"cn-hangzhou",
				"ZoneId":"cn-hangzhou-f"
			},
			{
				"Status":"Available",
				"RegionId":"cn-hangzhou",
				"ZoneId":"cn-hangzhou-b"
			},
			{
				"Status":"Available",
				"RegionId":"cn-hangzhou",
				"ZoneId":"cn-hangzhou-e"
			}
		]
	}
}
```

## Error codes { .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|404|Invalid.RegionId|The specified RegionId does not exist.|The error message returned because the specified RegionId parameter is invalid.|
|404|Unavailable.Regions|The available regions does not exists|The error message returned because the specified RegionId parameter is invalid.|
|400|Invalid.InstanceChargeType|The specified InstanceChargeType is not valid.|The error message returned because the specified InstanceChargeType parameter is invalid.|
|400|Invalid.Param|The input parameter DestinationResource that is mandatory for processing this request is not supplied.|The error message returned because the specified DestinationResource parameter is invalid.|
|404|Invalid.ResourceType|The ResourceType provided does not exist in our records.|The error message returned because the specified ResourceType parameter is invalid.|
|404|Invalid.DestinationResource|The specified DestinationResource is not valid.|The error message returned because the specified DestinationResource parameter is invalid.|
|404|Invalid.IoOptimized|The specified IoOptimized is not valid.|The error message returned because the specified IoOptimized parameter is invalid.|
|404|Invalid.NetworkCategory|The specified NetworkCategory is not valid.|The error message returned because the specified NetworkCategory parameter is invalid.|
|404|Invalid.SpotStrategy|The specified SpotStrategy is not valid.|The error message returned because the specified SpotStrategy parameter is invalid.|
|403|InvalidDedicatedHostId.NotFound|The specified DedicatedHostId does not exist.|The error message returned because the specified DDH ID does not exist.|
|404|Invalid.NetworkType|The specified NetworkType is not valid.|The error message returned because the specified NetworkType parameter is invalid.|
|404|InvalidResourceId.NotFound|The specified ResourceId is not found in our records|The error message returned because the specified ResourceId parameter is invalid.|
|403|InvalidParam.TypeAndCpuMem.Conflict|The specified 'InstanceType' and 'Cores','Memory' are not blank at the same time.|The error message returned because the specified InstanceType, Cores, and Memory parameters conflict with each other.|
|403|InvalidParam.Cores|The specified parameter 'Cores' should be empty|The error message returned because the specified Cores parameter is invalid.|
|403|InvalidParam.Memory|The specified parameter 'Memory' should be empty|The error message returned because the specified Memory parameter is invalid.|
|400|InvalidRegionId.MalFormed|The specified parameter RegionId is not valid.|The error message returned because the specified RegionId parameter is invalid.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

