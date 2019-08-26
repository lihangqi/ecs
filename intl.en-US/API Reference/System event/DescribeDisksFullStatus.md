# DescribeDisksFullStatus {#doc_api_1063476 .reference}

Queries the full status information of one or more disks.

## Description {#description .section}

-   The full status information of a disk includes the disk lifecycle status \(Status\), disk health status \(HealthStatus\), and disk event type \(EventType\).
-   The disk-related event publishing time, scheduled event execution time, and actual event execution time are the same. If you specify a time period \[EventTime.Start,EventTime.End\], the system queries all events that occurred during this period. You can query events within the last seven days.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=DescribeDisksFullStatus) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|RegionId|String|Yes|cn-hangzhou| The ID of the region to which the disk belongs. You can call [DescribeRegions](~~25609~~) to view the latest regions of Alibaba Cloud.

 |
|Action|String|No|DescribeDisksFullStatus| The operation that you want to perform. Set the value to DescribeDisksFullStatus.

 |
|DiskId.N|RepeatList|No|d-disk1| The ID of the disk to be queried. Valid values of N: 1 to 100.

 |
|EventId.N|RepeatList|No|e-event1| The event ID. Valid values of N: 1 to 100.

 |
|EventTime.End|String|No|2018-05-08T02:48:52Z| The end time of events to be queried. The time follows the [ISO 8601](~~25696~~) standard and uses UTC time. The format is yyyy-MM-ddTHH:mm:ssZ.

 |
|EventTime.Start|String|No|2018-05-06T02:43:10Z| The start time of events to be queried. The time follows the [ISO 8601](~~25696~~) standard and uses UTC time. The format is yyyy-MM-ddTHH:mm:ssZ.

 |
|EventType|String|No|Stalled| The disk event type. Valid values:

 -   Degraded: The disk performance is degraded.
-   SeverelyDegraded: The disk performance is seriously degraded.
-   Stalled: The disk may be stalled with I/O suspended.

 |
|HealthStatus|String|No|Warning| The health status of the disk. Valid values:

 -   Impaired: The disk performance is damaged.
-   Warning: The disk performance may be degraded because of maintenance or technical issues.
-   Initializing: The instance is being initialized.
-   InsufficientData: The status cannot be determined because of insufficient data.
-   NotApplicable: Not applicable.

 |
|PageNumber|Integer|No|1| The page number of the query result. The value must be a positive integer.

 Default value: 1.

 |
|PageSize|Integer|No|10| The number of entries per page. Valid values: 1 to 100.

 Default value: 10.

 |
|Status|String|No|Available| The lifecycle status of the disk. For more information, see [Cloud disk status](~~25689~~). Valid values:

 -   In\_Use
-   Available
-   Attaching
-   Detaching
-   Creating
-   ReIniting

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|DiskFullStatusSet| | | An array of DiskFullStatus data.

 |
|└Device|String|/dev/xvdb| The device name of the disk that is attached to an instance, such as /dev/xvdb. It is null unless the disk is in the In\_use state.

 |
|└DiskEventSet| | | An array of DiskEvent data.

 |
|└EventEndTime|String|2018-05-06T02:48:52Z| The end time of the event.

 |
|└EventId|String|e-event1| The ID of the disk event.

 |
|└EventTime|String|2018-05-08T02:43:10Z| The occurrence time of the event.

 |
|└EventType| | | The event type.

 |
|└Code|Integer|7| The code of the event type.

 |
|└Name|String|Stalled| The name of the event type.

 |
|└DiskId|String|d-disk1| The ID of the disk.

 |
|└HealthStatus| | | The disk health status.

 |
|└Code|Integer|128| The code of the disk health status.

 |
|└Name|String|Impaired| The name of the disk health status.

 |
|└InstanceId|String|i-instance1| The ID of the instance.

 |
|└Status| | | The disk lifecycle status.

 |
|└Code|Integer|129| The code of the disk lifecycle status.

 |
|└Name|String|Available| The name of the disk lifecycle status.

 |
|PageNumber|Integer|1| The page number of the instance list.

 |
|PageSize|Integer|10| The number of entries per page.

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request.

 |
|TotalCount|Integer|2| The total number of instance statuses.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=DescribeDisksFullStatus
&RegionId=cn-hangzhou
&DiskId.1=d-disk1
&EventId.1=e-event1
&Status=Available
&HealthStatus=Warning
&EventType=Stalled
&EventTime.Start=2018-05-06T02:43:10Z
&EventTime.End=2018-05-08T02:48:52Z
&PageNumber=1 
&PageSize=10 
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
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

`JSON` format

``` {#json_return_success_demo}
{
	"PageNumber":1,
	"TotalCount":2,
	"PageSize":10,
	"RequestId":"1A8B4B27-8B2D-XXXX-XXXX-0F64DBE4C211",
	"DiskFullStatusSet":{
		"DiskFullStatusType":[
			{
				"Status":{
					"Name":"Available",
					"Code":129
				},
				"Device":"/dev/xvda",
				"HealthStatus":{
					"Name":"Impaired",
					"Code":128
				},
				"InstanceId":"i-instance1",
				"DiskEventSet":{
					"DiskEventType":[
						{
							"EventTime":"2018-05-08T02:43:10Z",
							"EventId":"e-event1",
							"EventType":{
								"Name":"Stalled",
								"Code":"7"
							}
						}
					]
				},
				"DiskId":"d-disk1"
			},
			{
				"Status":{
					"Name":"Available",
					"Code":129
				},
				"Device":"/dev/xvdb",
				"HealthStatus":{
					"Name":"Ok",
					"Code":0
				},
				"InstanceId":"i-instance2",
				"DiskEventSet":{
					"DiskEventType":[
						{
							"EventTime":"2018-05-06T02:43:10Z",
							"EventId":"e-event2",
							"EventType":{
								"Name":"Degraded",
								"Code":"1"
							},
							"EventEndTime":"2018-05-06T02:48:52Z"
						}
					]
				},
				"DiskId":"d-disk2"
			}
		]
	}
}
```

## Error codes {#section_fy3_yhe_h1i .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|404|MissingParameter|%s|The error message returned when a required parameter is not specified.|
|403|InvalidParameter|%s|The error message returned when the parameter format is invalid.|
|403|DiskIdLimitExceeded|%s|The error message returned when the specified instance IDs is more than 100.|
|403|EventIdLimitExceeded|%s|The error message returned when more than 100 simulated event IDs are specified.|
|403|InvalidParameter.TimeEndBeforeStart|%s|The error message returned when the end time is earlier than the start time.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

