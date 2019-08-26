# DescribeDiskMonitorData {#doc_api_Ecs_DescribeDiskMonitorData .reference}

调用DescribeDiskMonitorData查询一块云盘指定时间内的使用信息。可查询云盘实用信息包括读IOPS、写IOPS、读带宽（Bps）、写带宽（Bps）、读时延（μs）以及写时延（μs）。若查询的信息中出现内容缺失，是因为我们无法获取该段时间的使用信息，即云盘状态不是使用中（In\_Use）。

## 接口说明 {#description .section}

调用该接口时，您需要注意：

-   只能查询状态为使用中（In\_Use）的云盘使用信息。更多详情，请参见[普通云盘状态表](~~25689~~)。
-   一次最多返回400条数据，即指定的（EndTime–StartTime）/Peroid需要小于等于400。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=DescribeDiskMonitorData&type=RPC&version=2014-05-26)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|DiskId|String|是|d-myDisk|云盘ID。

 |
|EndTime|String|是|2014-07-23T12:09:00Z|数据的结束时间。按照[ISO8601](~~25696~~)标准表示，并使用UTC +0时间，格式为yyyy-MM-ddTHH:mm:ssZ。如果秒（ss）不是00，则自动取为下一分钟开始时。

 |
|StartTime|String|是|2014-07-23T12:07:00Z|数据的起始时间。按照[ISO8601](~~25696~~)标准表示，并使用UTC +0时间，格式为yyyy-MM-ddTHH:mm:ssZ。如果秒（ss）不是00，则自动取为下一分钟开始时。

 |
|Action|String|否|DescribeDiskMonitorData|系统规定参数。取值：DescribeDiskMonitorData

 |
|Period|Integer|否|60|数据的精度，单位为秒。取值范围：

 -   60
-   600
-   3600

 默认值：60

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|MonitorData| | |云盘的监控数据集合。

 |
|BPSRead|Integer|0|系统盘读带宽，单位：Byte/s

 |
|BPSTotal|Integer|204|系统盘读写总带宽，单位：Byte/s

 |
|BPSWrite|Integer|204|系统盘写带宽，单位：Byte/s

 |
|DiskId|String|d-mydisk001|云盘ID。

 |
|IOPSRead|Integer|0|系统盘I/O读操作，单位：次/s

 |
|IOPSTotal|Integer|0|系统盘I/O读写总操作，单位：次/s

 |
|IOPSWrite|Integer|0|系统盘I/O写操作，单位：次/s

 |
|LatencyRead|Integer|0|云盘读时延。单位：μs（微秒）

 |
|LatencyWrite|Integer|0|云盘写时延。单位：μs（微秒）

 |
|TimeStamp|String|2014-07-23T12:07:00Z|查询监控信息的时间戳。按照[ISO8601](~~25696~~)标准表示，并使用UTC +0时间，格式为yyyy-MM-ddTHH:mm:ssZ。

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。

 |
|TotalCount|Integer|3|云盘使用信息的返回条目数量。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=DescribeDiskMonitorData
&DiskId=d-myDisk
&EndTime=2014-07-23T12:09:00Z
&StartTime=2014-07-23T12:07:00Z
&Period=60
&<公共请求参数>
```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeDiskMonitorDataResponse>
          <MonitorData>
                    <DiskMonitorData>
                              <BPSRead>0</BPSRead>
                              <BPSTotal>0</BPSTotal>
                              <BPSWrite>0</BPSWrite>
                              <DiskId>d-23b3p4r**</DiskId>
                              <IOPSRead>0</IOPSRead>
                              <IOPSTotal>0</IOPSTotal>
                              <IOPSWrite>0</IOPSWrite>
                              <TimeStamp>2014-07-23T12:07:00Z</TimeStamp>
                    </DiskMonitorData>
                    <DiskMonitorData>
                              <BPSRead>0</BPSRead>
                              <BPSTotal>204</BPSTotal>
                              <BPSWrite>204</BPSWrite>
                              <DiskId>d-23b3p4r**</DiskId>
                              <IOPSRead>0</IOPSRead>
                              <IOPSTotal>0</IOPSTotal>
                              <IOPSWrite>0</IOPSWrite>
                              <TimeStamp>2014-07-23T12:08:00Z</TimeStamp>
                    </DiskMonitorData>
                    <DiskMonitorData>
                              <BPSRead>0</BPSRead>
                              <BPSTotal>819</BPSTotal>
                              <BPSWrite>819</BPSWrite>
                              <DiskId>d-23b3p4r**</DiskId>
                              <IOPSRead>0</IOPSRead>
                              <IOPSTotal>0</IOPSTotal>
                              <IOPSWrite>0</IOPSWrite>
                              <TimeStamp>2014-07-23T12:09:00Z</TimeStamp>
                    </DiskMonitorData>
          </MonitorData>
          <RequestId>BF666447-B171-4076-BCBA-48437C18FD76</RequestId>
          <TotalCount>3</TotalCount>
</DescribeDiskMonitorDataResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"TotalCount":3,
	"RequestId":"A48A0A77-34F5-4C33-9066-9E8D2DA0D8E2",
	"MonitorData":{
		"DiskMonitorData":[
			{
				"TimeStamp":"2014-07-23T12:07:00Z",
				"BPSRead":0,
				"IOPSTotal":0,
				"IOPSRead":0,
				"BPSTotal":0,
				"BPSWrite":0,
				"IOPSWrite":0,
				"DiskId":"d-23b3p4r**"
			},
			{
				"TimeStamp":"2014-07-23T12:08:00Z",
				"BPSRead":0,
				"IOPSTotal":0,
				"IOPSRead":0,
				"BPSTotal":204,
				"BPSWrite":204,
				"IOPSWrite":0,
				"DiskId":"d-23b3p4r**"
			},
			{
				"TimeStamp":"2014-07-23T12:09:00Z",
				"BPSRead":0,
				"IOPSTotal":0,
				"IOPSRead":0,
				"BPSTotal":819,
				"BPSWrite":819,
				"IOPSWrite":0,
				"DiskId":"d-23b3p4r**"
			}
		]
	}
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|404|InvalidDiskId.NotFound|The DiskId provided does not exist in our records.|指定的磁盘不存在。请您检查磁盘 ID 是否正确。|
|400|InvalidStartTime.Malformed|The specified parameter "StartTime" is not valid.|指定的开始时间格式不合法。|
|400|InvalidEndTime.Malformed|The specified parameter "EndTime" is not valid.|指定的结束时间格式不合法。|
|400|InvalidPeriod.ValueNotSupported|The specified parameter "Period" is not valid.|指定的 Period 参数不合法。|
|400|InvalidStartTime.TooEarly|The specified parameter "StartTime" is too early.|指定的开始时间太早。|
|400|InvalidParameter.TooManyDataQueried|Too many data queried.|监控数据节点超出范围。|
|400|Throttling|Request was denied due to request throttling.|当前的操作太过频繁，请稍后重试。|
|400|InvalidInstanceType.NotSupportCredit|The InstanceType of the specified instance does not support credit.|实例规格不支持突发性能实例。|
|400|InvalidParameter.EndTime|The specified parameter EndTime is earlier than StartTime.|结束时间不得早于开始时间。|
|500|InternalError|The request processing has failed due to some unknown error, exception or failure.|发生未知错误。|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

