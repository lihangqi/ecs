# DescribeDiskMonitorData {#doc_api_999554 .reference}

Queries the monitoring data of a specified disk. The monitoring data includes read IOPS, write IOPS, read bandwidth \(Byte/s\), write bandwidth \(Byte/s\), read latency \(ms\), and write latency \(ms\) of the disk. Some portion may be missing from the monitoring data information. This is because the system cannot obtain the relevant information, such as when the disk is not in the In\_Use state.

## Description {#description .section}

When you call this operation, note that:

-   You can only query monitoring information for the disks that are in the In\_use state. For more information, see [Basic cloud disk status](~~25689~~).
-   Up to 400 monitoring data entries can be returned at a time. If the value of \(EndTime - StartTime\)/Period is greater than 400, an error is returned.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=DescribeDiskMonitorData) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|DiskId|String|Yes|d-myDisk| The ID of the disk.

 |
|EndTime|String|Yes|2014-07-23T12:09:00Z| The end time of the query. The time format follows the [ISO 8601](~~25696~~) standard and uses UTC time. The format is yyyy-mm-ddThh:mm:ssZ. If the specified number of seconds \(ss\) is not 00, the time will be automatically rounded up to the next minute.

 |
|StartTime|String|Yes|2014-07-23T12:07:00Z| The start time of the query. The time format follows the [ISO 8601](~~25696~~) standard and uses UTC time. The format is yyyy-mm-ddThh:mm:ssZ. If the specified number of seconds \(ss\) is not 00, the time will be automatically rounded up to the next minute.

 |
|Action|String|No|DescribeDiskMonitorData| The operation that you want to perform. Set the value to DescribeDiskMonitorData.

 |
|Period|Integer|No|60| The granularity of the retrieved monitoring data. Unit: seconds. Valid values:

 -   60
-   600
-   3600

 Default value: 60.

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|MonitorData| | | A collection consisting of disk monitoring data.

 |
|└BPSRead|Integer|0| The system disk read bandwidth. Unit: Byte/s.

 |
|└BPSTotal|Integer|204| The system disk read and write bandwidth. Unit: Byte/s.

 |
|└BPSWrite|Integer|204| The system disk write bandwidth. Unit: Byte/s.

 |
|└DiskId|String|d-mydisk001| The ID of the disk.

 |
|└IOPSRead|Integer|0| The system disk read I/O operations. Unit: times/s.

 |
|└IOPSTotal|Integer|0| The system disk read and write I/O operations. Unit: times/s.

 |
|└ IOPSWrite|Integer|0| The system disk write I/O operations. Unit: times/s.

 |
|└LatencyRead|Integer|0| The read latency of the disk. Unit: Byte/s.

 |
|└LatencyWrite|Integer|0| The write latency of the disk. Unit: Byte/s.

 |
|└TimeStamp|String|2014-07-23T12:07:00Z| The time of the data query. The time format follows the [ISO 8601](~~25696~~) standard and uses UTC time. The format is yyyy-MM-ddTHH:mm:ssZ.

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request.

 |
|TotalCount|Integer|3| The total number of disk monitoring data entries.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=DescribeDiskMonitorData
&DiskId=d-myDisk
&EndTime=2014-07-23T12:09:00Z 
&StartTime=2014-07-23T12:07:00Z
&Period=60 
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<DescribeDiskMonitorDataResponse>
  <MonitorData> 
    <DiskMonitorData>
      <BPSRead>0</BPSRead>
      <BPSTotal>0</BPSTotal> 
      <BPSWrite>0</BPSWrite>
      <DiskId>d-23b3p4r8b</DiskId>
      <IOPSRead>0</IOPSRead>
      <IOPSTotal>0</IOPSTotal>
      <IOPSWrite>0</IOPSWrite>
      <TimeStamp>2014-07-23T12:07:00Z</TimeStamp>
    </DiskMonitorData>
    <DiskMonitorData>
      <BPSRead>0</BPSRead>
      <BPSTotal>204</BPSTotal>
      <BPSWrite>204</BPSWrite>
      <DiskId>d-23b3p4r8b</DiskId>
      <IOPSRead>0</IOPSRead>
      <IOPSTotal>0</IOPSTotal>
      <IOPSWrite>0</IOPSWrite>
      <TimeStamp>2014-07-23T12:08:00Z</TimeStamp>
    </DiskMonitorData>
    <DiskMonitorData>
      <BPSRead>0</BPSRead>
      <BPSTotal>819</BPSTotal>
      <BPSWrite>819</BPSWrite>
      <DiskId>d-23b3p4r8b</DiskId>
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

`JSON` format

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
				"DiskId":"d-23b3p4r8b"
			},
			{
				"TimeStamp":"2014-07-23T12:08:00Z",
				"BPSRead":0,
				"IOPSTotal":0,
				"IOPSRead":0,
				"BPSTotal":204,
				"BPSWrite":204,
				"IOPSWrite":0,
				"DiskId":"d-23b3p4r8b"
			},
			{
				"TimeStamp": "2014-07-23T12:09:00Z"
				"BPSRead":0,
				"IOPSTotal":0,
				"IOPSRead":0,
				"BPSTotal":819,
				"BPSWrite":819,
				"IOPSWrite":0,
				"DiskId":"d-23b3p4r8b"
			}
		]
	}
}
```

## Error codes {#section_3t9_994_7ba .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|400|InvalidInstanceType.NotSupportCredit|The InstanceType of the specified instance does not support credit.|The error message returned when the instance type does not support burstable instances.|
|400|InvalidParameter.EndTime|The specified parameter EndTime is earlier than StartTime.|The error message returned when the end time is earlier than the start time.|
|500|InternalError|The request processing has failed due to some unknown error, exception or failure.|The error message returned when an unknown error occurs.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

