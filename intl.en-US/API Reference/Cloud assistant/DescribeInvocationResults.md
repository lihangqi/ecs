# DescribeInvocationResults {#doc_api_1030544 .reference}

Views the command output of a cloud assistant command in the specified ECS instance.

## Description {#description .section}

After you invoke a command, it may not succeed. You can call [DescribeInvocationResults](~~64845~~) to view the command output of command invocation. The command output shall prevail.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=DescribeInvocationResults) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|RegionId|String|Yes|cn-hangzhou| The ID of the region. You can call [DescribeRegions](~~25609~~) to view the latest regions of Alibaba Cloud.

 |
|Action|String|No|DescribeInvocationResults| The operation that you want to perform. Set the value to DescribeInvocationResults.

 |
|CommandId|String|No|c-4d34302d02424c5c8e10281e3a315a05| The ID of the command.

 |
|InstanceId|String|No|i-uf614fhehhzmxdqx| The ID of the instance.

 |
|InvokeId|String|No|t-7d2a745b412b4601b2d47f6a768d3a14| The invocation ID of the command. The invocation ID of the command process. You can call [DescribeInvocations](~~64840~~) to view the invocation IDs.

 |
|InvokeRecordStatus|String|No|Finished| The status of the command invocation.

 |
|PageNumber|Long|No|1| The current page number. Starting value: 1.

 Default value: 1.

 |
|PageSize|Long|No|5| The number of entries per page. Maximum value: 50.

 Default value: 10.

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|Invocation| | | The command invocation data.

 |
|└InvocationResults| | | The results of command invocation.

 |
|└CommandId|String|c-4d34302d02424c5c8e10281e3a315a05| The ID of the command.

 |
|└ ExitCode|Long|0| The exit code of the command process:

 -   For Linux-based instances, the exit code is the Shell process exit code.
-   For Windows-based instances, the exit code is the Bat or PowerShell process exit code.

 |
|└FinishedTime|String|2018-01-05 15:45:02| The time when the command process is completed. If a command process times out, the command completion time is subject to the TimedOut parameter specified in the [CreateCommand](~~64844~~) operation.

 |
|└InstanceId|String|i-uf614fhehhzmxdqx| The ID of the instance.

 |
|└InvokeId|String|t-7d2a745b412b4601b2d47f6a768d3a14| The invocation ID of the command. The invocation ID of the command process. You can call [DescribeInvocations](~~64840~~) to view the invocation IDs.

 |
|└InvokeRecordStatus|String|Finished| The status of the command invocation.

 |
|└Output|String|MTU6MzA6MDEK| The output of the command invocation, which is Base64-encoded.

 |
|└PageNumber|Long|1| The current page number. Starting value: 1.

 Default value: 1.

 |
|└PageSize|Long|5| The number of entries per page. Maximum value: 20.

 Default value: 10.

 |
|└TotalCount|Long|5| The total number of commands.

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=DescribeInvocationResults
&RegionId=cn-hangzhou 
&InvokeId=t-7d2a745b412b4601b2d47f6a768d3a14
&InstanceId=i-uf614fhehhzmxdqx
&CommandId=c-4d34302d02424c5c8e10281e3a315a05
&InvokeRecordStatus=Finished
&PageNumber=1 
&PageSize=5
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<DescribeInvocationResultsResponse>
    <TotalCount>5</TotalCount>
    <PageNumber>1</PageNumber> 
    <PageSize>5</PageSize>
    <InvocationResults> 
        <InvocationResult>
            <FinishedTime>2018-01-05 15:45:02</FinishedTime>
            <InstanceId>i-uf614fhehhzmxdqw</InstanceId>
            <Output>MTU6NDU6MDEK</Output>
	<InvokeRecordStatus> Finished<InvokeRecordStatus>
            <ExitCode>0</ExitCode>
        </InvocationResult>
        <InvocationResult>
            <FinishedTime>2018-01-05 15:40:02</FinishedTime>
            <InstanceId>i-uf614fhehhzmxdqw</InstanceId>
            <Output> </Output>
<InvokeRecordStatus> Finished<InvokeRecordStatus>
            <ExitCode>0</ExitCode>
        </InvocationResult>
        <InvocationResult>
            <FinishedTime>2018-01-05 15:30:02</FinishedTime>
            <InstanceId>i-uf614fhehhzmxdqw</InstanceId>
            <Output>MTU6MzA6MDEK</Output>
            <ExitCode>0</ExitCode>
        </InvocationResult>
        <InvocationResult>
            <FinishedTime>2018-01-05 15:20:02</FinishedTime>
            <InstanceId>i-uf614fhehhzmxdqw</InstanceId>
            <Output> </Output>
            <ExitCode>0</ExitCode>
        </InvocationResult>
        <InvocationResult>
            <FinishedTime>2018-01-05 15:15:02</FinishedTime>
            <InstanceId>i-uf614fhehhzmxdqw</InstanceId>
            <Output>MTU6MTU6MDEK</Output>
            <ExitCode>0</ExitCode>
        </InvocationResult>
        </InvocationResults>
<RequestId>"E69EF3CC-94CD-42E7-8926-F133B86387C0</RequestId> 
</DescribeInvocationResultsResponse> 
```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"E69EF3CC-94CD-42E7-8926-F133B86387C0",
	"Invocation":{
		"PageNumber":1,
		"TotalCount":5,
		"InvocationResults":{
			"InvocationResult":[
				{
					"InvokeRecordStatus":"Finished",
					"FinishedTime":"2018-01-05 15:45:02",
					"ExitCode":0,
					"InstanceId":"i-uf614fhehhzmxdqw",
					"Output":"MTU6NDU6MDEK"
				},
				{
					"InvokeRecordStatus":"Finished",
					"FinishedTime":"2018-01-05 15:40:02",
					"ExitCode":0,
					"InstanceId":"i-uf614fhehhzmxdqw",
					"Output":""
				},
				{
					"FinishedTime":"2018-01-05 15:30:02",
					"ExitCode":0,
					"InstanceId":"i-uf614fhehhzmxdqw",
					"Output":"MTU6MzA6MDEK"
				},
				{
					"FinishedTime":"2018-01-05 15:20:02",
					"ExitCode":0,
					"InstanceId":"i-uf614fhehhzmd3zj4k74",
					"Output":""
				},
				{
					"InvokeRecordStatus":"Finished",
					"FinishedTime":"2018-01-05 15:15:02",
					"ExitCode":0,
					"InstanceId":"i-uf614fhehhzmd3zj4k74",
					"Output":"MTU6MTU6MDEK"
				}
			]
		},
		"PageSize":5
	}
}
```

## Error codes {#section_fk2_prx_1n4 .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|500|InternalError.Dispatch|An error occurred when you dispatched the request.|The error message returned when an unknown error occurs.|
|403|InvalidParam.PageNumber|The specified parameter is invalid.|The error message returned when the specified parameter is invalid.|
|403|InvalidParam.PageSize|The specified parameter is invalid.|The error message returned when the specified parameter is invalid.|
|403|InvalidRegionId.CloudAssistant|Current region is not available.|The error message returned when the specified region is unavailable.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

