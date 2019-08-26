# DescribeDisksFullStatus {#doc_api_1063476 .reference}

查询一块或多块磁盘的全部状态信息。

## 描述 {#description .section}

-   磁盘的全部状态信息包含磁盘生命周期（Status），磁盘健康状态（HealthStatus）和磁盘事件类型（EventType）。
-   由于磁盘相关事件的发布时间、事件的计划执行时间以及事件的实际执行时间相同，如果指定一段时间 EventTime.Start~EventTime.End，则可以查询这段时间中发生过的所有历史事件。目前，您最多可以查询最近一周的历史事件。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=DescribeDisksFullStatus)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|RegionId|String|是|cn-hangzhou|磁盘所在地域ID。您可以调用 [DescribeRegions](~~25609~~) 查看最新的阿里云地域列表。

 |
|Action|String|否|DescribeDisksFullStatus|系统规定参数。取值：DescribeDisksFullStatus

 |
|DiskId.N|RepeatList|否|d-disk1|磁盘ID，N的取值范围：1~100。

 |
|EventId.N|RepeatList|否|e-event1|事件ID，N的取值范围：1~100。

 |
|EventTime.End|String|否|2018-05-08T02:48:52Z|查询事件发生时间的结束时间。按照 [ISO8601](~~25696~~) 标准表示，并需要使用UTC时间，格式为yyyy-MM-ddTHH:mm:ssZ。

 |
|EventTime.Start|String|否|2018-05-06T02:43:10Z|查询事件发生时间的开始时间。按照 [ISO8601](~~25696~~) 标准表示，并需要使用UTC时间，格式为yyyy-MM-ddTHH:mm:ssZ。

 |
|EventType|String|否|Stalled|指定磁盘的事件类型。取值范围：

 -   Degraded：磁盘性能降级
-   SeverelyDegraded：磁盘性能严重降级
-   Stalled：磁盘性能受到严重影响

 |
|HealthStatus|String|否|Warning|指定磁盘的健康状态。取值范围：

 -   Impaired：暂时性不可读写
-   Warning：服务降级
-   Initializing：初始化中
-   InsufficientData：数据不足
-   NotApplicable：不适用

 |
|OwnerAccount|String|否|ECSforCloud@Alibaba.com|RAM 用户的账号登录名称。

 |
|PageNumber|Integer|否|1|查询结果的页码。取值范围：正整数

 默认值：1

 |
|PageSize|Integer|否|10|查询结果的分页大小。取值范围：1~100

 默认值：10

 |
|Status|String|否|Available|指定磁盘的生命周期状态，参阅 [云盘状态表](~~25689~~)。取值范围：

 -   In\_use：使用中
-   Available：待挂载
-   Attaching：挂载中
-   Detaching：卸载中
-   Creating：创建中
-   ReIniting：初始化中

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|DiskFullStatusSet| | |磁盘全状态数组。

 |
|└Device|String|/dev/xvdb|磁盘挂载于实例上的设备名，例如 /dev/xvdb。只有在Status为In\_use时才有值，其他状态为空。

 |
|└DiskEventSet| | |磁盘事件数组。

 |
|└EventEndTime|String|2018-05-06T02:48:52Z|事件结束时间。

 |
|└EventId|String|e-event1|磁盘事件ID。

 |
|└EventTime|String|2018-05-08T02:43:10Z|事件发生时间。

 |
|└EventType| | |事件类型。

 |
|└Code|Integer|7|事件类型代码。

 |
|└Name|String|Stalled|事件类型名称。

 |
|└DiskId|String|d-disk1|磁盘ID。

 |
|└HealthStatus| | |磁盘健康状态。

 |
|└Code|Integer|128|磁盘健康状态代码。

 |
|└Name|String|Impaired|磁盘健康状态名称。

 |
|└InstanceId|String|i-instance1|实例ID。

 |
|└Status| | |磁盘生命周期状态。

 |
|└Code|Integer|129|磁盘生命周期状态代码。

 |
|└Name|String|Available|磁盘生命周期状态名称。

 |
|PageNumber|Integer|1|ECS实例列表页码。

 |
|PageSize|Integer|10|每页大小。

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。

 |
|TotalCount|Integer|2|ECS实例状态总个数。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

https://ecs.aliyuncs.com/?Action=DescribeDisksFullStatus
&RegionId=cn-hangzhou
&DiskId.1=d-disk1
&EventId.1=e-event1
&Status=Available
&HealthStatus=Warning
&EventType=Stalled
&EventTime.Start=2018-05-06T02:43:10Z
&EventTime.End=2018-05-08T02:48:52Z
&PageNumber=1
&PageSize=10
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeDisksFullStatusResponse>
  <DiskFullStatusSet>
    <DiskFullStatusType>
      <DiskEventSet>
        <DiskEventType>
          <EventId>e-event1</EventId>
          <EventType>
            <Code>7</Code>
            <Name>Stalled</Name>
          </EventType>
          <EventTime>2018-05-08T02:43:10Z</EventTime>
        </DiskEventType>
      </DiskEventSet>
      <DiskId>d-disk1</DiskId>
      <InstanceId>i-instance1</InstanceId>
      <Device>/dev/xvda</Device>
      <HealthStatus>
        <Code>128</Code>
        <Name>Impaired</Name>
      </HealthStatus>
      <Status>
        <Code>129</Code>
        <Name>Available</Name>
      </Status>
    </DiskFullStatusType>
    <DiskFullStatusType>
      <DiskEventSet>
        <DiskEventType>
          <EventId>e-event2</EventId>
          <EventType>
            <Code>1</Code>
            <Name>Degraded</Name>
          </EventType>
          <EventTime>2018-05-06T02:43:10Z</EventTime>
          <EventEndTime>2018-05-06T02:48:52Z</EventEndTime>
        </DiskEventType>
      </DiskEventSet>
      <DiskId>d-disk2</DiskId>
      <InstanceId>i-instance2</InstanceId>
      <Device>/dev/xvdb</Device>
      <HealthStatus>
        <Code>64</Code>
        <Name>Warning</Name>
      </HealthStatus>
      <Status>
        <Code>0</Code>
        <Name>Ok</Name>
      </Status>
    </DiskFullStatusType>
  </DiskFullStatusSet>
  <PageNumber>1</PageNumber>
  <PageSize>10</PageSize>
  <RequestId>1A8B4B27-8B2D-XXXX-XXXX-0F64DBE4C211</RequestId>
  <TotalCount>2</TotalCount>
</DescribeDisksFullStatusResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"PageNumber":1,
	"TotalCount":2,
	"PageSize":10,
	"RequestId":"1A8B4B27-8B2D-XXXX-XXXX-0F64DBE4C211",
	"DiskFullStatusSet":{
		"DiskFullStatusType":[
			{
				"Status":{
					"Name":"Available",
					"Code":129
				},
				"Device":"/dev/xvda",
				"HealthStatus":{
					"Name":"Impaired",
					"Code":128
				},
				"InstanceId":"i-instance1",
				"DiskEventSet":{
					"DiskEventType":[
						{
							"EventTime":"2018-05-08T02:43:10Z",
							"EventId":"e-event1",
							"EventType":{
								"Name":"Stalled",
								"Code":"7"
							}
						}
					]
				},
				"DiskId":"d-disk1"
			},
			{
				"Status":{
					"Name":"Available",
					"Code":129
				},
				"Device":"/dev/xvdb",
				"HealthStatus":{
					"Name":"Ok",
					"Code":0
				},
				"InstanceId":"i-instance2",
				"DiskEventSet":{
					"DiskEventType":[
						{
							"EventTime":"2018-05-06T02:43:10Z",
							"EventId":"e-event2",
							"EventType":{
								"Name":"Degraded",
								"Code":"1"
							},
							"EventEndTime":"2018-05-06T02:48:52Z"
						}
					]
				},
				"DiskId":"d-disk2"
			}
		]
	}
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|404|MissingParameter|%s|缺失必需参数。|
|403|InvalidParameter|%s|参数格式不正确。|
|403|DiskIdLimitExceeded|%s|指定的DiskId个数不得超过100个。|
|403|EventIdLimitExceeded|%s|一次最多能指定100个模拟事件ID。|
|403|InvalidParameter.TimeEndBeforeStart|%s|结束时间不得早于开始时间。|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Ecs)

