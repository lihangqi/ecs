# DescribeInstancesFullStatus {#doc_api_1006045 .reference}

查询一台或多台实例的全状态信息。全状态信息包括实例状态和实例事件状态，其中，实例状态为实例的生命周期状态，实例事件为维护事件的健康状态，更多详情，请参阅实例生命周期和实例系统事件。

## 描述 {#description .section}

返回结果包括实例状态和待执行（Scheduled）状态的实例系统事件。

如果指定一个时间段，则根据时间段筛选事件。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=DescribeInstancesFullStatus)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|RegionId|String|是|cn-hangzhou|实例所在地域 ID。您可以调用 [DescribeRegions](~~25609~~) 查看最新的阿里云地域列表。

 |
|Action|String|否|DescribeInstancesFullStatus|系统规定参数。取值：DescribeInstancesFullStatus

 |
|EventId.N|RepeatList|否|\[EventId.1="e-xhskHun1256xxxx"，EventId.2="e-xhskHun1257xxxx"……\]|一个或者多个事件 ID。N 的取值范围：1~100，多个取值使用重复列表的形式。

 |
|EventPublishTime.End|String|否|2017-12-07T00:00:00Z|查询事件发布时间的结束时间。按照 [ISO8601](~~25696~~) 标准表示，并需要使用UTC时间，格式为yyyy-MM-ddTHH:mm:ssZ。

 |
|EventPublishTime.Start|String|否|2017-11-30T00:00:00Z|查询事件发布时间的开始时间。按照 [ISO8601](~~25696~~) 标准表示，并需要使用UTC时间，格式为yyyy-MM-ddTHH:mm:ssZ。

 |
|EventType|String|否|InstanceExpiration.Stop|一个事件的类型。EventType 参数只在未指定 InstanceEventType.N 参数时有效。取值范围：

 -   SystemMaintenance.Reboot：因系统维护实例重启
-   SystemFailure.Reboot：因系统错误实例重启
-   InstanceFailure.Reboot：因实例错误实例重启
-   InstanceExpiration.Stop：因预付费期限到期，实例停止
-   InstanceExpiration.Delete：因预付费期限到期，实例释放
-   AccountUnbalanced.Stop：因账号欠费，按量付费实例停止
-   AccountUnbalanced.Delete：因账号欠费，按量付费实例释放

 |
|HealthStatus|String|否|Maintaining|指定实例的健康状态。取值范围：

 -   Impaired：服务损坏
-   Warning：服务降级
-   Maintaining：系统维护
-   Initializing：初始化中
-   InsufficientData：数据不足
-   NotApplicable：不适用

 以上参数取值均区分大小写。

 |
|InstanceEventType.N|RepeatList|否|InstanceExpiration.Stop|一个或者多个事件的类型。N 的取值范围：1~30，多个取值使用重复列表的形式。取值范围：

 -   SystemMaintenance.Reboot：因系统维护实例重启
-   SystemFailure.Reboot：因系统错误实例重启
-   InstanceFailure.Reboot：因实例错误实例重启
-   InstanceExpiration.Stop：因预付费期限到期，实例停止
-   InstanceExpiration.Delete：因预付费期限到期，实例释放
-   AccountUnbalanced.Stop：因账号欠费，按量付费实例停止
-   AccountUnbalanced.Delete：因账号欠费，按量付费实例释放

 |
|InstanceId.N|RepeatList|否|\[InstanceId.1="i-instance1"，InstanceId.2="i-instance2"……\]|一台或者多台实例 ID。N 的取值范围：1~100，多个取值使用重复列表的形式。

 |
|NotBefore.End|String|否|2017-11-30T00:00:00Z|查询事件计划执行时间的结束时间。按照 [ISO8601](~~25696~~) 标准表示，并需要使用UTC时间，格式为yyyy-MM-ddTHH:mm:ssZ。

 |
|NotBefore.Start|String|否|2017-12-07T00:00:00Z|查询事件计划执行时间的开始时间。按照 [ISO8601](~~25696~~) 标准表示，并需要使用UTC时间，格式为yyyy-MM-ddTHH:mm:ssZ。

 |
|OwnerAccount|String|否|ECSforCloud@Alibaba.com|RAM 用户的账号登录名称。

 |
|PageNumber|Integer|否|1|查询结果的页码。取值范围：正整数

 默认值：1

 |
|PageSize|Integer|否|10|查询结果的分页大小。取值范围：1~100

 默认值：10

 |
|Status|String|否|Running|指定实例的生命周期状态。取值范围：

 -   Starting：启动中
-   Running：运行中
-   Stopped：已停止

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|InstanceFullStatusSet| | |实例全状态数组

 |
|└HealthStatus| | |实例的健康状态

 |
|└Code|Integer|64|健康状态代码

 |
|└Name|String|Warning|健康状态名称

 |
|└InstanceId|String|i-instance1|实例 ID

 |
|└ScheduledSystemEventSet| | |系统计划事件数组

 |
|└EventCycleStatus| | |事件状态

 |
|└Code|Integer|24|事件状态代码

 |
|└Name|String|Scheduled|事件状态名称

 |
|└EventId|String|e-event1|实例事件 ID

 |
|└EventPublishTime|String|2017-11-30T06:32:31Z|事件的发布时间。按照 [ISO8601](~~25696~~) 标准表示，并需要使用UTC时间，格式为yyyy-MM-ddTHH:mm:ssZ。

 |
|└EventType| | |事件类型

 |
|└Code|Integer|1|事件类型代码

 |
|└Name|String|SystemMaintenance.Reboot|事件类型名称

 |
|└ExtendedAttribute| | |本地盘实例系统事件拓展属性。

 |
|└Device|String|/dev/vdb|本地盘磁盘设备名。

 |
|└DiskId|String|d-diskid2|本地盘磁盘ID。

 |
|└NotBefore|String|2017-12-07T00:00:00Z|事件的计划执行时间。按照 [ISO8601](~~25696~~) 标准表示，并需要使用UTC时间，格式为yyyy-MM-ddTHH:mm:ssZ。

 |
|└Status| | |实例生命周期状态

 |
|└Code|Integer|1|实例生命周期状态代码

 |
|└Name|String|Running|实例生命周期状态名称

 |
|PageNumber|Integer|1|页码

 |
|PageSize|Integer|10|每页大小

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。无论调用接口成功与否，我们都会返回请求 ID。

 |
|TotalCount|Integer|2|总条数

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

https://ecs.aliyuncs.com/?Action=DescribeInstancesFullStatus
&RegionId=cn-hangzhou
&InstanceId.1=i-instance1
&EventId.1=e-event1
&Status=Running
&HealthStatus=Maintaining
&InstanceEventType.1=InstanceExpiration.Stop
&EventType=InstanceExpiration.Stop
&NotBefore.Start=2017-12-07T00:00:00Z
&NotBefore.End=2017-11-30T00:00:00Z
&EventPublishTime.Start=2017-11-30T00:00:00Z
&EventPublishTime.End=2017-12-07T00:00:00Z
&PageNumber=1
&PageSize=10
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeInstancesFullStatusResponse>
    <?xml version="1.0" encoding="UTF-8" ?>
    <InstanceFullStatusSet>
        <InstanceFullStatusType>
            <InstanceId>i-instance1</InstanceId>
            <Status>
                <Code>1</Code>
                <Name>Running</Name>
            </Status>
            <HealthStatus>
                <Code>0</Code>
                <Name>Maintaining</Name>
            </HealthStatus>
            <ScheduledSystemEventSet>
                <ScheduledSystemEventType>
                    <EventId>e-event1</EventId>
                    <EventCycleStatus>
                        <Code>24</Code>
                        <Name>Scheduled</Name>
                    </EventCycleStatus>
                    <EventType>
                        <Code>1</Code>
                        <Name>SystemMaintenance.Reboot</Name>
                    </EventType>
                    <EventPublishTime>2017-11-30T06:32:31Z</EventPublishTime>
                    <NotBefore>2017-12-01T06:32:31Z</NotBefore>
                </ScheduledSystemEventType>
                <ScheduledSystemEventType>
                    <EventId>e-event2</EventId>
                    <EventCycleStatus>
                        <Code>24</Code>
                        <Name>Scheduled</Name>
                    </EventCycleStatus>
                    <EventType>
                        <Code>34</Code>
                        <Name>InstanceExpiration.Stop</Name>
                    </EventType>
                    <EventPublishTime>2017-11-30T00:00:00Z</EventPublishTime>
                    <NotBefore>2017-12-07T00:00:00Z</NotBefore>
                </ScheduledSystemEventType>
            </ScheduledSystemEventSet>
        </InstanceFullStatusType>
        <InstanceFullStatusType>
            <InstanceId>i-instance2</InstanceId>
            <Status>
                <Code>1</Code>
                <Name>Running</Name>
            </Status>
            <HealthStatus>
                <Code>64</Code>
                <Name>Warning</Name>
            </HealthStatus>
            <ScheduledSystemEventSet>
                <ScheduledSystemEventType>
                    <EventId>e-event3</EventId>
                    <EventCycleStatus>
                        <Code>24</Code>
                        <Name>Scheduled</Name>
                    </EventCycleStatus>
                    <EventType>
                        <Code>65</Code>
                        <Name>SystemFailure.Reboot</Name>
                    </EventType>
                    <EventPublishTime>2017-11-30T06:32:31Z</EventPublishTime>
                    <NotBefore>2017-12-01T06:32:31Z</NotBefore>
                </ScheduledSystemEventType>
            </ScheduledSystemEventSet>
        </InstanceFullStatusType>
    </InstanceFullStatusSet>
    <PageSize>10</PageSize>
    <PageNumber>1</PageNumber>
    <TotalCount>2</TotalCount>
    <RequestId>AAC49D3E-ED6F-4F00-XXXX-377C551B1DD4</RequestId>
</DescribeInstancesFullStatusResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"PageNumber":1,
	"TotalCount":2,
	"PageSize":10,
	"InstanceFullStatusSet":{
		"InstanceFullStatusType":[
			{
				"Status":{
					"Name":"Running",
					"Code":1
				},
				"HealthStatus":{
					"Name":"Maintaining",
					"Code":0
				},
				"InstanceId":"i-instance1",
				"ScheduledSystemEventSet":{
					"ScheduledSystemEventType":[
						{
							"EventPublishTime":"2017-11-30T06:32:31Z",
							"NotBefore":"2017-12-01T06:32:31Z",
							"EventId":"e-event1",
							"EventType":{
								"Name":"SystemMaintenance.Reboot",
								"Code":1
							},
							"EventCycleStatus":{
								"Name":"Scheduled",
								"Code":24
							}
						},
						{
							"EventPublishTime":"2017-11-30T00:00:00Z",
							"NotBefore":"2017-12-07T00:00:00Z",
							"EventId":"e-event2",
							"EventType":{
								"Name":"InstanceExpiration.Stop",
								"Code":34
							},
							"EventCycleStatus":{
								"Name":"Scheduled",
								"Code":24
							}
						}
					]
				}
			},
			{
				"Status":{
					"Name":"Running",
					"Code":1
				},
				"HealthStatus":{
					"Name":"Warning",
					"Code":64
				},
				"InstanceId":"i-instance2",
				"ScheduledSystemEventSet":{
					"ScheduledSystemEventType":[
						{
							"EventPublishTime":"2017-11-30T06:32:31Z",
							"NotBefore":"2017-12-01T06:32:31Z",
							"EventId":"e-event3",
							"EventType":{
								"Name":"SystemFailure.Reboot",
								"Code":65
							},
							"EventCycleStatus":{
								"Name":"Scheduled",
								"Code":24
							}
						}
					]
				}
			}
		]
	},
	"RequestId":"AAC49D3E-ED6F-4F00-XXXX-377C551B1DD4"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|404|MissingParameter|%s|缺失必需参数。|
|403|InvalidParameter|%s|参数格式不正确。|
|403|InvalidParameter.TimeEndBeforeStart|%s|结束时间不得早于开始时间。|
|403|OperationDenied.NotInWhiteList|%s|无权限执行此操作。|
|403|InstanceIdLimitExceeded|%s|指定的InstanceId个数不得超过100个。|
|403|EventIdLimitExceeded|%s|一次最多能指定100个模拟事件ID。|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Ecs)

