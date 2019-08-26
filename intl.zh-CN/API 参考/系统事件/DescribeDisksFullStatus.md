# DescribeDisksFullStatus {#DescribeDisksFullStatus .reference}

查询一块或多块磁盘的全部状态信息。

## 描述 {#section_gpz_ts4_ydb .section}

-   磁盘的全部状态信息包含磁盘生命周期（`Status`），磁盘健康状态（`HealthStatus`）和磁盘事件类型（`EventType`）。

-   由于磁盘相关**事件的发布时间**、**事件的计划执行时间**以及**事件的实际执行时间**相同，如果指定一段时间\[`EventTime.Start`, `EventTime.End`\]，则可以查询这段时间中发生过的所有历史事件。目前，您最多可以查询最近一周的历史事件。


## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：DescribeDisksFullStatus|
|RegionId|String|是|磁盘所在地域ID。您可以调用[DescribeRegions](../intl.zh-CN/API 参考/地域/DescribeRegions.md#)查看最新的阿里云地域列表。|
|DiskId.N|String|否|磁盘ID，N的取值范围：\[1, 100\]。|
|EventId.N|String|否|事件ID，N的取值范围：\[1, 100\]。|
|Status|String|否|指定磁盘的生命周期状态，参阅[云盘状态表](intl.zh-CN/API 参考/附录/普通云盘状态表.md#)。取值范围：-   In\_use：使用中
-   Available：待挂载
-   Attaching：挂载中
-   Detaching：卸载中
-   Creating：创建中
-   ReIniting：初始化中

|
|HealthStatus|String|否|指定磁盘的健康状态。取值范围：-   Impaired：暂时性不可读写
-   Warning：服务降级
-   Initializing：初始化中
-   InsufficientData：数据不足
-   NotApplicable：不适用

|
|EventType|String|否|指定磁盘的事件类型。取值范围：-   Degraded：磁盘性能降级
-   SeverelyDegraded：磁盘性能严重降级
-   Stalled：磁盘性能受到严重影响

|
|EventTime.Start|String|否|查询事件发生时间的开始时间。按照[ISO8601](../intl.zh-CN/API 参考/附录/时间格式.md#)标准表示，并需要使用UTC时间，格式为yyyy-MM-ddTHH:mm:ssZ。|
|EventTime.End|String|否|查询事件发生时间的结束时间。按照[ISO8601](../intl.zh-CN/API 参考/附录/时间格式.md#)标准表示，并需要使用UTC时间，格式为yyyy-MM-ddTHH:mm:ssZ。|
|PageNumber|Integer|否|查询结果的页码。取值范围：正整数默认值：1

|
|PageSize|Integer|否|查询结果的分页大小。取值范围：\[1, 100\]默认值：10

|

## 返回参数 {#ResponseParameter .section}

|名称|类型|描述|
|:-|:-|:-|
|TotalCount|Integer|ECS实例状态总个数。|
|PageNumber|Integer|ECS实例列表页码。|
|PageSize|Integer|每页大小。|
|DiskFullStatusSet|Array of [DiskFullStatusType](#)|磁盘全状态数组。|

**数据类型 DiskFullStatusType** 

|名称|类型|描述|
|:-|:-|:-|
|DiskId|String|磁盘ID。|
|InstanceId|String|实例ID。|
|Device|String|磁盘挂载于实例上的设备名，例如 /dev/xvdb。只有在`Status`为`In_use`时才有值，其他状态为空。|
|DiskEventSet|Array of [DiskEventType](#)|磁盘事件数组。|
|Status.Code|Integer|磁盘生命周期状态代码。|
|Status.Name|String|磁盘生命周期状态名称。|
|HealthStatus.Code|Integer|磁盘健康状态代码。|
|HealthStatus.Name|String|磁盘健康状态名称。|

**数据类型 DiskEventType** 

|名称|类型|描述|
|:-|:-|:-|
|EventId|String|磁盘事件ID。|
|EventType.Code|Integer|事件类型代码。|
|EventType.Name|String|事件类型名称。|
|EventTime|String|事件发生时间。您可以调用[DescribeRegions](../intl.zh-CN/API 参考/地域/DescribeRegions.md#)查看最新的阿里云地域列表。|
|EventEndTime|String|事件结束时间。您可以调用[DescribeRegions](../intl.zh-CN/API 参考/地域/DescribeRegions.md#)查看最新的阿里云地域列表。|

## 示例 { .section}

**请求示例**

```
https://ecs.aliyuncs.com/?Action=DescribeDisksFullStatus
&RegionId=cn-hangzhou
&<公共请求参数>
```

**正常返回示例**

**XML格式**

```
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

**JSON格式**

```
{
    "DiskFullStatusSet": {
        "DiskFullStatusType": [
            {
                "DiskEventSet": {
                    "DiskEventType": [
                        {
                            "EventId": "e-event1",
                            "EventType": {
                                "Code": "7",
                                "Name": "Stalled"
                            },
                            "EventTime": "2018-05-08T02:43:10Z"
                        }
                    ]
                },
                "DiskId": "d-disk1",
                "InstanceId": "i-instance1",
                "Device": "/dev/xvda",
                "HealthStatus": {
                    "Code": 128,
                    "Name": "Impaired"
                },
                "Status": {
                    "Code": 129,
                    "Name": "Available"
                }
            },
            {
                "DiskEventSet": {
                    "DiskEventType": [
                        {
                            "EventId": "e-event2",
                            "EventType": {
                                "Code": "1",
                                "Name": "Degraded"
                            },
                            "EventTime": "2018-05-06T02:43:10Z",
                            "EventEndTime": "2018-05-06T02:48:52Z"
                        }
                    ]
                },
                "DiskId": "d-disk2",
                "InstanceId": "i-instance2",
                "Device": "/dev/xvdb",
                "HealthStatus": {
                    "Code": 0,
                    "Name": "Ok"
                },
                "Status": {
                    "Code": 129,
                    "Name": "Available"
                }
            }
        ]
    },
    "PageNumber": 1,
    "PageSize": 10,
    "RequestId": "1A8B4B27-8B2D-XXXX-XXXX-0F64DBE4C211",
    "TotalCount": 2
}
```

**异常返回示例**

**XML格式**

```
<Error>
    <RequestId>C38E0D94-C18B-44F3-8C05-6E35BE334086</RequestId>
    <HostId>ecs.aliyuncs.com</HostId>
    <Code>MissingParameter</Code>
    <Message>The input parameter that is mandatory for processing this request is not supplied.</Message>
</Error>
```

**JSON格式** 

```
{
    "RequestId": "1A8B4B27-8B2D-XXXX-XXXX-0F64DBE4C211",
    "HostId": "ecs.aliyuncs.com"
    "Code": "MissingParameter"
    "Message": "The input parameter that is mandatory for processing this request is not supplied."
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问[API错误中心](https://error-center.alibabacloud.com/status/product/Ecs)。

|错误代码|错误信息|HTTP状态码|说明|
|:---|:---|:------|:-|
|InvalidParameter|The Parameter provided is not valid.|403|请求参数不合法。|
|InvalidParameter.LengthExceeded|The Parameter provided exceeds maximum length.|403|参数EventId.N中N的指定范围只能为\[1, 100\]。|
|InvalidParameter.TooManyDiskId|The diskIds provided is out of bounds \[1,100\].|403|指定的参数值超出了合法范围。|
|InvalidParameter.TimeEndBeforeStart|The event time end should be after event time start.|403|指定的事件时间筛选条件不合法，结束时间必须晚于开始时间。|
|MissingParameter|The input parameter that is mandatory for processing this request is not supplied.|403|输入的参数缺少必填项。|
|InternalError|The request processing has failed due to some unknown error,exception or failure.|500|内部错误。|

