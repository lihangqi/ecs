# CancelSimulatedSystemEvents {#doc_api_1000143 .reference}

Cancels one or more simulated system events that are in the Scheduled or Executing state. After you cancel a simulated system event, the simulated event is in the Canceled state.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=CancelSimulatedSystemEvents) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|EventId.N|RepeatList|Yes|e-xhskHun1256xxxx| The IDs of one or multiple system events. Valid values of N: 1 to 100. You can specify multiple values in the form of a repeated list.

 |
|RegionId|String|Yes|cn-hangzhou| The ID of the region. You can call [DescribeRegions](~~25609~~) to view the latest regions of Alibaba Cloud.

 |
|Action|String|No|CancelSimulatedSystemEvents| The operation that you want to perform. Set the value to CancelSimulatedSystemEvents.

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=CancelSimulatedSystemEvents
&EventId. 1=e-xhskHun1256xxxx
&RegionId=cn-hangzhou 
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<CancelSimulatedSystemEventsResponse> 
  <RequestId>E69EF3CC-94CD-42E7-8926-F133B86387C0</RequestId> 
</CancelSimulatedSystemEventsResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"E69EF3CC-94CD-42E7-8926-F133B86387C0"
}
```

## Error codes {#section_39y_f6b_3so .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|404|MissingParameter|%s|The error message returned when a required parameter is not specified.|
|403|InvalidParameter|%s|The error message returned when the parameter format is invalid.|
|403|CannotCancelSystemEvent.NotSimulated|%s|The error message returned when you cancel a non-simulated system event.|
|403|InvalidEventId.NotFound|%s|The error message returned when the specified EventId does not exist.|
|400|EventIdLimitExceeded|%s|The error message returned when more than 100 simulated event IDs are specified.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

