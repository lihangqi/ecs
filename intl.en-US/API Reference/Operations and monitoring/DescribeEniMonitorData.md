# DescribeEniMonitorData {#doc_api_1006116 .reference}

Queries traffic data information about a secondary ENI over a specific period.

## Description {#description .section}

The traffic data information includes intranet inbound and outbound traffic, the number of packets sent and received by the secondary ENI, and the number of packets discarded by the secondary ENI. If some content in the returned information is missing, it is possible that the system did not obtain the corresponding information. For example, the traffic data information on the secondary ENI cannot be queried if the instance is in the Stopped state. Data also cannot be queried if the secondary ENI is not attached to an instance and in the Available state. When you call this operation, note that:

-   Up to 400 monitored data entries can be returned per query. If the value of \(EndTime and StartTime\)/Period is greater than 400, an error is returned.
-   You can only query the monitored data in the last 30 days. If the value of the StartTime parameter is earlier than 30 days, an error is returned.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=DescribeEniMonitorData) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|EndTime|String|Yes|2018-05-21T12:22:00Z| The end time of the retrieved data. The time follows the [ISO 8601](~~25696~~) standard and uses UTC time. The format is yyyy-MM-ddTHH:mm:ssZ. If the specified number of seconds \(ss\) is not 00, the time will be automatically rounded up to the next minute.

 |
|InstanceId|String|Yes|myInstance| The ID of the instance to which the secondary ENI is bound.

 |
|RegionId|String|Yes|cn-hangzhou| The ID of the region. You can call [DescribeRegions](~~25609~~) to view the latest regions of Alibaba Cloud.

 |
|StartTime|String|Yes|2018-05-21T12:19:00Z| The start time of the retrieved data. The time follows the [ISO 8601](~~25696~~) standard and uses UTC time. The format is yyyy-MM-ddTHH:mm:ssZ. If the specified number of seconds \(ss\) is not 00, the time will be automatically rounded up to the next minute.

 |
|Action|String|No|DescribeEniMonitorData| The operation that you want to perform. Set the value to DescribeEniMonitorData.

 |
|EniId|String|No|eni-myENI| The ID of the secondary ENI. All secondary ENIs that are bound to the instance are queried by default.

 |
|Period|Integer|No|60| The interval of the retrieved data. Unit: seconds. Valid values:

 -   60
-   600
-   3600

 Default value: 60.

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|MonitorData| | | An array of EniMonitorDataType data.

 |
|└DropPacketRx|String|0| The discarded intranet data packets received by the secondary ENI. Unit: packets.

 |
|└DropPacketTx|String|0| The discarded intranet data packets sent by the secondary ENI. Unit: packets.

 |
|└EniId|String|eni-myENI| The ID of the secondary ENI.

 |
|└IntranetRx|String|0| The intranet data traffic received by the secondary ENI. Unit: Kbit/s.

 |
|└IntranetTx|String|0| The intranet data traffic sent by the secondary ENI. Unit: Kbit/s.

 |
|└PacketRx|String|0| The intranet data traffic packets received by the secondary ENI. Unit: packets.

 |
|└PacketTx|String|0| The intranet data packets sent by the secondary ENI. Unit: packets.

 |
|└TimeStamp|String|2018-05-21T03:22:00Z| The timestamp of traffic query. The time follows the [ISO 8601](~~25696~~) standard and uses UTC time. The format is yyyy-MM-ddTHH:mm:ssZ.

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request.

 |
|TotalCount|Integer|4| The total number of returned entries.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=DescribeEniMonitorData
&EndTime=2018-05-21T12:22:00Z
&InstanceId=myInstance
&RegionId=cn-hangzhou 
&StartTime=2018-05-21T12:19:00Z
&EniId=eni-myENI
&Period=60 
&<Common request parameters>
```

Successful response examples

`XML` format

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

`JSON` format

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

## Error codes {#section_8wh_6ec_7od .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|403|InvalidInstanceType.NotSupportCredit|The InstanceType of the specified instance does not support credit.|The error message returned when the instance type does not support burstable instances.|
|403|InvalidParameter.EndTime|The specified parameter EndTime is earlier than StartTime.|The error message returned when the end time is earlier than the start time.|
|4,003|InvalidParam.Malformed|The specified parameter "EniId" and "InstanceId" are not valid|The error message returned when the specified parameter is invalid.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

