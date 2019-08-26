# DescribeInstanceMonitorData {#DescribeInstanceMonitorData .reference}

查询一台 ECS 实例所有相关的监控信息。返回的监控内容包括 ECS 实例的 CPU 使用率、接收的数据流量、发送的数据流量、网络流量、平均带宽。当返回信息中缺少部分内容时，可能是由于系统没有获取到相应的信息，比如当时实例处于 **已停止**（`Stopped`）状态。

## 描述 {#section_dwp_4w4_ydb .section}

调用该接口时，您需要注意：

-   每次最多返回 400 条监控数据，如果指定的参数 \(`EndTime` `StartTime`\)/`Peroid` \> 400 时，则返回错误。

-   单次最多能查询近 30 天内的监控信息，如果指定的参数 `StartTime` 超过 30 天，则返回错误。


## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：DescribeInstanceMonitorData|
|InstanceId|String|是|待查询的实例 ID。|
|StartTime|String|是|获取数据的起始时间点。按照 [ISO8601](intl.zh-CN/API参考/附录/时间格式.md#) 表示，并需要使用 UTC 时间，格式为：YYYY-MM-DDThh:mm:ssZ。如果指定的秒（`ss`）不是 00，则自动换算为下一分钟。|
|EndTime|String|是|获取数据的结束时间点。按照 ISO8601 标准表示，并需要使用 UTC 时间，格式为：YYYY-MM-DDThh:mm:ssZ。 如果指定的秒（`ss`）不是 00，则自动换算为下一分钟。|
|Period|Integer|否|获取监控数据的间隔时间，单位为秒。取值范围：-   60
-   600
-   3600

默认值：60|

## 返回参数 {#ResponseParameter .section}

|名称|类型|描述|
|:-|:-|:-|
|MonitorData|[InstanceMonitorDataType](intl.zh-CN/API参考/数据类型/InstanceMonitorDataType.md#)|实例的监控数据集合|

## 示例 { .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=DescribeInstanceMonitorData
&InstanceId=i-instnace1
&StartTime=2014-10-29T23:00:00Z
&EndTime=2014-10-30T08:00:00Z
&<公共请求参数>
```

**返回示例** 

**XML 格式**

```
<DescribeInstanceMonitorDataResponse>
    <RequestId>C8B26B44-0189-443E-9816-D951F59623A9</RequestId>
    <MonitorData>
        <InstanceMonitorData>
            <InstanceId>Bc0102-23xYm09</InstanceId>
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

 **JSON 格式** 

```
{
    "RequestId": "C8B26B44-0189-443E-9816-D951F59623A9",
    "MonitorData": {
        "InstanceMonitorData": [{
            "InstanceId": "Bc0102-23xYm09",
            "CPU": 0,
            "IntranetRX": 122,
            "IntranetTX": 343,
            "IntranetFlow": 675,
            "IntranetBandwidth": 10,
            "InternetRX": 122,
            "InternetTX": 343,
            "InternetFlow": 675,
            "InternetBandwidth": 10,
            "IOPSRead": 1000,
            "IOPSWrite": 200,
            "BPSRead": 1000,
            "BPSWrite": 200,
            "TimeStamp": "2010-01-21T09:50:23Z"
        }]
    }
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问 [API 错误中心](https://error-center.alibabacloud.com/status/product/Ecs)。

|错误代码|错误信息|HTTP 状态码|说明|
|:---|:---|:-------|:-|
|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|404|指定的 `InstanceId`不存在。|
|InvalidStartTime.Malformed|The specified parameter “StartTime” is not valid.|400|指定的 `StartTime`格式不正确。|
|InvalidEndTime.Malformed|The specified parameter “EndTime” is not valid.|400|指定的 `EndTime` 格式不正确。|
|InvalidPeriod.ValueNotSupported|The specified parameter “Period” is not valid.|400|指定的 `Period` 不合法。|
|InvalidStartTime.TooEarly|The specified parameter “StartTime” is too early.|400|指定的 `StartTime`早于 30 天，单次最多能查询近 30 天内的监控信息。|
|InvalidParameter.TooManyDataQueried|Too many data queried.|400|查询的数据量过多，每次最多查询 400 条监控数据。|
|Throttling|You have made too many requests within a short time; your request is denied due to request throttling.|400|请求被流控，请稍后再试。|

