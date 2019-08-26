# DescribeInstanceHistoryEvents {#doc_api_1033074 .reference}

Queries the system events of the specified instance. You can query system events within the last week. You can specify the InstanceEventCycleStatus parameter to query system events in the Scheduled or Executing status.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=DescribeInstanceHistoryEvents) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|RegionId|String|Yes|cn-hangzhou| The ID of the region where the ECS instance resides. You can call [DescribeRegions](~~25609~~) to view the latest regions of Alibaba Cloud.

 |
|Action|String|No|DescribeInstanceHistoryEvents| The operation that you want to perform. Set the value to DescribeInstanceHistoryEvents.

 |
|EventCycleStatus|String|No|Executed| The lifecycle status of a system event. The EventCycleStatus parameter is applicable only when the InstanceEventCycleStatus.N parameter is not specified. Valid values:

 -   Scheduled
-   Avoided
-   Executing
-   Executed
-   Canceled
-   Failed

 |
|EventId.N|RepeatList|No|e-2ze9yxxxxwtqcvai68rl| The IDs of one or multiple system events. Valid values of N: 1 to 100. Multiple values are displayed in a list.

 |
|EventPublishTime.End|String|No|2017-12-01T06:32:31Z| The end time of the period during which a system event is pushed. The time follows the [ISO 8601](~~25696~~) standard and uses UTC time. The format is yyyy-MM-ddTHH:mm:ssZ.

 |
|EventPublishTime.Start|String|No|2017-11-30T06:32:31Z| The start time of the period during which a system event is pushed. The time follows the [ISO 8601](~~25696~~) standard and uses UTC time. The format is yyyy-MM-ddTHH:mm:ssZ.

 |
|EventType|String|No|SystemMaintenance.Reboot| The system event type. The EventType parameter is applicable only when the InstanceEventType.N parameter is not specified. Valid values:

 -   SystemMaintenance.Reboot: The instance has been restarted due to system maintenance.
-   SystemFailure.Reboot: The instance has been restarted due to system failure.
-   InstanceFailure.Reboot: The instance has been restarted due to instance failure.
-   InstanceExpiration.Stop: The instance has been stopped due to subscription expiration.
-   InstanceExpiration.Delete: The instance has been released due to subscription expiration.
-   AccountUnbalanced.Stop: The instance has been stopped due to overdue payments.
-   AccountUnbalanced.Delete: The instance has been released due to overdue payments.

 |
|InstanceEventCycleStatus.N|RepeatList|No|Executed| The lifecycle status of one or multiple system events. Valid values of N: 1 to 6. Multiple values are displayed in a list. Valid values:

 -   Scheduled
-   Avoided
-   Executing
-   Executed
-   Canceled
-   Failed

 |
|InstanceEventType.N|RepeatList|No|SystemMaintenance.Reboot| The types of one or multiple system events. Valid values of N: 1 to 30. Multiple values are displayed in a list. Valid values:

 -   SystemMaintenance.Reboot: The instance has been restarted due to system maintenance.
-   SystemFailure.Reboot: The instance has been restarted due to system failure.
-   InstanceFailure.Reboot: The instance has been restarted due to instance failure.
-   InstanceExpiration.Stop: The instance has been stopped due to subscription expiration.
-   InstanceExpiration.Delete: The instance has been released due to subscription expiration.
-   AccountUnbalanced.Stop: The instance has been stopped due to overdue payments.
-   AccountUnbalanced.Delete: The instance has been released due to overdue payments.

 |
|InstanceId|String|No|i-myInstance| The ID of the instance. If no instance ID is specified, system events of all instances in the specified region will be queried.

 |
|NotBefore.End|String|No|2017-12-01T06:32:31Z| The end time of a period during which a system event is scheduled for execution. The time follows the [ISO 8601](~~25696~~) standard and uses UTC time. The format is yyyy-MM-ddTHH:mm:ssZ.

 |
|NotBefore.Start|String|No|2017-11-30T06:32:31Z| The start time of a period during which a system event is scheduled for execution. The time follows the [ISO 8601](~~25696~~) standard and uses UTC time. The format is yyyy-MM-ddTHH:mm:ssZ.

 |
|PageNumber|Integer|No|1| The page number of the query result. The parameter value is a positive integer.

 Default value: 1.

 |
|PageSize|Integer|No|10| The number of entries on each page. Valid values: 1 to 100.

 Default value: 10

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|InstanceSystemEventSet| | | The array of system events for the instance.

 |
|└EventCycleStatus| | | The lifecycle status of a system event.

 |
|└Code|Integer|0| The status code of a system event.

 |
|└Name|String|Executed| The status name of a system event.

 |
|└EventFinishTime|String|2017-12-01T06:35:31Z| The end time of a system event. The time follows the [ISO 8601](~~25696~~) standard and uses UTC time. The format is yyyy-MM-ddTHH:mm:ssZ.

 |
|└EventId|String|e-2ze9yxxxxwtqcvai68rx| The ID of a system event.

 |
|└EventPublishTime|String|2017-11-30T06:32:31Z| The time a system event is pushed. The time follows the [ISO 8601](~~25696~~) standard and uses UTC time. The format is yyyy-MM-ddTHH:mm:ssZ.

 |
|└EventType| | | The system event type.

 |
|└Code|Integer|34| The code of a system event type.

 |
|└Name|String|InstanceExpiration.Stop| The name of a system event type.

 |
|└ExtendedAttribute| | | The extended attributes of an event.

 |
|└Device|String|/dev/vda| The name of a local disk.

 |
|└DiskId|String|d-diskid1| The ID of a local disk.

 |
|└InstanceId|String|i-myInstance| The ID of the instance.

 |
|└NotBefore|String|2017-12-06T00:00:00Z| The scheduled time for the execution of a system event. The time follows the [ISO 8601](~~25696~~) standard and uses UTC time. The format is yyyy-MM-ddTHH:mm:ssZ.

 |
|PageNumber|Integer|1| The page number of the instance list.

 |
|PageSize|Integer|10| The number of entries per page.

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request.

 |
|TotalCount|Integer|2| The total number of instance states.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

https://ecs.aliyuncs.com/?Action=DescribeInstanceHistoryEvents
&RegionId=cn-hangzhou 
&InstanceId=i-myInstance
&EventId.1=e-2ze9yxxxxwtqcvai68rl
&InstanceEventCycleStatus. 1=Executed
&EventCycleStatus=Executed
&InstanceEventType.1=SystemMaintenance.Reboot
&EventType=SystemMaintenance.Reboot
&NotBefore.Start=2017-11-30T06:32:31Z
&NotBefore.End=2017-12-01T06:32:31Z
&EventPublishTime.Start=2017-11-30T06:32:31Z
&EventPublishTime.End=2017-12-01T06:32:31Z
&PageNumber=1
&PageSize=10
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
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

`JSON` format

``` {#json_return_success_demo}
{
	"PageNumber":1,
	"TotalCount":2,
	"PageSize":10,
	"RequestId":"02EA76D3-5A2A-44EB-XXXX-8901881D8707",
	"InstanceSystemEventSet":{
		"InstanceSystemEventType":[
			{
				"EventPublishTime":"2017-11-30T06:32:31Z",
				"NotBefore":"2017-12-01T06:32:31Z",
				"EventFinishTime":"2017-12-01T06:35:31Z",
				"InstanceId":"i-2ze3tphuqvc93cixxxx3",
				"EventId":"e-2ze9yxxxxwtqcvai68rl",
				"EventType":{
					"Name":"SystemMaintenance.Reboot",
					"Code":1
				},
				"EventCycleStatus":{
					"Name":"Executed",
					"Code":0
				}
			},
			{
				"EventPublishTime":"2017-11-29T06:32:31Z",
				"NotBefore":"2017-12-06T00:00:00Z",
				"EventFinishTime":"2017-12-05T12:35:31Z",
				"InstanceId":"i-2ze3tphuqvc93cixxxx3",
				"EventId":"e-2ze9yxxxxwtqcvai68r3", 
				"EventType":{
					"Name":"InstanceExpiration.Stop",
					"Code":34
				},
				"EventCycleStatus":{
					"Name":"Avoided",
					"Code":8
				}
			}
		]
	}
}
```

## Error codes {#section_oj9_na5_j1r .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|404|MissingParameter|%s|The error message returned when a required parameter is not specified.|
|403|InvalidParameter|%s|The error message returned when the parameter format is invalid.|
|403|EventIdLimitExceeded|%s|The error message returned when more than 100 events are specified.|
|403|InvalidParameter.TimeEndBeforeStart|%s|The error message returned when the end time is earlier the start time.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

