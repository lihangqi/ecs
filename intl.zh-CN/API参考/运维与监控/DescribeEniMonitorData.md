# DescribeEniMonitorData {#doc_api_1006116 .reference}

查询一块辅助网卡在指定时间段内使用的流量信息。

## 描述 {#description .section}

可查询的辅助网卡流量信息包括辅助网卡收发数据包的数量、内网出入流量、辅助网卡收发丢包的数量。当返回信息中缺少部分内容时，可能是由于系统没有获取到相应的信息。例如，当时实例处于已停止（Stopped）状态或者辅助网卡没有挂载到实例上，即处于可用（Available）状态。调用该接口时，您需要注意：

-   每次最多返回400条监控数据，即，如果指定的参数\(EndTime - StartTime\)/Peroid\>400时，则返回错误。
-   单次最多能查询近30天内的监控信息，如果指定的参数StartTime超过30天，则返回错误。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=DescribeEniMonitorData)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|EndTime|String|是|2018-05-21T12:22:00Z|获取数据的结束时间点。按照 [ISO8601](~~25696~~) 标准表示，并需要使用UTC时间，格式为yyyy-MM-ddTHH:mm:ssZ。如果指定的秒（ss）不是00，则自动换算为下一分钟。

 |
|InstanceId|String|是|myInstance|辅助网卡绑定的实例ID。

 |
|RegionId|String|是|cn-hangzhou|地域ID。您可以调用 [DescribeRegions](~~25609~~) 查看最新的阿里云地域列表。

 |
|StartTime|String|是|2018-05-21T12:19:00Z|获取数据的起始时间点。按照 [ISO8601](~~25696~~) 标准表示，并需要使用UTC时间，格式为yyyy-MM-ddTHH:mm:ssZ。如果指定的秒（ss）不是00，则自动换算为下一分钟。

 |
|Action|String|否|DescribeEniMonitorData|系统规定参数。取值：DescribeEniMonitorData

 |
|EniId|String|否|eni-myENI|辅助网卡的ID。默认查询指定实例上所有已绑定的辅助网卡。

 |
|OwnerAccount|String|否|ECSforCloud@Alibaba.com|RAM 用户的账号登录名称。

 |
|Period|Integer|否|60|获取监控数据的间隔时间，单位：秒。取值范围：

 -   60
-   600
-   3600

 默认值：60

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|MonitorData| | |辅助网卡流量的监控数据EniMonitorDataType组成的集合。

 |
|└DropPacketRx|String|0|辅助网卡接收丢弃的内网数据包，单位：packets。

 |
|└DropPacketTx|String|0|辅助网卡发送丢弃的内网数据包，单位：packets。

 |
|└EniId|String|eni-myENI|辅助网卡ID。

 |
|└IntranetRx|String|0|辅助网卡接收的内网数据流量，单位：kbits。

 |
|└IntranetTx|String|0|辅助网卡发送的内网数据流量，单位：kbits。

 |
|└PacketRx|String|0|辅助网卡接收的内网数据包，单位：packets。

 |
|└PacketTx|String|0|辅助网卡发送的内网数据包，单位：packets。

 |
|└TimeStamp|String|2018-05-21T03:22:00Z|查询监控信息的时间戳。按照 [ISO8601](~~25696~~) 标准表示，并需要使用UTC时间，格式为yyyy-MM-ddTHH:mm:ssZ。

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。

 |
|TotalCount|Integer|4|返回条目数量。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

https://ecs.aliyuncs.com/?Action=DescribeEniMonitorData
&EndTime=2018-05-21T12:22:00Z
&InstanceId=myInstance
&RegionId=cn-hangzhou
&StartTime=2018-05-21T12:19:00Z
&EniId=eni-myENI
&Period=60
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeEniMonitorDataResponse>
  <RequestId>5A03C2BA-3BCE-4A87-8076-7DC1629</RequestId>
  <TotalCount>4</TotalCount>
  <MonitorData>
    <EniMonitorData>
      <PacketTx>0</PacketTx>
      <TimeStamp>2018-05-21T03:22:00Z</TimeStamp>
      <IntranetOut>0</IntranetOut>
      <DropPacketRx>0</DropPacketRx>
      <IntranetIn>0</IntranetIn>
      <EniId>eni-myENI</EniId>
      <DropPacketTx>0</DropPacketTx>
      <PacketRx>0</PacketRx>
    </EniMonitorData>
    <EniMonitorData>
      <PacketTx>0</PacketTx>
      <TimeStamp>2018-05-21T03:21:00Z</TimeStamp>
      <IntranetOut>0</IntranetOut>
      <DropPacketRx>0</DropPacketRx>
      <IntranetIn>0</IntranetIn>
      <EniId>eni-myENI</EniId>
      <DropPacketTx>0</DropPacketTx>
      <PacketRx>0</PacketRx>
    </EniMonitorData>
    <EniMonitorData>
      <PacketTx>52240</PacketTx>
      <TimeStamp>2018-05-21T03:19:00Z</TimeStamp>
      <IntranetOut>73344</IntranetOut>
      <DropPacketRx>0</DropPacketRx>
      <IntranetIn>467</IntranetIn>
      <EniId>eni-myENI</EniId>
      <DropPacketTx>0</DropPacketTx>
      <PacketRx>6603</PacketRx>
    </EniMonitorData>
    <EniMonitorData>
      <PacketTx>34925</PacketTx>
      <TimeStamp>2018-05-21T03:20:00Z</TimeStamp>
      <IntranetOut>48871</IntranetOut>
      <DropPacketRx>0</DropPacketRx>
      <IntranetIn>350</IntranetIn>
      <EniId>eni-myENI</EniId>
      <DropPacketTx>0</DropPacketTx>
      <PacketRx>4888</PacketRx>
    </EniMonitorData>
  </MonitorData>
</DescribeEniMonitorDataResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"5A03C2BA-3BCE-4A87-8076-7DC1629",
	"MonitorData":{
		"EniMonitorData":[
			{
				"TimeStamp":"2018-05-21T03:22:00Z",
				"PacketTx":0,
				"IntranetOut":0,
				"DropPacketRx":0,
				"EniId":"eni-myENI",
				"IntranetIn":0,
				"PacketRx":0,
				"DropPacketTx":0
			},
			{
				"TimeStamp":"2018-05-21T03:21:00Z",
				"PacketTx":0,
				"IntranetOut":0,
				"DropPacketRx":0,
				"EniId":"eni-myENI",
				"IntranetIn":0,
				"PacketRx":0,
				"DropPacketTx":0
			},
			{
				"TimeStamp":"2018-05-21T03:19:00Z",
				"PacketTx":52240,
				"IntranetOut":73344,
				"DropPacketRx":0,
				"EniId":"eni-myENI",
				"IntranetIn":467,
				"PacketRx":6603,
				"DropPacketTx":0
			},
			{
				"TimeStamp":"2018-05-21T03:20:00Z",
				"PacketTx":34925,
				"IntranetOut":48871,
				"DropPacketRx":0,
				"EniId":"eni-myENI",
				"IntranetIn":350,
				"PacketRx":4888,
				"DropPacketTx":0
			}
		]
	}
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|403|InvalidInstanceType.NotSupportCredit|The InstanceType of the specified instance does not support credit.|实例规格不支持突发性能实例。|
|403|InvalidParameter.EndTime|The specified parameter EndTime is earlier than StartTime.|结束时间不得早于开始时间。|
|4,003|InvalidParam.Malformed|The specified parameter "EniId" and "InstanceId" are not valid|指定的参数无效。|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Ecs)

