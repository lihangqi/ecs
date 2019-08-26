# DescribeEniMonitorData {#DescribeEniMonitorData .reference}

查询一块辅助网卡在指定时间段内使用的流量信息。

## 描述 {#BestPractice .section}

可查询的辅助网卡流量信息包括辅助网卡收发数据包的数量、内网出入流量、辅助网卡收发丢包的数量。当返回信息中缺少部分内容时，可能是由于系统没有获取到相应的信息。例如，当时实例处于**已停止**（`Stopped`）状态或者辅助网卡没有挂载到实例上，即处于**可用**（`Available`）状态。调用该接口时，您需要注意：

-   每次最多返回400条监控数据，即，如果指定的参数\(EndTime-StartTime\)/Peroid\>400时，则返回错误。
-   单次最多能查询近30天内的监控信息，如果指定的参数StartTime超过30天，则返回错误。

## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：DescribeEniMonitorData|
|InstanceId|String|是|辅助网卡绑定的实例ID。|
|EniId|String|否|辅助网卡的ID。默认查询指定实例上所有已绑定的辅助网卡。|
|StartTime|String|是|获取数据的起始时间点。按照[ISO8601](../cn.zh-CN/API 参考/附录/时间格式.md#)标准表示，并需要使用UTC时间，格式为yyyy-MM-ddTHH:mm:ssZ。如果指定的秒（`ss`）不是`00`，则自动换算为下一分钟。|
|EndTime|String|是|获取数据的起始时间点。按照[ISO8601](../cn.zh-CN/API 参考/附录/时间格式.md#)标准表示，并需要使用UTC时间，格式为yyyy-MM-ddTHH:mm:ssZ。如果指定的秒（`ss`）不是`00`，则自动换算为下一分钟。|
|Period|Integer|否|获取监控数据的间隔时间，单位：秒。取值范围：60 | 600 | 3600默认值：60

|

## 返回参数 {#ResponseParameter .section}

|名称|类型|描述|
|:-|:-|:-|
|MonitorData|[EniMonitorDataType](https://lark.alipay.com/docs/share/983c4182-3f3f-48d5-9615-6a214f9568e2)|辅助网卡流量的监控数据EniMonitorDataType组成的集合。|

**数据类型EniMonitorDataType**

|名称|类型|描述|
|:-|:-|:-|
|EniId|String|辅助网卡ID。|
|TimeStamp|String|查询监控信息的时间戳。按照[ISO8601](../cn.zh-CN/API 参考/附录/时间格式.md#)标准表示，并需要使用UTC时间，格式为yyyy-MM-ddTHH:mm:ssZ。|
|PacketTx|String|辅助网卡发送的内网数据包，单位：packets。|
|PacketRx|String|辅助网卡接收的内网数据包，单位：packets。|
|IntranetTx|String|辅助网卡发送的内网数据流量，单位：kbits。|
|IntranetRx|String|辅助网卡接收的内网数据流量，单位：kbits。|
|DropPacketTx|String|辅助网卡发送丢弃的内网数据包，单位：packets。|
|DropPacketRx|String|辅助网卡接收丢弃的内网数据包，单位：packets。|

## 示例 { .section}

**请求示例**

```
https://ecs.aliyuncs.com/?Action=DescribeEniMonitorData
&EniId=eni-myENI
&InstanceId=myInstance
&StartTime=2018-05-21T12:19:00Z
&EndTime=2018-05-21T12:22:00Z
&<公共请求参数>
```

**返回示例**

**XML格式**

```
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

**JSON格式**

```
{
 "RequestId":"5A03C2BA-3BCE-4A87-8076-7DC1629",
 "MonitorData":{
     "EniMonitorData":[
         {
             "PacketTx":0,
             "TimeStamp":"2018-05-21T03:22:00Z",
             "IntranetOut":0,
             "DropPacketRx":0,
             "IntranetIn":0,
             "EniId":"eni-myENI",
             "DropPacketTx":0,
             "PacketRx":0
         },
         {
             "PacketTx":0,
             "TimeStamp":"2018-05-21T03:21:00Z",
             "IntranetOut":0,
             "DropPacketRx":0,
             "IntranetIn":0,
             "EniId":"eni-myENI",
             "DropPacketTx":0,
             "PacketRx":0
         },
         {
             "PacketTx":52240,
             "TimeStamp":"2018-05-21T03:19:00Z",
             "IntranetOut":73344,
             "DropPacketRx":0,
             "IntranetIn":467,
             "EniId":"eni-myENI",
             "DropPacketTx":0,
             "PacketRx":6603
         },
         {
             "PacketTx":34925,
             "TimeStamp":"2018-05-21T03:20:00Z",
             "IntranetOut":48871,
             "DropPacketRx":0,
             "IntranetIn":350,
             "EniId":"eni-myENI",
             "DropPacketTx":0,
             "PacketRx":4888
         }
     ]
 }
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问[API错误中心](https://error-center.aliyun.com/status/product/Ecs)。

|错误代码|错误信息|HTTP状态码|说明|
|:---|:---|:------|:-|
|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|404|指定的InstanceId不存在。|
|InvalidStartTime.Malformed|The specified parameter “StartTime” is not valid.|400|指定的StartTime格式不正确。|
|InvalidEndTime.Malformed|The specified parameter “EndTime” is not valid.|400|指定的EndTime格式不正确。|
|InvalidPeriod.ValueNotSupported|The specified parameter “Period” is not valid.|400|指定的Period不合法。|
|InvalidStartTime.TooEarly|The specified parameter “StartTime” is too early.|400|指定的StartTime早于30天，单次最多能查询近30天内的监控信息。|
|InvalidParameter.TooManyDataQueried|Too many data queried.|400|查询的数据量过多，每次最多查询400条监控数据。|
|Throttling|You have made too many requests within a short time; your request is denied due to request throttling.|400|请求被流控，请稍后再试。|

