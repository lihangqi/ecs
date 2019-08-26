# DescribeBandwidthLimitation {#doc_api_1000083 .reference}

Queries a list of bandwidth resources.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=DescribeBandwidthLimitation) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|RegionId|String|Yes|cn-hangzhou| The ID of the region where an instance resides. You can call [DescribeRegions](~~25609~~) to view the latest regions of Alibaba Cloud.

 |
|Action|String|No|DescribeBandwidthLimitation| The operation that you want to perform. Set the value to DescribeBandwidthLimitation.

 |
|InstanceChargeType|String|No|PrePaid| The billing method of the instance. For more information, see [Pricing overview](~~25398~~). Valid values:

 -   PrePaid: the subscription-based billing method.
-   PostPaid: the Pay-As-You-Go billing method.

 Default value: PostPaid.

 |
|InstanceType|String|No|ecs.g5.large| The type of the instance. For more information, see [Instance type families](~~25378~~), or call the[DescribeInstanceTypes](~~25620~~) to query latest instance types.

 |
|OperationType|String|No|Upgrade| Specifies bandwidth operations. Valid values:

 -   Upgrade
-   Downgrade
-   Create

 Default value: Create.

 |
|ResourceId|String|No|s-946ntx4xx| The ID of the resource. When you set the OperationType parameter to Upgrade or Downgrade, the ResourceId parameter is required.

 |
|SpotStrategy|String|No|NoSpot| The spot strategy for a Pay-As-You-Go instance. Valid values:

 -   NoSpot: indicates a regular Pay-As-You-Go instance.
-   SpotWithPriceLimit: indicates a Pay-As-You-Go instance with the maximum hourly price.
-   SpotAsPriceGo: indicates that the system automatically offers a spot hourly price for an instance based on the supply-demand statistics. The spot price is limited to the cost of resources you actually use.

 Default: NoSpot.

 The SpotStrategy parameter is applicable only when the InstanceChargeType parameter is set to PostPaid.

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|Bandwidths| | | The bandwidth types.

 |
|└InternetChargeType|String|PayByTraffic| The bandwidth billing method. Valid values:

 -   PayByBandwidth: You are billed based on the fixed amount of bandwidth.
-   PayByTraffic

 |
|└Max|Integer|100| The maximum bandwidth. No value is returned if the parameter is empty.

 |
|└Min|Integer|0| The minimum bandwidth. No value is returned if the parameter is empty.

 |
|└Unit|String|Mbps| The bandwidth unit. No value is returned if the parameter is empty.

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=DescribeBandwidthLimitation
&RegionId=cn-hangzhou 
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<DescribeBandwidthLimitationResponse>
  <Bandwidths>
    <Bandwidth>
      <InternetChargeType>PayByTraffic</InternetChargeType>
      <Max>100</Max>
      <Min>0</Min>
      <Unit>Mbps</Unit>
    </Bandwidth>
    <Bandwidth>
      <InternetChargeType>PayByTraffic</InternetChargeType>
      <Max>100</Max>
      <Min>0</Min>
      <Unit>Mbps</Unit>
    </Bandwidth>
  </Bandwidths>
  <RequestId>675B6D89-A3EB-4987-BAF3-610591E0D019</RequestId>
</DescribeBandwidthLimitationResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"675B6D89-A3EB-4987-BAF3-610591E0D019",
	" Bandwidths":{
		" Bandwidth":[
			{
				"Max":100,
				"InternetChargeType":"PayByTraffic",
				"Unit":"Mbps",
				"Min":0
			},
			{
				"Max":100,
				"InternetChargeType":"PayByTraffic",
				"Unit":"Mbps",
				"Min":0
			}
		]
	}
}
```

## Error codes {#section_yyl_z7c_bjo .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|400|Invalid.InstanceChargeType|The specified InstanceChargeType is not valid.|The error message returned when the InstanceChargeType parameter is invalid.|
|404|Invalid.NetworkCategory|The specified NetworkCategory is not valid.|The error message returned when the NetworkCategory parameter is invalid.|
|404|Invalid.SpotStrategy|The specified SpotStrategy is not valid.|The error message returned when the SpotStrategy parameter is invalid.|
|404|Invalid.IoOptimized|The specified IoOptimized is not valid.|The error message returned when the IoOptimized parameter is invalid.|
|404|Invalid.ResourceId|The specified ResourceId is not valid.|The error message returned when the resource does not exist in the region or is released.|
|404|Invalid.InstancePayType|The specified InstancePayType is not valid.|The error message returned when the InstancePayType parameter is invalid.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

