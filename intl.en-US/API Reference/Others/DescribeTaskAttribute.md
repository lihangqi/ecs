# DescribeTaskAttribute {#doc_api_1006031 .reference}

Views the details about asynchronous tasks. You can query the ImportImage and ExportImage tasks.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=DescribeTaskAttribute) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|RegionId|String|Yes|cn-hangzhou| The ID of the region. You can call [DescribeRegions](~~25609~~) to view the latest regions of Alibaba Cloud.

 |
|TaskId|String|Yes|t-taskid| The ID of the task. You can call DescribeTasks to obtain the list of task IDs.

 |
|Action|String|No|DescribeTaskAttribute| The operation that you want to perform. Set the value to DescribeTaskAttribute.

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|CreationTime|String|2015-11-23T02:13Z| The creation time of the task.

 |
|FailedCount|Integer|0| The number of failed tasks.

 |
|FinishedTime|String|2015-11-23T02:19Z| The completion time of the task.

 |
|OperationProgressSet| | | The returned task-related information such as the status of each subtask.

 |
|└ErrorCode|String|ParameterInvalid| The error code.

 |
|└ErrorMsg|String|The specified RegionId parameter is invalid.| Error message

 |
|└OperationStatus|String|Success| The status of the operation.

 |
|└RelatedItemSet| | | The type of the resource information.

 |
|└Name|String|OSSObject| The name of the related item.

 |
|└Value|String|MYOSSPRE\_m-23f8tcp8y\_t-23ym6mvro.vhd| The value of the related item.

 |
|RegionId|String|cn-hangzhou| The ID of the region.

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request.

 |
|SuccessCount|Integer|1| The number of tasks that were completed.

 |
|SupportCancel|String|true| Indicates whether the task can be canceled. Valid values:

 -   True
-   False

 |
|TaskAction|String|ExportImage| The operation name of the task.

 |
|TaskId|String|t-taskid| The ID of the task.

 |
|TaskProcess|String|100%| The progress of the task.

 |
|TaskStatus|String|Finished| The status of the task.

 |
|TotalCount|Integer|1| The total number of tasks.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=DescribeTaskAttribute
&RegionId=cn-hangzhou
&TaskId=t-taskid 
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<DescribeTaskAttributeResponse> 
  <CreationTime>2015-11-23T02:13Z</CreationTime> 
  <OperationProgressSet> 
    <OperationProgress> 
      <RelatedItemSet>
        <RelatedItem> 
          <Name>OSSBucket</Name> 
          <Value>image-temp</Value> 
        </RelatedItem>
        <RelatedItem> 
          <Name>OSSObject</Name> 
          <Value>MYOSSPRE_m-23f8tcp8y_t-23ym6mvro.vhd</Value> 
        </RelatedItem> 
        <RelatedItem> 
          <Name>ImageFormat</Name> 
          <Value>vhd</Value> 
        </RelatedItem> 
      </RelatedItemSet> 
      <ErrorMsg/> 
      <ErrorCode/> 
      <OperationStatus>Success</OperationStatus> 
    </OperationProgress>
  </OperationProgressSet> 
  <FinishedTime>2015-11-23T02:19Z</FinishedTime> 
  <FailedCount>0</FailedCount> 
  <SupportCancel>true</SupportCancel> 
  <TotalCount>1</TotalCount>
  <SuccessCount>1</SuccessCount> 
  <RequestId>EF0C5969-279B-49C8-AD83-BACCC74DD38C</RequestId> 
  <RegionId>cn-hangzhou</RegionId> 
  <TaskAction>ExportImage</TaskAction> 
  <TaskStatus>Finished</TaskStatus> 
  <TaskProcess>100%</TaskProcess> 
  <TaskId>t-23ym6mvro</TaskId> 
</DescribeTaskAttributeResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"OperationProgressSet":{
		"OperationProgress":[
			{
				"RelatedItemSet":{
					"RelatedItem":[
						{
							"Name":"OSSBucket",
							"Value":"image-temp"
						},
						{
							"Name":"OSSObject",
							"Value":"MYOSSPRE_m-23f8tcp8y_t-23ym6mvro.vhd"
						},
						{
							"Name":"ImageFormat",
							"Value":"vhd"
						}
					]
				},
				"ErrorMsg":"",
				"ErrorCode":"",
				"OperationStatus":"Success"
			}
		]
	},
	"FailedCount":0,
	"SupportCancel":true,
	"TotalCount":1,
	"TaskAction":"ExportImage",
	"TaskProcess":"100%",
	"TaskId":"t-23ym6mvro",
	"CreationTime":"2015-11-23T02:13Z",
	"FinishedTime":"2015-11-23T02:19Z",
	"SuccessCount":1,
	"RequestId":"4BE2C7FE-C7A4-4675-A153-174E032AABFB",
	"RegionId":"cn-hangzhou",
	"TaskStatus":"Finished"
}
```

## Error codes {#section_4y2_idt_jgz .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|400|InvalidRegionId.NotFound|The specified RegionId does not exist.|The error message returned when the specified Region ID does not exist. Check whether the service is available in this region.|
|400|MissingParameter|An input parameter "RegionId" that is mandatory for processing the request is not supplied.|The error message returned when the required RegionId parameter is not specified.|
|400|MissingParameter|An input parameter "TaskId" that is mandatory for processing the request is not supplied.|The error message returned when the TaskId parameter is not specified.|
|400|InvalidTaskId.NotFound|The specified "TaskId" is not found.|The error message returned when the specified task ID does not exist.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

