# CancelTask {#doc_api_1000174 .reference}

Cancels a running task. You can cancel the running ImportImage and ExportImage tasks.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=CancelTask) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|RegionId|String|Yes|cn-hangzhou| The ID of the region. You can call [DescribeRegions](~~25609~~) to view the latest regions of Alibaba Cloud.

 |
|TaskId|String|Yes|t-23ym6mvro| The ID of the task. You can call [DescribeTasks](~~25622~~) to view the list of task IDs.

 |
|Action|String|No|CancelTask| The operation that you want to perform. Set the value to CancelTask.

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=CancelTask
&RegionId=cn-hangzhou
&TaskId=t-23ym6mvro
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<CancelTaskResponse> 
  <RequestId>4BE2C7FE-C7A4-4675-A153-174E032AABFB</RequestId> 
</CancelTaskResponse> 
```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"4BE2C7FE-C7A4-4675-A153-174E032AABFB"
}
```

## Error codes {#section_rl7_cst_sy9 .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|400|MissingParameter|An input parameter "RegionId" that is mandatory for processing the request is not supplied.|The error message returned when the RegionId parameter is not specified.|
|400|MissingParameter|An input parameter "TaskId" that is mandatory for processing the request is not supplied.|The error message returned when the TaskId parameter is null.|
|400|InvalidRegionId.NotFound|The specified RegionId does not exist.|The error message returned when the specified Region ID does not exist. Check whether the service is available in this region.|
|400|InvalidTaskId.NotFound|The specified "TaskId" is not found.|The error message returned when the specified task ID does not exist.|
|403|CancelTaskFailed|The task is failed to cancel, Please contact the administrator.|The error message returned when the system failed to cancel the task. Contact a system administrator.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

