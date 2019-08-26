# DescribeSpotPriceHistory {#doc_api_1161581 .reference}

查询抢占式实例近 30 天内的历史价格。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=DescribeSpotPriceHistory)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|InstanceType|String|是|ecs.t1.xsmall| 实例规格。

 |
|NetworkType|String|是|vpc| 抢占式实例网络类型。取值范围：

 -   classic：表示抢占式实例的网络类型为经典网络
-   vpc：表示抢占式实例的网络类型为专有网络

 |
|RegionId|String|是|cn-hangzhou| 实例所属的地域 ID。您可以调用 [DescribeRegions](~~25609~~) 查看最新的阿里云地域列表。

 |
|Action|String|否|DescribeSpotPriceHistory| 系统规定参数。取值：DescribeSpotPriceHistory

 |
|EndTime|String|否|2017-08-22T08:45:08Z| 查询抢占式实例历史价格的结束时间。按照 [ISO8601](~~25696~~) 标准表示，并需要使用 UTC 时间。格式为：yyyy-MM-ddTHH:mm:ssZ。

 默认为空，空表示当前时间。

 |
|IoOptimized|String|否|none| 是否为 I/O 优化实例。取值范围：

 -   optimized：表示抢占式实例为 I/O 优化实例
-   none：表示抢占式实例为非 I/O 优化实例

 系列 I 实例默认值：none

 系列 II 实例默认值：optimized系列 III 实例默认值：optimized

 |
|OSType|String|否|linux| 操作系统的发行平台类型。

 |
|Offset|Integer|否|0| 查询开始行。

 默认值：0

 |
|OwnerAccount|String|否|ECSforCloud@Alibaba.com| RAM用户的账号登录名称。

 |
|StartTime|String|否|2017-08-22T08:45:08Z| 查询抢占式实例历史价格的起始时间。按照 [ISO8601](~~25696~~) 标准表示，并需要使用 UTC 时间。格式为：yyyy-MM-ddTHH:mm:ssZ。

 默认为空，空代表结束时间前 3 天，最大值不得超过指定的结束时间 30 天。

 |
|ZoneId|String|否|cn-hangzhou-g| 可用区 ID。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|Currency|String|CNY| 价格的货币单位。

 |
|NextOffset|Integer|1000| 下一页开始行，查询下一页的数据。参数 **Offset** 的指定值为该值。

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| 请求 ID。无论调用接口成功与否，我们都会返回请求 ID。

 |
|SpotPrices| | | 抢占价格详情

 |
|└InstanceType|String|ecs.t1.xsmall| 抢占式实例的实例规格

 |
|└IoOptimized|String|none| 抢占式实例是否为 I/O 优化实例

 |
|└NetworkType|String|PayByTraffic| 抢占式实例的网络类型

 |
|└OriginPrice|Float|0.028| 按量付费实例部分原价

 |
|└SpotPrice|Float|0.006| 抢占式实例价格

 |
|└Timestamp|String|2017-09-18T11:00:00Z| 时间格式为 yyyy-MM-ddTHH:MM:SS 的价格时间

 |
|└ZoneId|String|cn-hangzhou-c| 抢占式实例所属的可用区 ID

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

https://ecs.aliyuncs.com/?Action=DescribeSpotPriceHistory
&NetworkType=vpc
&RegionId=cn-hangzhou
&InstanceType=ecs.t1.xsmall
&IoOptimized=none
&Offset=0
&StartTime=2017-08-22T08:45:08Z
&<公共请求参数>

```

正常返回示例

`XML` 格式

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
      <NetworkType>classic</NetworkType>
      <Timestamp>2017-09-18T12:00:00Z</Timestamp>
      <ZoneId>cn-hangzhou-c</ZoneId>
      <SpotPrice>0.006</SpotPrice>
      <InstanceType>ecs.t1.xsmall</InstanceType>
    </SpotPriceType>
  </SpotPrices>
</DescribeSpotPriceHistoryResponse>

```

`JSON` 格式

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

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|403|InvalidUserType.NotSupported|%s|此操作暂不支持您的账号类型。|
|403|Abs.InvalidAccount.NotFound|%s|您的阿里云账号不存在，或者您的AccessKey已经过期。|
|400|MissingParameter|%s|缺失必需参数。|
|403|Forbedden.NotSupportRAM|%s|暂不支持 RAM 用户执行该操作。|
|403|Forbbiden.SubUser|%s|暂不支持 RAM 用户执行该操作。|
|400|InvalidParameter|%s|参数格式不正确。|
|400|InvalidInstanceID.Malformed|%s|实例 ID 格式不正确。|
|400|InvalidParams.StartTime|%s|开始时间格式不正确。|
|400|InvalidParams.EndTime|%s|结束时间格式不正确。|
|400|Abs.Abs.InvalidSpotInstanceUID|%s|抢占式实例ID格式不正确。|
|400|InvalidParams.NetworkType|%s|实例网络类型不正确。|
|400|InvalidParams.IoOptimized|%s|实例I/O优化属性不正确。|
|400|InvalidParams.OSType|%s|实例OSType属性不正确。|
|400|Abs.IoOptimized.ValueNotSupported|%s|实例I/O优化属性不正确。|
|400|InvalidParams.ZoneId|%s|zoneId属性不正确。|
|400|InvalidParams.RegionId|%s|regionId属性不正确。|
|400|InvalidParams.InstanceType|%s|instanceType属性不正确。|
|400|InvalidParams.PageSize|%s|分页pageSize属性不正确。|
|400|InvalidParams.Offset|%s|分页offset属性不正确。|
|400|InvalidInstanceType.ValueNotSupported|%s|实例类型属性不正确。|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Ecs)

