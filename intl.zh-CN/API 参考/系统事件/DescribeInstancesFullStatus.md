# DescribeInstancesFullStatus {#DescribeInstancesFullStatus .reference}

查询一台或多台实例的全状态信息。全状态信息包括实例状态和实例事件状态，其中，实例状态为实例的生命周期状态，实例事件为维护事件的健康状态，更多详情，请参阅 [实例生命周期](../intl.zh-CN/产品简介/实例/实例生命周期.md#) 和 [实例系统事件](../intl.zh-CN/用户指南/运维与监控/系统事件.md#)。

## 描述 {#section_rcq_354_ydb .section}

返回结果包括实例状态和 **待执行**（`Scheduled`） 状态的实例系统事件。

如果指定一个时间段，则根据时间段筛选事件。

## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：DescribeInstancesFullStatus|
|RegionId|String|是|实例所在地域 ID。您可以调用[DescribeRegions](../intl.zh-CN/API 参考/地域/DescribeRegions.md#)查看最新的阿里云地域列表。|
|InstanceId.N|String|否|一台或者多台实例 ID。`N` 的取值范围：\[1, 100\]，多个取值使用重复列表的形式，示例 `InstanceId.1="i-instance1"`，`InstanceId.2="i-instance2"`……|
|EventId.N|String|否|一个或者多个事件 ID。`N` 的取值范围：\[1, 100\]，多个取值使用重复列表的形式，示例 `EventId.1="e-xhskHun1256xxxx"`，`EventId.2="e-xhskHun1257xxxx"`……|
|Status|String|否|指定实例的生命周期状态。取值范围：-   Starting：启动中
-   Running：运行中
-   Stopped：已停止

|
|HealthStatus|String|否|指定实例的健康状态。取值范围：-   Impaired：服务损坏
-   Warning：服务降级
-   Maintaining：系统维护
-   Initializing：初始化中
-   InsufficientData：数据不足
-   NotApplicable：不适用

以上参数取值均大小写敏感。

|
|InstanceEventType.N|String|否|一个或者多个事件的类型。`N` 的取值范围：\[1, 30\]，多个取值使用重复列表的形式，示例 `InstanceEventType.1="SystemMaintenance.Reboot"`，`InstanceEventType.2="SystemFailure.Reboot"`……。取值范围：-   SystemMaintenance.Reboot：因系统维护实例重启
-   SystemFailure.Reboot：因系统错误实例重启
-   InstanceFailure.Reboot：因实例错误实例重启
-   InstanceExpiration.Stop：因预付费期限到期，实例停止
-   InstanceExpiration.Delete：因预付费期限到期，实例释放
-   AccountUnbalanced.Stop：因账号欠费，按量付费实例停止
-   AccountUnbalanced.Delete：因账号欠费，按量付费实例释放

|
|EventType|String|否|一个事件的类型。`EventType` 参数只在未指定 `InstanceEventType.N` 参数时有效。取值范围：-   SystemMaintenance.Reboot：因系统维护实例重启
-   SystemFailure.Reboot：因系统错误实例重启
-   InstanceFailure.Reboot：因实例错误实例重启
-   InstanceExpiration.Stop：因预付费期限到期，实例停止
-   InstanceExpiration.Delete：因预付费期限到期，实例释放
-   AccountUnbalanced.Stop：因账号欠费，按量付费实例停止
-   AccountUnbalanced.Delete：因账号欠费，按量付费实例释放

|
|NotBefore.Start|String|否|查询事件计划执行时间的开始时间。按照[ISO8601](../intl.zh-CN/API 参考/附录/时间格式.md#)标准表示，并需要使用UTC时间，格式为yyyy-MM-ddTHH:mm:ssZ。|
|NotBefore.End|String|否|查询事件计划执行时间的结束时间。按照[ISO8601](../intl.zh-CN/API 参考/附录/时间格式.md#)标准表示，并需要使用UTC时间，格式为yyyy-MM-ddTHH:mm:ssZ。|
|EventPublishTime.Start|String|否|查询事件发布时间的开始时间。按照[ISO8601](../intl.zh-CN/API 参考/附录/时间格式.md#)标准表示，并需要使用UTC时间，格式为yyyy-MM-ddTHH:mm:ssZ。|
|EventPublishTime.End|String|否|查询事件发布时间的结束时间。按照[ISO8601](../intl.zh-CN/API 参考/附录/时间格式.md#)标准表示，并需要使用UTC时间，格式为yyyy-MM-ddTHH:mm:ssZ。|
|PageNumber|Integer|否|查询结果的页码。取值范围：正整数默认值：1

|
|PageSize|Integer|否|查询结果的分页大小。取值范围：\[1,100\]默认值：10

|

## 返回参数 {#ResponseParameter .section}

|名称|类型|描述|
|:-|:-|:-|
|TotalCount|Integer|总条数|
|PageNumber|Integer|页码|
|PageSize|Integer|每页大小|
|InstanceFullStatusSet|Array of [`InstanceFullStatusType`](#)|实例全状态数组|

**数据类型 InstanceFullStatusType** 

|名称|类型|描述|
|:-|:-|:-|
|InstanceId|String|实例 ID|
|ScheduledSystemEventSet|Array of [`ScheduledSystemEventType`](#)|系统计划事件数组|
|Status.Code|Integer|实例生命周期状态代码|
|Status.Name|String|实例生命周期状态名称|
|HealthStatus.Code|Integer|健康状态代码|
|HealthStatus.Name|String|健康状态名称|

 **数据类型 ScheduledSystemEventType** 

|名称|类型|描述|
|:-|:-|:-|
|EventId|String|实例事件 ID|
|EventCycleStatus.Code|Integer|事件状态代码|
|EventCycleStatus.Name|String|事件状态名称|
|EventType.Code|Integer|事件类型代码|
|EventType.Name|String|事件类型名称|
|EventPublishTime|String|事件的发布时间。按照[ISO8601](../intl.zh-CN/API 参考/附录/时间格式.md#)标准表示，并需要使用UTC时间，格式为yyyy-MM-ddTHH:mm:ssZ。|
|NotBefore|String|事件的计划执行时间。按照[ISO8601](../intl.zh-CN/API 参考/附录/时间格式.md#)标准表示，并需要使用UTC时间，格式为yyyy-MM-ddTHH:mm:ssZ。|

## 示例 { .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=DescribeInstancesFullStatus
&RegionId=cn-hangzhou
&<公共请求参数>
```

**正常返回示例** 

**XML 格式**

```
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

**JSON 格式** 

```
{
  "InstanceFullStatusSet": {
    "InstanceFullStatusType": [
      {
        "InstanceId": "i-instance1",
        "Status": {
          "Code": 1,
          "Name": "Running"
        },
        "HealthStatus": {
          "Code": 0,
          "Name": "Maintaining"
        },
        "ScheduledSystemEventSet": {
          "ScheduledSystemEventType": [
            {
              "EventId": "e-event1",
              "EventCycleStatus": {
                "Code": 24,
                "Name": "Scheduled"
              },
              "EventType": {
                "Code": 1,
                "Name": "SystemMaintenance.Reboot"
              },
              "EventPublishTime": "2017-11-30T06:32:31Z",
              "NotBefore": "2017-12-01T06:32:31Z"
            },
            {
              "EventId": "e-event2",
              "EventCycleStatus": {
                "Code": 24,
                "Name": "Scheduled"
              },
              "EventType": {
                "Code": 34,
                "Name": "InstanceExpiration.Stop"
              },
              "EventPublishTime": "2017-11-30T00:00:00Z",
              "NotBefore": "2017-12-07T00:00:00Z"
            }
          ]
        }
      },
      {
        "InstanceId": "i-instance2",
        "Status": {
          "Code": 1,
          "Name": "Running"
        },
        "HealthStatus": {
          "Code": 64,
          "Name": "Warning"
        },
        "ScheduledSystemEventSet": {
          "ScheduledSystemEventType": [
            {
              "EventId": "e-event3",
              "EventCycleStatus": {
                "Code": 24,
                "Name": "Scheduled"
              },
              "EventType": {
                "Code": 65,
                "Name": "SystemFailure.Reboot"
              },
              "EventPublishTime": "2017-11-30T06:32:31Z",
              "NotBefore": "2017-12-01T06:32:31Z"
            }
          ]
        }
      }
    ]
  },
  "PageSize": 10,
  "PageNumber": 1,
  "TotalCount": 2,
  "RequestId": "AAC49D3E-ED6F-4F00-XXXX-377C551B1DD4"
}
```

**异常返回示例** 

**XML 格式**

```
<Error>
    <RequestId>C38E0D94-C18B-44F3-8C05-6E35BE334088</RequestId>
    <HostId>ecs.aliyuncs.com</HostId>
    <Code>InstanceIdLimitExceeded</Code>
    <Message>The amount of InstanceId specified exceeds limit 100.</Message>
</Error>
```

**JSON 格式** 

```
{
    "RequestId": "1A8B4B27-8B2D-XXXX-XXXX-0F64DBE4C213",
    "HostId": "ecs.aliyuncs.com"
    "Code": "InstanceIdLimitExceeded"
    "Message": "The amount of InstanceId specified exceeds limit 100."
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问[API错误中心](https://error-center.alibabacloud.com/status/product/Ecs)。

|错误代码|错误信息|HTTP 状态码|说明|
|:---|:---|:-------|:-|
|InvalidParameter|The Parameter provided is not valid.|403|请求参数不合法。|
|EventIdLimitExceeded|The amount of EventId specified exceeds limit 100.|403|指定的 `EventId` 参数值个数超出了合法范围。|
|InstanceIdLimitExceeded|The amount of InstanceId specified exceeds limit 100.|403|指定的 `InstanceId` 参数值个数超出了合法范围。|
|MissingParameter|The input parameter that is mandatory for processing this request is not supplied.|403|输入的参数缺少必填项。|
|InternalError|The request processing has failed due to some unknown error,exception or failure.|500|内部错误。|

