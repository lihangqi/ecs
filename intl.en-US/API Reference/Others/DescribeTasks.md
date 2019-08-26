# DescribeTasks {#doc_api_Ecs_DescribeTasks .reference}

You can call this operation to query the progress of one or more asynchronous requests.

## Debugging {#apiExplorer .section}

Alibaba Cloud provides [OpenAPI Explorer](https://api.aliyun.com/#product=Ecs&api=DescribeTasks) to simplify API usage. You can use OpenAPI Explorer to search for APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|RegionId|String|Yes|cn-hangzhou|The ID of the region for which to query the progress of requests. You can call the [DescribeRegions](~~25609~~) operation to query the latest region list.

 |
|Action|String|No|DescribeTasks|The operation that you want to perform. For API requests using the HTTP and HTTPS methods, `Action` is required. Set the value to DescribeTasks.

 |
|EndTime|String|No|2015-11-23T15:16:00Z|The end of the time range where the data is queried. Specify the time in the [ISO 8601](~~25696~~) standard in the yyyy-MM-ddTHH:mm:ssZ format. The time must be in UTC.

 |
|PageNumber|Integer|No|1|The number of the page to return. Pages start from page 1. Default value: 1.

 |
|PageSize|Integer|No|2|The number of entries to return on each page. Valid values: 1 to 100. Default value: 10.

 |
|StartTime|String|No|2015-11-23T15:10:00Z|The beginning of the time range where the data is queried. Specify the time in the [ISO 8601](~~25696~~) standard in the yyyy-MM-ddTHH:mm:ssZ format. The time must be in UTC.

 |
|TaskAction|String|No|ImportImage|The operation name of the task. Valid values:

 -   ImportImage
-   ExportImage
-   RedeployInstance

 |
|TaskIds|String|No|\["t-bp10e8or\*\*\*\*\*\*\*\*74o8x","t-bp10e8or\*\*\*\*\*\*\*\*74o8y"\]|The task IDs. You can specify up to 100 task IDs at a time. Separate multiple tasks IDs with commas \(,\).

 |
|TaskStatus|String|No|Finished|The status of the task. Valid values:

 -   Finished
-   Processing
-   Waiting
-   Deleted
-   Paused
-   Failed

 Default value: null. The system only retrieves tasks in the Finished, Processing, and Failed states. The request ignores other values.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|PageNumber|Integer|1|The number of the page returned.

 |
|PageSize|Integer|2|The number of entries returned on the page.

 |
|RegionId|String|cn-hangzhou|The region ID.

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request.

 |
|TaskSet| | |A set of tasks.

 |
|└CreationTime|String|2015-11-24T12:50Z|The time when the task was created.

 |
|└FinishedTime|String|2015-11-24T12:50Z|The time when the task was finished.

 |
|└SupportCancel|String|true|Indicates whether the task can be canceled.

 |
|└TaskAction|String|IMPORT\_IMAGE|The name of the task.

 |
|└TaskId|String|t-bp10e8or\*\*\*\*\*\*\*\*74o8X|The ID of the task.

 |
|└TaskStatus|String|Finished|The status of the task.

 |
|TotalCount|Integer|2|The total number of tasks.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=DescribeTasks
&RegionId=cn-hangzhou
&PageNumber=1
&PageSize=2
&TaskIds=t-bp10e8or********74o8X
&TaskAction=ImportImage
&TaskStatus=Finished
&StartTime=2015-11-23T15:10:00Z
&EndTime=2015-11-23T15:16:00Z
&<Common request parameters>
```

Sample success responses

`XML` format

``` {#xml_return_success_demo}
<DescribeTasksResponse>
  <PageNumber>1</PageNumber>
  <TotalCount>2</TotalCount>
  <PageSize>2</PageSize>
  <RegionId>cn-hangzhou</RegionId>
  <RequestId>E5C82807-5588-4661-9A96-350B206A7623</RequestId>
  <TaskSet>
    <Task>
      <CreationTime>2015-11-24T12:50Z</CreationTime>
      <FinishedTime>2015-11-24T12:50Z</FinishedTime>
      <SupportCancel>true</SupportCancel>
      <TaskAction>IMPORT_IMAGE</TaskAction>
      <TaskStatus>Finished</TaskStatus>
      <TaskId>t-bp10e8or********74o8X</TaskId>
    </Task>
    <Task>
      <CreationTime>2015-11-23T15:10Z</CreationTime>
      <FinishedTime>2015-11-23T15:16Z</FinishedTime>
      <SupportCancel>true</SupportCancel>
      <TaskAction>IMPORT_IMAGE</TaskAction>
      <TaskStatus>Finished</TaskStatus>
      <TaskId>t-23sgu0dyj</TaskId>
    </Task>
  </TaskSet>
</DescribeTasksResponse>

```

`JSON` format

``` {#json_return_success_demo}
{
	"PageNumber":1,
	"TotalCount":2,
	"TaskSet":[
		{
			"Task":[
				{
					"CreationTime":"2015-11-24T12:50Z",
					"FinishedTime":"2015-11-24T12:50Z",
					"SupportCancel":true,
					"TaskAction":"ImportImage",
					"TaskStatus":"Finished",
					"TaskId":"t-bp10e8or********74o8X"
				},
				{
					"CreationTime":"2015-11-23T15:10Z",
					"FinishedTime":"2015-11-23T15:16Z",
					"SupportCancel":true,
					"TaskAction":"ImportImage",
					"TaskStatus":"Finished",
					"TaskId":"t-23sgu0dyj"
				}
			]
		}
	],
	"PageSize":2,
	"RequestId":"F746C690-D9EA-4F87-AF31-8E1910FAB541",
	"RegionId":"cn-hangzhou"
}
```

## Error codes { .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|400|MissingParameter|An input parameter "RegionId" that is mandatory for processing the request is not supplied.|The error message returned because the RegionId parameter is not specified.|
|400|InvalidRegionId.NotFound|The specified RegionId does not exist.|The error message returned because the specified Region ID does not exist. Check whether ECS is available in that region.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

