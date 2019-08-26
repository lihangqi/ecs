# DescribeInstanceHistoryEvents {#doc_api_Ecs_DescribeInstanceHistoryEvents .reference}

调用DescribeInstanceHistoryEvents查询指定实例的系统事件信息，默认查询处于非活跃状态的历史系统事件。您最多可以查询最近一周的历史系统事件。通过指定InstanceEventCycleStatus参数，可以查询处于Scheduled（计划中）和Executing（执行中）状态的系统事件。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=DescribeInstanceHistoryEvents)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|RegionId|String|是|cn-hangzhou|实例所在地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。

 |
|Action|String|否|DescribeInstanceHistoryEvents|系统规定参数。对于您自行拼凑HTTP/HTTPS URL发起的API请求，`Action`为必选参数。取值：DescribeInstanceHistoryEvents

 |
|EventCycleStatus|String|否|Executed|系统事件的生命周期状态。EventCycleStatus只在未指定InstanceEventCycleStatus.N参数时有效。取值范围：

 -   Scheduled
-   Avoided
-   Executing
-   Executed
-   Canceled
-   Failed

 |
|EventId.N|RepeatList|否|e-2ze9yxxxxwtqcvai68rl|一个或者多个系统事件ID。N的取值范围：1~100，多个取值使用重复列表的形式。

 |
|EventPublishTime.End|String|否|2017-12-01T06:32:31Z|查询系统事件发布时间的结束时间。按照[ISO8601](~~25696~~)标准表示，并需要使用UTC +0时间，格式为yyyy-MM-ddTHH:mm:ssZ。

 |
|EventPublishTime.Start|String|否|2017-11-30T06:32:31Z|查询系统事件发布时间的开始时间。按照[ISO8601](~~25696~~)标准表示，并需要使用UTC +0时间，格式为yyyy-MM-ddTHH:mm:ssZ。

 |
|EventType|String|否|SystemMaintenance.Reboot|系统事件的类型。EventType参数只在未指定InstanceEventType.N参数时有效。取值范围：

 -   SystemMaintenance.Reboot：因系统维护实例重启
-   SystemFailure.Reboot：因系统错误实例重启
-   SystemFailure.Delete：因实例创建失败实例释放
-   InstanceFailure.Reboot：因实例错误实例重启
-   InstanceExpiration.Stop：因预付费期限到期，实例停止
-   InstanceExpiration.Delete：因预付费期限到期，实例释放
-   AccountUnbalanced.Stop：因账号欠费，按量付费实例停止
-   AccountUnbalanced.Delete：因账号欠费，按量付费实例释放

 |
|InstanceEventCycleStatus.N|RepeatList|否|Executed|一个或者多个系统事件的生命周期状态。N的取值范围：1~6，多个取值使用重复列表的形式。取值范围：

 -   Scheduled：等待执行事件
-   Avoided：事件已避免
-   Executing：事件执行中
-   Executed：事件已完成执行
-   Canceled：事件已取消
-   Failed：事件执行失败

 |
|InstanceEventType.N|RepeatList|否|SystemMaintenance.Reboot|一个或者多个系统事件的类型。N的取值范围：1~30，多个取值使用重复列表的形式。取值范围：

 -   SystemMaintenance.Reboot：因系统维护实例重启
-   SystemFailure.Reboot：因系统错误实例重启
-   SystemFailure.Delete：因实例创建失败实例释放
-   InstanceFailure.Reboot：因实例错误实例重启
-   InstanceExpiration.Stop：因预付费期限到期，实例停止
-   InstanceExpiration.Delete：因预付费期限到期，实例释放
-   AccountUnbalanced.Stop：因账号欠费，按量付费实例停止
-   AccountUnbalanced.Delete：因账号欠费，按量付费实例释放

 |
|InstanceId|String|否|i-myInstance|实例ID。不指定实例ID 时，表示查询您指定地域下所有实例的系统事件信息。

 |
|NotBefore.End|String|否|2017-12-01T06:32:31Z|查询系统事件计划执行时间的结束时间。按照[ISO8601](~~25696~~)标准表示，并需要使用UTC +0时间，格式为yyyy-MM-ddTHH:mm:ssZ。

 |
|NotBefore.Start|String|否|2017-11-30T06:32:31Z|查询系统事件计划执行时间的开始时间。按照[ISO8601](~~25696~~)标准表示，并需要使用UTC +0时间，格式为yyyy-MM-ddTHH:mm:ssZ。

 |
|PageNumber|Integer|否|1|查询结果的页码。取值范围：正整数

 默认值：1

 |
|PageSize|Integer|否|10|查询结果的分页大小。取值范围：1~100

 默认值：10

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|InstanceSystemEventSet| | |实例历史系统事件数组。

 |
|EventCycleStatus| | |系统事件的生命周期状态。

 |
|Code|Integer|0|系统事件状态代码。

 |
|Name|String|Executed|系统事件状态名称。

 |
|EventFinishTime|String|2017-12-01T06:35:31Z|系统事件结束时间。按照[ISO8601](~~25696~~)标准表示，并需要使用UTC +0时间，格式为yyyy-MM-ddTHH:mm:ssZ。

 |
|EventId|String|e-2ze9yxxxxwtqcvai6\*\*\*|系统事件ID。

 |
|EventPublishTime|String|2017-11-30T06:32:31Z|系统事件发布时间。按照[ISO8601](~~25696~~)标准表示，并需要使用UTC +0时间，格式为yyyy-MM-ddTHH:mm:ssZ。

 |
|EventType| | |系统事件类型。

 |
|Code|Integer|34|系统事件类型代码。

 |
|Name|String|InstanceExpiration.Stop|系统事件类型名称。

 |
|ExtendedAttribute| | |事件扩展属性。

 |
|Device|String|/dev/vda|本地盘磁盘设备名。

 |
|DiskId|String|d-diskid1|本地盘磁盘ID。

 |
|InstanceId|String|i-myInstance|实例ID。

 |
|NotBefore|String|2017-12-06T00:00:00Z|系统事件计划执行时间。按照[ISO8601](~~25696~~)标准表示，并需要使用UTC +0时间，格式为yyyy-MM-ddTHH:mm:ssZ。

 |
|PageNumber|Integer|1|实例列表页码。

 |
|PageSize|Integer|10|输入时设置的每页行数。

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。

 |
|TotalCount|Integer|2|实例状态总个数。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=DescribeInstanceHistoryEvents
&RegionId=cn-hangzhou
&InstanceId=i-myInstance
&EventId.1=e-2ze9yxxxxwtqcvai6***
&InstanceEventCycleStatus.1=Executed
&EventCycleStatus=Executed
&InstanceEventType.1=SystemMaintenance.Reboot
&EventType=SystemMaintenance.Reboot
&NotBefore.Start=2017-11-30T06:32:31Z
&NotBefore.End=2017-12-01T06:32:31Z
&EventPublishTime.Start=2017-11-30T06:32:31Z
&EventPublishTime.End=2017-12-01T06:32:31Z
&PageNumber=1
&PageSize=10
&<公共请求参数>
```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeInstanceHistoryEventsResponse>
  <InstanceSystemEventSet>
    <InstanceSystemEventType>
      <InstanceId>i-2ze3tphuqvc93ci****3</InstanceId>
      <EventId>e-2ze9y****wtqcvai68rl</EventId>
      <EventType>
        <Code>1</Code>
        <Name>SystemMaintenance.Reboot</Name>
      </EventType>
      <EventCycleStatus>
        <Code>0</Code>
        <Name>Executed</Name>
      </EventCycleStatus>
      <EventPublishTime>2017-11-30T06:32:31Z</EventPublishTime>
      <NotBefore>2017-12-01T06:32:31Z</NotBefore>
      <EventFinishTime>2017-12-01T06:35:31Z</EventFinishTime>
    </InstanceSystemEventType>
    <InstanceSystemEventType>
      <InstanceId>i-2ze3tphuqvc93ci****3</InstanceId>
      <EventId>e-2ze9y****wtqcvai68r3</EventId>
      <EventType>
        <Code>34</Code>
        <Name>InstanceExpiration.Stop</Name>
      </EventType>
      <EventCycleStatus>
        <Code>8</Code>
        <Name>Avoided</Name>
      </EventCycleStatus>
      <EventPublishTime>2017-11-29T06:32:31Z</EventPublishTime>
      <NotBefore>2017-12-06T00:00:00Z</NotBefore>
      <EventFinishTime>2017-12-05T12:35:31Z</EventFinishTime>
    </InstanceSystemEventType>
  </InstanceSystemEventSet>
  <PageSize>10</PageSize>
  <PageNumber>1</PageNumber>
  <TotalCount>2</TotalCount>
  <RequestId>02EA76D3-5A2A-44EB-XXXX-8901881D8707</RequestId>
</DescribeInstanceHistoryEventsResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"PageNumber":1,
	"TotalCount":2,
	"PageSize":10,
	"RequestId":"02EA76D3-5A2A-44EB-XXXX-8901881D8707",
	"InstanceSystemEventSet":{
		"InstanceSystemEventType":[
			{
				"EventPublishTime":"2017-11-30T06:32:31Z",
				"NotBefore":"2017-12-01T06:32:31Z",
				"EventFinishTime":"2017-12-01T06:35:31Z",
				"InstanceId":"i-2ze3tphuqvc93ci****3",
				"EventId":"e-2ze9y****wtqcvai68rl",
				"EventType":{
					"Name":"SystemMaintenance.Reboot",
					"Code":1
				},
				"EventCycleStatus":{
					"Name":"Executed",
					"Code":0
				}
			},
			{
				"EventPublishTime":"2017-11-29T06:32:31Z",
				"NotBefore":"2017-12-06T00:00:00Z",
				"EventFinishTime":"2017-12-05T12:35:31Z",
				"InstanceId":"i-2ze3tphuqvc93ci****3",
				"EventId":"e-2ze9y****wtqcvai68r3",
				"EventType":{
					"Name":"InstanceExpiration.Stop",
					"Code":34
				},
				"EventCycleStatus":{
					"Name":"Avoided",
					"Code":8
				}
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
|403|EventIdLimitExceeded|%s|一次最多能指定100个模拟事件ID。|
|403|InvalidParameter.TimeEndBeforeStart|%s|结束时间不得早于开始时间。|
|403|OperationDenied.NotInWhiteList|%s|无权限执行此操作。|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

