# DescribeInstanceHistoryEvents {#DescribeInstanceHistoryEvents .reference}

查询指定实例的[系统事件](../intl.zh-CN/用户指南/运维与监控/系统事件.md#)信息，默认查询处于非活跃状态的历史系统事件。目前，您最多可以查询最近一周的历史系统事件。

## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：DescribeInstanceHistoryEvents|
|RegionId|String|是|实例所在地域 ID。您可以调用[DescribeRegions](../intl.zh-CN/API 参考/地域/DescribeRegions.md#)查看最新的阿里云地域列表。|
|InstanceId|String|否|实例 ID。不指定实例 ID 时，表示查询您指定地域下所有实例的系统事件信息。|
|EventId.N|String|否|一个或者多个系统事件 ID。N 的取值范围：\[1, 100\]，多个取值使用重复列表的形式，示例 `EventId.1="e-xhskHun1256xxxx"`，`EventId.2="e-xhskHun1257xxxx"` ……|
|InstanceEventCycleStatus.N|String|否|一个或者多个系统事件的生命周期状态。N 的取值范围：\[1, 6\]，多个取值使用重复列表的形式，示例 `InstanceEventCycleStatus.1="Scheduled"`，`InstanceEventCycleStatus.2="Canceled"`……。取值范围：-   Scheduled：等待执行事件
-   Avoided：事件已避免
-   Executing：事件执行中
-   Executed：事件已完成执行
-   Canceled：事件已取消
-   Failed：事件执行失败

|
|EventCycleStatus|String|否|系统事件的生命周期状态。`EventCycleStatus` 只在未指定 `InstanceEventCycleStatus.N` 参数时有效。取值范围：-   Scheduled
-   Avoided
-   Executing
-   Executed
-   Canceled
-   Failed

|
|InstanceEventType.N|String|否|一个或者多个系统事件的类型。N 的取值范围：\[1, 30\]，多个取值使用重复列表的形式，示例 `InstanceEventType.1="Reboot"`，`InstanceEventType.2="SystemFailure.Reboot"`……。取值范围：-   SystemMaintenance.Reboot：因系统维护实例重启
-   SystemFailure.Reboot：因系统错误实例重启
-   InstanceFailure.Reboot：因实例错误实例重启
-   InstanceExpiration.Stop：因预付费期限到期，实例停止
-   InstanceExpiration.Delete：因预付费期限到期，实例释放
-   AccountUnbalanced.Stop：因账号欠费，按量付费实例停止
-   AccountUnbalanced.Delete：因账号欠费，按量付费实例释放

|
|EventType|String|否|系统事件的类型。`EventType` 参数只在未指定 `InstanceEventType.N` 参数时有效。取值范围：-   SystemMaintenance.Reboot：因系统维护实例重启
-   SystemFailure.Reboot：因系统错误实例重启
-   InstanceFailure.Reboot：因实例错误实例重启
-   InstanceExpiration.Stop：因预付费期限到期，实例停止
-   InstanceExpiration.Delete：因预付费期限到期，实例释放
-   AccountUnbalanced.Stop：因账号欠费，按量付费实例停止
-   AccountUnbalanced.Delete：因账号欠费，按量付费实例释放

|
|NotBefore.Start|String|否|查询系统事件计划执行时间的开始时间。按照[ISO8601](../intl.zh-CN/API 参考/附录/时间格式.md#)标准表示，并需要使用UTC时间，格式为yyyy-MM-ddTHH:mm:ssZ。|
|NotBefore.End|String|否|查询系统事件计划执行时间的结束时间。按照[ISO8601](../intl.zh-CN/API 参考/附录/时间格式.md#)标准表示，并需要使用UTC时间，格式为yyyy-MM-ddTHH:mm:ssZ。|
|EventPublishTime.Start|String|否|查询系统事件发布时间的开始时间。按照[ISO8601](../intl.zh-CN/API 参考/附录/时间格式.md#)标准表示，并需要使用UTC时间，格式为yyyy-MM-ddTHH:mm:ssZ。|
|EventPublishTime.End|String|否|查询系统事件发布时间的结束时间。按照[ISO8601](../intl.zh-CN/API 参考/附录/时间格式.md#)标准表示，并需要使用UTC时间，格式为yyyy-MM-ddTHH:mm:ssZ。|
|PageNumber|Integer|否|查询结果的页码。取值范围：正整数默认值：1

|
|PageSize|Integer|否|查询结果的分页大小。取值范围：\[1, 100\]默认值：10

|

## 返回参数 {#ResponseParameter .section}

|名称|类型|描述|
|:-|:-|:-|
|TotalCount|Integer|实例状态总个数。|
|PageNumber|Integer|实例列表页码。|
|PageSize|Integer|输入时设置的每页行数。|
|InstanceSystemEventSet|Array of [InstanceSystemEventType](#)|实例历史系统事件数组。|

**数据类型 InstanceSystemEventType** 

|名称|类型|描述|
|:-|:-|:-|
|InstanceId|String|实例 ID。|
|EventId|String|系统事件 ID。|
|EventType.Code|Integer|系统事件类型代码。|
|EventType.Name|String|系统事件类型名称。|
|EventCycleStatus.Code|Integer|系统事件状态代码。|
|EventCycleStatus.Name|String|系统事件状态名称。|
|EventPublishTime|String|系统事件发布时间。按照[ISO8601](../intl.zh-CN/API 参考/附录/时间格式.md#)标准表示，并需要使用UTC时间，格式为yyyy-MM-ddTHH:mm:ssZ。|
|NotBefore|String|系统事件计划执行时间。按照[ISO8601](../intl.zh-CN/API 参考/附录/时间格式.md#)标准表示，并需要使用UTC时间，格式为yyyy-MM-ddTHH:mm:ssZ。|
|EventFinishTime|String|系统事件结束时间。按照[ISO8601](../intl.zh-CN/API 参考/附录/时间格式.md#)标准表示，并需要使用UTC时间，格式为yyyy-MM-ddTHH:mm:ssZ。|

## 示例 { .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=DescribeInstanceHistoryEvents
&RegionId=cn-hangzhou
&InstanceId=i-2ze3tphuqvc93cixxxx3
&<公共请求参数>
```

**正常返回示例** 

**XML 格式**

```
<DescribeInstanceHistoryEventsResponse>
    <InstanceSystemEventSet>
        <InstanceSystemEventType>
            <InstanceId>i-2ze3tphuqvc93cixxxx3</InstanceId>
            <EventId>e-2ze9yxxxxwtqcvai68rl</EventId>
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
            <InstanceId>i-2ze3tphuqvc93cixxxx3</InstanceId>
            <EventId>e-2ze9yxxxxwtqcvai68r3</EventId>
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

**JSON 格式** 

```
{
  "InstanceSystemEventSet": {
    "InstanceSystemEventType": [
      {
        "InstanceId": "i-2ze3tphuqvc93cixxxx3",
        "EventId": "e-2ze9yxxxxwtqcvai68rl",
        "EventType": {
          "Code": 1,
          "Name": "SystemMaintenance.Reboot"
        },
        "EventCycleStatus": {
          "Code": 0,
          "Name": "Executed"
        },
        "EventPublishTime": "2017-11-30T06:32:31Z",
        "NotBefore": "2017-12-01T06:32:31Z",
        "EventFinishTime": "2017-12-01T06:35:31Z"
      },
      {
        "InstanceId": "i-2ze3tphuqvc93cixxxx3",
        "EventId": "e-2ze9yxxxxwtqcvai68r3",
        "EventType": {
          "Code": 34,
          "Name": "InstanceExpiration.Stop"
        },
        "EventCycleStatus": {
          "Code": 8,
          "Name": "Avoided"
        },
        "EventPublishTime": "2017-11-29T06:32:31Z",
        "NotBefore": "2017-12-06T00:00:00Z",
        "EventFinishTime": "2017-12-05T12:35:31Z"
      }
    ]
  },
  "PageSize": 10,
  "PageNumber": 1,
  "TotalCount": 2,
  "RequestId": "02EA76D3-5A2A-44EB-XXXX-8901881D8707"
}
```

**异常返回示例** 

**XML 格式**

```
<Error>
    <RequestId>C38E0D94-C18B-44F3-8C05-6E35BE334087</RequestId>
    <HostId>ecs.aliyuncs.com</HostId>
    <Code>InvalidParameter</Code>
    <Message>The Parameter "EventCycleStatus" provided is not valid.</Message>
</Error>
```

**JSON 格式** 

```
{
    "RequestId": "1A8B4B27-8B2D-XXXX-XXXX-0F64DBE4C212",
    "HostId": "ecs.aliyuncs.com"
    "Code": "InvalidParameter"
    "Message": "The Parameter "EventCycleStatus" provided is not valid."
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问[API错误中心](https://error-center.alibabacloud.com/status/product/Ecs)。

|错误代码|错误信息|HTTP 状态码|说明|
|:---|:---|:-------|:-|
|InvalidParameter|The Parameter provided is not valid.|403|请求参数不合法。|
|EventIdLimitExceeded|The amount of EventId specified exceeds limit 100.|403|指定的 `EventId` 参数值个数不能超过 100 个。|
|MissingParameter|The input parameter that is mandatory for processing this request is not supplied.|403|输入的参数缺少必填项。|
|InternalError|The request processing has failed due to some unknown error, exception or failure.|500|内部错误。|

