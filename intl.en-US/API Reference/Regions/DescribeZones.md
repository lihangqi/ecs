# DescribeZones {#doc_api_Ecs_DescribeZones .reference}

You can call this operation to query zones in a specified region.

## Description {#description .section}

Calling this operation only returns a list of zones and some resource inventory information related to each zone. If you want to query instance types and disk categories that are available for purchase in a zone, we recommend that you call the [DescribeAvailableResource](~~66186~~) operation.

## Debugging {#apiExplorer .section}

Alibaba Cloud provides [OpenAPI Explorer](https://api.aliyun.com/#product=Ecs&api=DescribeZones) to simplify API usage. You can use OpenAPI Explorer to search for APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|RegionId|String|Yes|cn-hangzhou| The ID of the region for which to query zones. You can call the [DescribeRegions](~~25609~~) operation to query the latest region list.

 |
|AcceptLanguage|String|No|zh-CN| The set of supported natural languages. For more information, see [RFC 7231](https://tools.ietf.org/html/rfc7231). Valid values:

 -   zh-CN
-   en-US
-   ja

 Default value: zh-CN

 |
|Action|String|No|DescribeZones| The operation that you want to perform. For API requests using the HTTP and HTTPS methods, `Action` is required. Set the value to DescribeZones.

 |
|InstanceChargeType|String|No|PostPaid| The billing method supported in the zone. For more information, see [Billing overview](~~25398~~). Valid values:

 -   PrePaid: subscription.
-   PostPaid: pay-as-you-go. This is the default value.

 |
|SpotStrategy|String|No|NoSpot| The bidding policy for the pay-as-you-go instance. Specify this parameter when the InstanceChargeType parameter is set to PostPaid. For more information, see [Preemptible instances](~~52088~~). Valid values:

 -   NoSpot: pay-as-you-go instance. This is the default value.
-   SpotWithPriceLimit: preemptible instance with the maximum price
-   SpotAsPriceGo: price automatically provided by the system with the pay-as-you-go instance price as the maximum value

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request.

 |
|Zones| | | An array that consists of ZoneType data.

 |
|AvailableDedicatedHostTypes| |Compute type| The supported types of DDHs. The data type of this parameter is List.

 |
|AvailableDiskCategories| |cloud| A set of supported disk categories. The data type of this parameter is List.

 |
|AvailableInstanceTypes| |c5| The types of the instances that can be created. The data type of this parameter is List.

 |
|AvailableResourceCreation| |DedicatedHost| A set of the types of resources that can be created. The data type of this parameter is List.

 |
|AvailableResources| | | The resources that can be created. This parameter is an array of AvailableResourcesType data.

 |
|DataDiskCategories| |cloud\_ssd| The categories of data disks. The data type of this parameter is List. Valid values:

 -   cloud
-   cloud\_efficiency: ultra disk
-   cloud\_ssd: standard SSD
-   cloud\_essd: enhanced SSD
-   ephemeral\_ssd: local SSD

 |
|InstanceGenerations| |I| The generation number of the instance family. The data type of this parameter is List.

 |
|InstanceTypeFamilies| |\["d1", "d1ne"\]| A list that consists of InstanceTypeFamilyItemType data.

 |
|InstanceTypes| |\["ecs.g5.large"\]| The type of the instance. The data type of this parameter is List.

 |
|IoOptimized|Boolean|true| Indicates whether the instance is I/O optimized. Valid values:

 -   none
-   optimized

 When the InstanceType parameter is [Phased-out instance types](~~55263~~), the default value of the IoOptimized parameter is none.

 For instance types that do not belong to Generation I, the default value is optimized.

 |
|NetworkTypes| |VPC| The type of the network. The data type of this parameter is List. Valid values:

 -   VPC
-   Classic

 |
|SystemDiskCategories| |cloud\_ssd| The category of the system disk. The data type of this parameter is List. Valid values:

 -   cloud
-   cloud\_efficiency: ultra disk
-   cloud\_ssd: standard SSD
-   cloud\_essd: enhanced SSD
-   ephemeral\_ssd: local SSD

 |
|AvailableVolumeCategories| |san\_ssd| The category of available shared storage. The data type of this parameter is List.

 |
|DedicatedHostGenerations| |I| The generation number of DDHs. The data type of this parameter is List.

 |
|LocalName|String|Hangzhou Zone G| The name of the zone in the local language.

 |
|ZoneId|String|cn-hangzhou-b| The ID of the zone.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=DescribeZones
&RegionId=cn-hangzhou
&InstanceChargeType=PostPaid
&SpotStrategy=NoSpot
&<Common request parameters>
```

Sample success responses

`XML` format

``` {#xml_return_success_demo}
<DescribeZonesResponse>
  <Zones>
    <Zone>
      <AvailableResourceCreation>
        <ResourceTypes>Instance</ResourceTypes>
        <ResourceTypes>Disk</ResourceTypes>
      </AvailableResourceCreation>
      <LocalName/>
      <ZoneId>cn-hangzhou-d</ZoneId>
      <AvailableDiskCategories>
        <DiskCategories>cloud</DiskCategories>
      </AvailableDiskCategories>
    </Zone>
    <Zone>
      <AvailableResourceCreation>
        <ResourceTypes>Instance</ResourceTypes>
        <ResourceTypes>Disk</ResourceTypes>
      </AvailableResourceCreation>
      <LocalName/>
      <ZoneId>cn-hangzhou-b</ZoneId>
      <AvailableDiskCategories>
        <DiskCategories>cloud</DiskCategories>
      </AvailableDiskCategories>
    </Zone>
  </Zones>
  <RequestId>6DB97BCC-92BA-424D-A7C8-3F6486612BAE</RequestId>
</DescribeZonesResponse>

```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"A347EF0E-BBCC-4EFA-BD79-27AA3ACFD1BF",
	"Zones":{
		"Zone":[
			{
				"AvailableResourceCreation":{
					"ResourceTypes":[
						"Instance",
						"Disk"
					]
				},
				"ZoneId":"cn-hangzhou-d",
				"LocalName":"",
				"AvailableDiskCategories":{
					"DiskCategories":[
						"cloud"
					]
				}
			},
			{
				"AvailableResourceCreation":{
					"ResourceTypes":[
						"Instance",
						"Disk"
					]
				},
				"ZoneId":"cn-hangzhou-b",
				"LocalName":"",
				"AvailableDiskCategories":{
					"DiskCategories":[
						"cloud"
					]
				}
			}
		]
	}
}
```

## Error codes {#section_37p_094_vwb .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|404|InvalidRegionId.NotFound|The specified RegionId does not exist.|The error message returned because the specified Region ID does not exist. Check whether ECS is available in that region.|
|404|InvalidInstanceChargeType.NotFound|The InstanceChargeType does not exist in our records|The error message returned because the specified instance type does not exist.|
|400|InvalidSpotStrategy|The specified SpotStrategy is not valid.|The error message returned because the specified SpotStrategy parameter is invalid.|
|404|InvalidAcceptLanguage.NotFound|Only Chinese \(zh-CN\), English \(en-US\), and Japanese \(ja\) are allowed.|The error message returned because the specified language is not supported.|

For more information about error codes, visit [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

