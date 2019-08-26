# DescribeInstanceMonitorData {#doc_api_Ecs_DescribeInstanceMonitorData .reference}

调用DescribeInstanceMonitorData查询一台 ECS 实例所有相关的监控信息。返回的监控内容包括 ECS 实例的 CPU 使用率、接收的数据流量、发送的数据流量、网络流量、平均带宽。当返回信息中缺少部分内容时，可能是由于系统没有获取到相应的信息，比如当时实例处于已停止（Stopped）状态。

## 接口说明 {#description .section}

调用该接口时，您需要注意：

-   每次最多返回 400 条监控数据，如果指定的参数 \(EndTime - StartTime\)/Peroid \> 400 时，则返回错误。
-   单次最多能查询近 30 天内的监控信息，如果指定的参数 StartTime 超过 30 天，则返回错误。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=DescribeInstanceMonitorData)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|EndTime|String|是|2014-10-30T08:00:00Z|获取数据的结束时间点。按照 [ISO8601](~~25696~~) 标准表示，并需要使用 UTC 时间，格式为：YYYY-MM-DDThh:mm:ssZ。 如果指定的秒（ss）不是 00，则自动换算为下一分钟。

 |
|InstanceId|String|是|i-instnace1|待查询的实例 ID。

 |
|StartTime|String|是|2014-10-29T23:00:00Z|获取数据的起始时间点。按照 [ISO8601](~~25696~~) 表示，并需要使用 UTC 时间，格式为：YYYY-MM-DDThh:mm:ssZ。如果指定的秒（ss）不是 00，则自动换算为下一分钟。

 |
|Action|String|否|DescribeInstanceMonitorData|系统规定参数。取值：DescribeInstanceMonitorData

 |
|Period|Integer|否|60|获取监控数据的间隔时间，单位为秒。取值范围：

 -   60
-   600
-   3600

 默认值：60

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|MonitorData| | |实例的监控数据集合。

 |
|BPSRead|Integer|1000|实例系统盘读带宽，单位：Byte/s。

 |
|BPSWrite|Integer|200|实例系统盘写带宽，单位：Byte/s。

 |
|CPU|Integer|2|实例 vCPU 的使用比例，单位：百分比（%）。

 |
|CPUAdvanceCreditBalance|Float|0.4|超额积分（t5实例积分超限部分）。

 |
|CPUCreditBalance|Float|120|突发性能（t5）实例积分总数。

 |
|CPUCreditUsage|Float|30|突发性能（t5）实例已使用的积分数。

 |
|CPUNotpaidSurplusCreditUsage|Float|0.5|超额未支付积分。

 |
|IOPSRead|Integer|1000|实例系统盘 I/O 读操作，单位：次/s。

 |
|IOPSWrite|Integer|200|实例系统盘 I/O 写操作，单位：次/s。

 |
|InstanceId|String|i-instnace1|实例ID。

 |
|InternetBandwidth|Integer|10|实例的公网带宽，单位时间内的网络流量，单位：kbits/s。

 |
|InternetRX|Integer|122|实例在 TimeStamp 时刻接收的公网数据流量，单位：kbits。

 |
|InternetTX|Integer|343|实例在 TimeStamp 时刻发送的公网数据流量，单位：kbits。

 |
|IntranetBandwidth|Integer|10|实例的内网带宽，单位时间内的网络流量，单位：kbits/s。

 |
|IntranetRX|Integer|122|实例在 TimeStamp 时刻接收的内网数据流量，单位：kbits。

 |
|IntranetTX|Integer|343|实例在 TimeStamp 时刻发送的内网数据流量，单位：kbits。

 |
|TimeStamp|String|2010-01-21T09:50:23Z|查询监控信息的时间戳。按照 [ISO8601](~~25696~~) 标准表示，并需要使用UTC时间，格式为yyyy-MM-ddTHH:mm:ssZ。

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=DescribeInstanceMonitorData
&EndTime=2014-10-30T08:00:00Z
&InstanceId=i-instnace1
&StartTime=2014-10-29T23:00:00Z
&Period=60
&<公共请求参数>
```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeInstanceMonitorDataResponse>
  <RequestId>C8B26B44-0189-443E-9816-D951F59623A9</RequestId>
  <MonitorData>
    <InstanceMonitorData>
      <InstanceId>i-Bc0102-23xYm**</InstanceId>
      <CPU>2</CPU>
      <IntranetRX>122</IntranetRX>
      <IntranetTX>343</IntranetTX>
      <IntranetFlow>675</IntranetFlow>
      <IntranetBandwidth>10</IntranetBandwidth>
      <InternetRX>122</InternetRX>
      <InternetTX>343</InternetTX>
      <InternetFlow>675</InternetFlow>
      <InternetBandwidth>10</InternetBandwidth>
      <IOPSRead>1000</IOPSRead>
      <IOPSWrite>200</IOPSWrite>
      <BPSRead>1000</BPSRead>
      <BPSWrite>200</BPSWrite>
      <TimeStamp>2010-01-21T09:50:23Z</TimeStamp>
    </InstanceMonitorData>
  </MonitorData>
</DescribeInstanceMonitorDataResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"C8B26B44-0189-443E-9816-D951F59623A9",
	"MonitorData":{
		"InstanceMonitorData":[
			{
				"IOPSRead":1000,
				"BPSWrite":200,
				"IntranetBandwidth":10,
				"IntranetTX":343,
				"IntranetRX":122,
				"InstanceId":"i-Bc0102-23xYm**",
				"InternetFlow":675,
				"CPU":0,
				"TimeStamp":"2010-01-21T09:50:23Z",
				"BPSRead":1000,
				"InternetRX":122,
				"IntranetFlow":675,
				"InternetBandwidth":10,
				"IOPSWrite":200,
				"InternetTX":343
			}
		]
	}
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|404|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|指定的实例不存在，请您检查实例ID是否正确。|
|400|InvalidStartTime.Malformed|The specified parameter "StartTime" is not valid.|指定的开始时间格式不合法。|
|400|InvalidEndTime.Malformed|The specified parameter "EndTime" is not valid.|指定的结束时间格式不合法。|
|400|InvalidPeriod.ValueNotSupported|The specified parameter "Period" is not valid.|指定的 Period 参数不合法。|
|400|InvalidStartTime.TooEarly|The specified parameter "StartTime" is too early.|指定的开始时间太早。|
|400|InvalidParameter.TooManyDataQueried|Too many data queried.|监控数据节点超出范围。|
|400|Throttling|Request was denied due to request throttling.|当前的操作太过频繁，请稍后重试。|
|400|InvalidStartTime.ValueNotSupported|The specified parameter StartTime is later than EndTime.|结束时间不得早于开始时间。|
|500|InternalError|The request processing has failed due to some unknown error.|内部错误，请重试。如果多次尝试失败，请提交工单|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

