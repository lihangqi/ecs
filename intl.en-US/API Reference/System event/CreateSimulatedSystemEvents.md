# CreateSimulatedSystemEvents {#doc_api_1006123 .reference}

Schedules simulated system events for one or more ECS instances. The simulated system events do not occur in the actual system and the simulation does not affect ECS instances.

## Description {#description .section}

You can use the ECS console, [ECS APIs](~~63962~~), or CloudMonitor to view the scheduled simulated system events.

The following table describes the lifecycle of a simulated system event.

-   Scheduled: The status for the simulated system event is automatically changed to Scheduled after it is scheduled.
-   Executed: The status for the simulated system event is automatically changed to Executed at the scheduled time specified by the NotBefore parameter if no manual intervention is involved.
-   Canceled: The status for the simulated system event is changed to Canceled if you cancel the event by calling [CancelSimulatedSystemEvents](~~88808~~).
-   Avoided: The status for the simulated system event of maintenance-triggered instance restart can be changed to Avoided if you [restart the instance](~~25502~~) before the scheduled time of the simulated system event. The maintenance-triggered instance restart is indicated by the SystemMaintenance.Reboot value.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=CreateSimulatedSystemEvents) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|EventType|String|Yes|SystemMaintenance.Reboot| The type of a system event. Valid values:

 -   SystemMaintenance.Reboot: The instance restarts due to maintenance.
-   SystemFailure.Reboot: The instance restarts due to a system failure.
-   InstanceFailure.Reboot: The instance restarts due to an instance failure.

 |
|InstanceId.N|RepeatList|Yes|i-instance1| The IDs of one or more ECS instances. Valid values of N: 1 to 100. You can specify multiple values in the form of a repeated list.

 |
|NotBefore|String|Yes|2018-12-01T06:32:31Z| The start time of the scheduled event execution period. The time follows the [ISO 8601](~~25696~~) standard and uses UTC time. The format is yyyy-MM-ddTHH:mm:ssZ.

 |
|RegionId|String|Yes|cn-hangzhou| The ID of the region. You can call [DescribeRegions](~~25609~~) to view the latest regions of Alibaba Cloud.

 |
|Action|String|No|CreateSimulatedSystemEvents| The operation that you want to perform. Set the value to CreateSimulatedSystemEvents.

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|EventIdSet| |e-xhskHun1256xxxx| The list of simulated event IDs.

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

https://ecs.aliyuncs.com/?Action=CreateSimulatedSystemEvents
&EventType=SystemMaintenance.Reboot 
&InstanceId.1=i-instance1
&NotBefore=2018-12-01T06:32:31Z 
&RegionId=cn-hangzhou 
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<CreateSimulatedSystemEventsResponse> 
  <EventIdSet> 
    <EventId>e-bp191hqye********34y</EventId> 
    <EventId>e-bp191hqye********34x</EventId> 
  </EventIdSet> 
  <RequestId>E69EF3CC-94CD-42E7-8926-F133B86387C0</RequestId> 
</CreateSimulatedSystemEventsResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
    "EventIdSet":{
        "EventId":[
            "e-bp191hqye********34y",
            "e-bp191hqye********34x"
        ]
    },
    "RequestId":"679E9056-9B75-4306-8A72-A1DF93EBEF74"
}
```

## Error codes {#section_za9_mjq_zlv .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|404|MissingParameter|%s|The error message returned when a required parameter is not specified.|
|403|InvalidParameter|%s|The error message returned when the parameter format is invalid.|
|403|InvalidNotBefore.Passed|%s|The error message returned when the specified value of the NotBefore parameter is earlier than the current time.|
|404|InvalidInstanceId.NotFound|%s|The error message returned when the specified instance does not exist.|
|403|SimulatedEventLimitExceeded|%s|The error message returned when the number of simulated events has reached the upper limit.|
|403|InstanceIdLimitExceeded|%s|The error message returned when the specified instance IDs is more than 100.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

