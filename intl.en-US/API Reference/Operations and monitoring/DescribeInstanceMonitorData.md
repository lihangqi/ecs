# DescribeInstanceMonitorData {#doc_api_999425 .reference}

Queries all the monitoring data about an ECS instance. The returned monitoring data includes the CPU usage, received data traffic, sent data traffic, network traffic, and average bandwidth of the ECS instance. If some of the traffic data information is missing, it is because the system is unable to obtain the relevant information, such as when an instance is in the Stopped state.

## Description {#description .section}

When you call this operation, note that:

-   Up to 400 monitored data entries can be returned per query. If the value of \(EndTime - StartTime\)/Period is greater than 400, an error is returned.
-   You can only query the monitoring data in the last 30 days. If the value of the StartTime parameter is earlier than 30 days, an error is returned.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=DescribeInstanceMonitorData) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|EndTime|String|Yes|2014-10-30T08:00:00Z| The end time of the retrieved monitoring data: The time format follows the [ISO 8601](~~25696~~) standard and uses UTC time. The format is YYYY-MM-DDThh:mm:ssZ. If the specified number of seconds \(ss\) is not 00, the time will be automatically rounded up to the next minute.

 |
|InstanceId|String|Yes|i-instnace1| The ID of the instance.

 |
|StartTime|String|Yes|2014-10-29T23:00:00Z| The start time of the retrieved monitoring data. The time format follows the [ISO 8601](~~25696~~) standard and the UTC time is used. The format is YYYY-MM-DDThh:mm:ssZ. If the specified number of seconds \(ss\) is not 00, the time will be automatically rounded up to the next minute.

 |
|Action|String|No|DescribeInstanceMonitorData| The operation that you want to perform. Set the value to DescribeInstanceMonitorData.

 |
|Period|Integer|No|60| The interval of the retrieved monitoring data. Unit: seconds. Valid values:

 -   60
-   600
-   3600

 Default value: 60.

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|MonitorData| | | A collection consisting of instance monitoring data.

 |
|└BPSRead|Integer|1000| The system disk read bandwidth. Unit: Byte/s.

 |
|└BPSWrite|Integer|200| The system disk write bandwidth. Unit: Byte/s.

 |
|└CPU|Integer|2| The CPU utilization. Unit: percent \(%\).

 |
|└CPUAdvanceCreditBalance|Float|0.4| The excess credits consumed by the t5 instance.

 |
|└CPUCreditBalance|Float|120| The total credits of the t5 instance.

 |
|└CPUCreditUsage|Float|30| The number of credits consumed by the t5 instance.

 |
|└CPUNotpaidSurplusCreditUsage|Float|0.5| The unpaid excess credits.

 |
|└IOPSRead|Integer|1000| The system disk read I/O operations. Unit: times/s.

 |
|└IOPSWrite|Integer|200| The system disk write I/O operations. Unit: times/s.

 |
|└InstanceId|String|i-instnace1| The ID of the instance.

 |
|└InternetBandwidth|Integer|10| The Internet traffic of the instance. Unit: Kbit/s.

 |
|└InternetRX|Integer|122| The Internet traffic received by the instance at the time of traffic query. Unit: Kbit/s.

 |
|└InternetTX|Integer|343| The Internet traffic sent by the instance at the time of traffic query. Unit: Kbit/s.

 |
|└IntranetBandwidth|Integer|10| The intranet bandwidth of the instance. Unit: Kbit/s.

 |
|└IntranetRX|Integer|122| The intranet traffic received by the instance at the time of traffic query. Unit: Kbit/s.

 |
|└IntranetTX|Integer|343| The intranet traffic sent by the instance at the time of traffic query. Unit: Kbit/s.

 |
|└TimeStamp|String|2010-01-21T09:50:23Z| The time of traffic query. The time format follows the [ISO 8601](~~25696~~) standard and uses UTC time. The format is yyyy-MM-ddTHH:mm:ssZ.

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request. This parameter is returned regardless of whether the operation is successful.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=DescribeInstanceMonitorData
&EndTime=2014-10-30T08:00:00Z 
&InstanceId=i-instnace1
&StartTime=2014-10-29T23:00:00Z 
&Period=60 
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
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

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"C8B26B44-0189-443E-9816-D951F59623A9",
	"MonitorData":{
		"InstanceMonitorData":[
			{
				"IOPSRead":1000,
				"BPSWrite":200,
				"IntranetBandwidth":10,
				"IntranetTX":343,
				"IntranetRX":122,
				"InstanceId":"Bc0102-23xYm09",
				"InternetFlow":675,
				"CPU":0,
				"TimeStamp":"2010-01-21T09:50:23Z",
				"BPSRead":1000,
				"InternetRX":122,
				"IntranetFlow":675,
				"InternetBandwidth":10,
				"IOPSWrite":200,
				"InternetTX":343
			}
		]
	}
}
```

## Error codes {#section_mum_mlq_hw8 .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|400|InvalidStartTime.ValueNotSupported|The specified parameter StartTime is later than EndTime.|The error message returned when the end time is earlier than the start time.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

