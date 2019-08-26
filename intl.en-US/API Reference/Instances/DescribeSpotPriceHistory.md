# DescribeSpotPriceHistory {#doc_api_1161581 .reference}

Queries the price history of the last 30 days for a preemptible instance.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=DescribeSpotPriceHistory) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|InstanceType|String|Yes|ecs.t1.xsmall| The type of the instance.

 |
|NetworkType|String|Yes|VPC| The network type of the preemptible instance. Valid values:

 -   classic.
-   vpc.

 |
|RegionId|String|Yes|cn-hangzhou| The region ID of the instance. You can call the [DescribeRegions](~~25609~~) operation to view the latest region list.

 |
|Action|String|No|DescribeSpotPriceHistory| The operation that you want to perform. Set the value to DescribeSpotPriceHistory.

 |
|EndTime|String|No|2017-08-22T08:45:08Z| The end time of the query. The time follows the [ISO 8601](~~25696~~) standard and is in UTC time. Format: yyyy-MM-ddTHH:mm:ssZ.

 Default value: null. If this parameter is empty, the current time is used.

 |
|IoOptimized|String|No|none| Specifies whether the instance is an I/O optimized instance. Valid values:

 -   optimized.
-   none.

 Default value: none for generation I instances,

 optimized for generations II and III instances.

 |
|OSType|String|No|Linux| The type of the operating system platform.

 |
|Offset|Integer|No|0| The start row of the query.

 Default value: 0

 |
|StartTime|String|No|2017-08-22T08:45:08Z| The start time of the query. The time follows the [ISO 8601](~~25696~~) standard and is in UTC time. Format: yyyy-MM-ddTHH:mm:ssZ.

 Default value: null. If this parameter is empty, the start time is defined as three days before the specified EndTime. You can specify a StartTime value of up to 30 days before the specified EndTime.

 |
|ZoneId|String|No|cn-hangzhou-g| The zone ID of the instance.

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|Currency|String|CNY| The currency unit of the price.

 |
|NextOffset|Integer|1000| The start row of the next page. It is the value of **Offset**.

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The request ID.

 |
|SpotPrices| | | The details of the price.

 |
|└InstanceType|String|ecs.t1.xsmall| The instance type.

 |
|└IoOptimized|String|none| Indicates whether it is an optimized instance.

 |
|└NetworkType|String|PayByTraffic| The network type of the preemptible instance.

 |
|└OriginPrice|Float|0.028| The original price of the Pay-As-You-Go instance.

 |
|└SpotPrice|Float|0.006| The spot price of the preemptible instance.

 |
|└Timestamp|String|2017-09-18T11:00:00Z| The time for the price. Format: yyyy-MM-ddTHH:MM:SS.

 |
|└ZoneId|String|cn-hangzhou-c| The zone ID of the preemptible instance.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=DescribeSpotPriceHistory
&NetworkType=vpc 
&RegionId=cn-hangzhou 
&InstanceType=ecs.t1.xsmall 
&IoOptimized=none 
&Offset=0 
&StartTime=2017-08-22T08:45:08Z
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<DescribeSpotPriceHistoryResponse>
  <RequestId>xxxxxxxxxxxxxx</RequestId>
  <NextOffset>1000</NextOffset>
  <SpotPrices>
    <SpotPriceType>
      <IoOptimized>none</IoOptimized>
      <OriginPrice>0.028</OriginPrice>
      <NetworkType>classic</NetworkType>
      <Timestamp>2017-09-18T11:00:00Z</Timestamp>
      <ZoneId>cn-hangzhou-c</ZoneId>
      <SpotPrice>0.006</SpotPrice>
      <InstanceType>ecs.t1.xsmall</InstanceType> 
    </SpotPriceType>
    <SpotPriceType>
      <IoOptimized>none</IoOptimized>
      <OriginPrice>0.028</OriginPrice>
      <NetworkType>classic<NetworkType>
      <Timestamp>2017-09-18T12:00:00Z</Timestamp>
      <ZoneId>cn-hangzhou-c</ZoneId>
      <SpotPrice>0.006</SpotPrice>
      <InstanceType>ecs.t1.xsmall</InstanceType> 
    </SpotPriceType>
  </SpotPrices>
</DescribeSpotPriceHistoryResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"xxxxxxxxxxxxxx",
	"SpotPrices":{
		"SpotPriceType":[
			{
				"IoOptimized":"none",
				"NetworkType":"classic",
				"OriginPrice":0.028,
				"ZoneId":"cn-hangzhou-c",
				"Timestamp":"2017-09-18T11:00:00Z",
				"InstanceType":"ecs.t1.xsmall",
				"SpotPrice":0.006
			}
		]
	},
	"NextOffset":1000
}
```

## Error codes { .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|403|InvalidUserType.NotSupported|%s|The error message returned when your account type is not supported.|
|403|Abs.InvalidAccount.NotFound|%s|The error message returned when your Alibaba Cloud account does not exist or your AccessKey is expired.|
|400|MissingParameter|%s|The error message returned when a required parameter is not specified.|
|403|Forbidden.NotSupportRAM|%s|The error message returned when RAM users are not allowed to perform this operation.|
|403|Forbidden.SubUser|%s|The error message returned when RAM users are not allowed to perform this operation.|
|400|InvalidParameter|%s|The error message returned when the parameter format is incorrect.|
|400|InvalidInstanceId.MalFormed|%s|The error message returned when the instance ID format is incorrect.|
|400|InvalidParams.StartTime|%s|The error message returned when the StartTime format is incorrect.|
|400|InvalidParams.EndTime|%s|The error message returned when the EndTime format is incorrect.|
|400|Abs.Abs.InvalidSpotInstanceUID|%s|The error message returned when the preemptible instance ID format is incorrect.|
|400|InvalidParams.NetworkType|%s|The error message returned when the network type of the instance is incorrect.|
|400|InvalidParams.IoOptimized|%s|The error message returned when the IoOptimized parameter of the instance is incorrect.|
|400|InvalidParams.OSType|%s|The error message returned when the OSType parameter of the instance is incorrect.|
|400|Abs.IoOptimized.ValueNotSupported|%s|The error message returned when the IoOptimized parameter of the instance is incorrect.|
|400|InvalidParams.ZoneId|%s|The error message returned when the ZoneId parameter of the instance is incorrect.|
|400|InvalidParams.RegionId|%s|The error message returned when the RegionId parameter of the instance is incorrect.|
|400|InvalidParams.InstanceType|%s|The error message returned when the InstanceType parameter is incorrect.|
|400|InvalidParams.PageSize|%s|The error message returned when the PageSize parameter of the instance is incorrect.|
|400|InvalidParams.Offset|%s|The error message returned when the Offset parameter of the instance is incorrect.|
|400|InvalidInstanceType.ValueNotSupported|%s|The error message returned when the InstanceType parameter is incorrect.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

