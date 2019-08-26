# DescribeInvocations {#doc_api_1030424 .reference}

Views the invocation list and status of cloud assistant commands.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=DescribeInvocations) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|RegionId|String|Yes|cn-hangzhou| The ID of the region. You can call [DescribeRegions](~~25609~~) to view the latest regions of Alibaba Cloud.

 |
|Action|String|No|DescribeInvocations| The operation that you want to perform. Set the value to DescribeInvocations.

 |
|CommandId|String|No|c-4d34302d02424c5c8e10281e3a315a05| The ID of the command. You can call [DescribeCommands](~~64843~~) to view all available command IDs.

 |
|CommandName|String|No|Test1| The name of the command.

 |
|CommandType|String|No|RunShellScript| The type of the command.

 |
|InstanceId|String|No|i-uf614fhehhzxx| The ID of the instance. When you specify this parameter, the system queries all the invocations of the commands in the instance.

 |
|InvokeId|String|No|t-7d2a745b412b4601b2d47f6a768d3b53| The invocation ID of the command.

 |
|InvokeStatus|String|No|Finished| The overall invocation status of the command. The overall invocation status depends on the invocation status of command processes on all target instances. Valid values:

 -   Running: The command process is running.
    -   Periodic invocation: Before you manually stop a command on periodic invocation, the command process is always in the Running state.
    -   One-time execution: The overall invocation state is Running, as long as the command process is in the Running state in any target instance.
-   Finished: The invocation of the command process is completed.
    -   Periodic invocation: The command process can never be in the Finished state.
    -   One-time execution: When invocations of command processes on all the target instances is completed, the overall invocation state is Finished. Or when you manually stop invocations of the command processes on some target instances and command invocations on other target instances are completed, the overall invocation state is Finished.
-   Failed: The command invocation failed, timed out, or encountered other exceptions.
    -   Periodic invocation: The command process can never be in the Failed state.
    -   One-time execution: When invocations of the command processes on all the target instances failed, the overall invocation state is Failed.
-   PartialFailed: The invocations of part of command processes failed.
    -   Periodical invocation: The command process can never be in the PartialFailed state.
    -   One-time execution: The overall invocation state is PartialFailed when any command process is in the Failed state on any target instance.
-   Stopped: The command process is manually stopped.

 |
|PageNumber|Long|No|1| The current page number. Starting value: 1.

 Default value: 1.

 |
|PageSize|Long|No|10| The number of entries per page. Maximum value: 50.

 Default value: 10.

 |
|Timed|Boolean|No|true| Indicates whether the command invocation is periodic. Default value: False.

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|Invocations| | | An array of InvocationSetType data.

 |
|└CommandId|String|c-4d34302d02424c5c8e10281e3a315a05| The ID of the command.

 |
|└CommandName|String|Test1| The name of the command.

 |
|└CommandType|String|RunShellScript| The type of the command.

 |
|└Frequency|String|0 \*/20 \* \* \* \*| The invocation cycle of a periodic task. For more information about the value specifications, see [Cron expressions](~~64769~~).

 |
|└InvokeId|String|t-7d2a745b412b4601b2d47f6a768d3b53| The invocation ID of the command.

 |
|└InvokeInstances| | | An array of InvokeInstanceSetType data.

 |
|└InstanceId|String|i-uf614fhehhzxx| The ID of the instance.

 |
|└InstanceInvokeStatus|String|Finished| The command process status in the specified instance.

 -   Running: The command process is running.
    -   Periodic invocation: Before you manually stop a command on periodic invocation, the command process is always in the Running state.
    -   One-time execution: The command process state in the specified instance is Running.
-   Finished: The invocation of the command process is completed.
    -   Periodic invocation: The command process can never be in the Finished state.
    -   One-time execution: The command process state in the specified instance is Finished.
-   Failed: The command invocation failed, timed out, or encountered other exceptions.
    -   Periodic invocation: The command process can never be in the Failed state.
    -   One-time execution: The command process state in the specified instance is Failed.
-   Stopped: The command process is manually stopped.

 |
|└InvokeStatus|String|Finished| The overall invocation status of the specified commands. The overall invocation status depends on the invocation status of command processes on all target instances. Valid values:

 -   Running: The command process is running.
    -   Periodic invocation: Before you manually stop a command on periodic invocation, the command process is always in the Running state.
    -   One-time execution: The overall invocation state is Running, as long as the command process is in the Running state in any target instance.
-   Finished: The invocation of the command process is completed.
    -   Periodic invocation: The command process can never be in the Finished state.
    -   One-time execution: When invocations of command processes on all the target instances are completed, the overall invocation state is Finished. Or when you manually stop invocations of command processes on some target instances and the invocations on other target instances is completed, the overall invocation state is Finished.
-   Failed: The command invocation failed, timed out, or encountered other exceptions.
    -   Periodic invocation: The command process can never be in the Failed state.
    -   One-time execution: When invocations of command processes on all the target instances failed, the overall invocation state is Failed.
-   PartialFailed: The invocations of part of command processes failed.
    -   Periodical invocation: The command process can never be in the PartialFailed state.
    -   One-time execution: The overall invocation state is PartialFailed when any command process is in the Failed state in any target instance.
-   Stopped: The command process is manually stopped.

 |
|└Timed|Boolean|false| Indicates whether the command invocation is periodic.

 |
|PageNumber|Long|1| The page number of the query result.

 |
|PageSize|Long|10| The number of entries per page.

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request.

 |
|TotalCount|Long|2| The total number of commands.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=DescribeInvocations
&RegionId=cn-hangzhou 
&InvokeId=t-7d2a745b412b4601b2d47f6a768d3b53
&CommandId=c-4d34302d02424c5c8e10281e3a315a05
&CommandName=Test1
&CommandType=RunShellScript 
&Timed=true 
&InvokeStatus=Finished
&InstanceId=i-uf614fhehhzxx 
&PageNumber=1 
&PageSize=10 
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<DescribeInvocationsResponse> 
  <TotalCount>2</TotalCount> 
  <PageNumber>1</PageNumber> 
  <PageSize>10</PageSize> 
  <Invocations>
    <Invocation>
      <InvokeStatus>Running</InvokeStatus>
      <InvokeId>t-7d2a745b412b4601b2d47f6a768d3b53</InvokeId> 
      <CommandName>Test1</CommandName> 
      <CommandType>RunShellScript</CommandType> 
      <Frequency>0 */20 * * * *</Frequency>
      <InvokeInstances>
        <InvokeInstance>
          <InstanceId>i-uf614fhehhzmx</InstanceId>
          <InstanceInvokeStatus>Finished</InstanceInvokeStatus>
        </InvokeInstance>
        <InvokeInstance>
          <InstanceId>i-uf614fhehhzmy</InstanceId>
          <InstanceInvokeStatus>Running</InstanceInvokeStatus>
        </InvokeInstance>
      </InvokeInstances>
      <Timed>True</Timed>
      <CommandId>c-7d2a745b412b4601b2d47f6a768d3a14</CommandId>
    </Invocation>
    <Invocation>
      <InvokeStatus>Finished</InvokeStatus>
      <InvokeId>t-7d2a745b412b4601b2d47f6a768d3b55</InvokeId>
      <CommandName>Test3</CommandName>
      <CommandType>RunShellScript</CommandType>
      <Frequency/>
      <InvokeInstances>
        <InvokeInstance>
          <InstanceId>i-uf614fhehhzmx</InstanceId>
          <InstanceInvokeStatus>Finished</InstanceInvokeStatus>
        </InvokeInstance>
        <InvokeInstance>
          <InstanceId>i-uf64isakb713x</InstanceId>
          <InstanceInvokeStatus>Finished</InstanceInvokeStatus>
        </InvokeInstance>
      </InvokeInstances>
      <Timed>False</Timed>
      <CommandId>c-7d2a745b412b4601b2d47f6a768d3a16</CommandId>
    </Invocation>
  </Invocations>
  <RequestId>E69EF3CC-94CD-42E7-8926-F133B86387C0</RequestId> 
</DescribeInvocationsResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"PageNumber":1,
	"Invocations":{
		"Invocation":[
			{
				"CommandType":"RunShellScript",
				"CommandName":"Test1",
				"InvokeStatus":"Running",
				"InvokeId":"t-7d2a745b412b4601b2d47f6a768d3b53",
				"CommandId":"c-7d2a745b412b4601b2d47f6a768d3a14",
				"Timed":true,
				"InvokeInstances":{
					"InvokeInstance":[
						{
							"InstanceInvokeStatus":"Finished",
							"InstanceId":"i-uf614fhehhzmx"
						},
						{
							"InstanceInvokeStatus":"Running",
							"InstanceId":"i-uf64isakb713x"
						}
					]
				},
				"Frequency":"0 */20 * * * *"
			},
			{
				"CommandType":"RunShellScript",
				"CommandName":"Test3",
				"InvokeStatus":"Finished",
				"InvokeId":">t-7d2a745b412b4601b2d47f6a768d3b55",
				"CommandId":"c-7d2a745b412b4601b2d47f6a768d3a16",
				"Timed":false,
				"InvokeInstances":{
					"InvokeInstance":[
						{
							"InstanceInvokeStatus":"Finished",
							"InstanceId":"i-uf614fhehhzmx"
						},
						{
							"InstanceInvokeStatus":"Finished",
							"InstanceId":"i-uf64isakb713x"
						}
					]
				}
			}
		]
	},
	"TotalCount":2,
	"PageSize":10,
	"RequestId":"E69EF3CC-94CD-42E7-8926-F133B86387C0"
}
```

## Error codes {#section_iu0_8gj_7g2 .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|500|InternalError.Dispatch|An error occurred when you dispatched the request.|The error message returned when an unknown error occurs.|
|403|InvalidParam.PageNumber|The specified parameter is invalid.|The error message returned when the specified parameter is invalid.|
|403|InvalidParam.PageSize|The specified parameter is invalid.|The error message returned when the specified parameter is invalid.|
|403|InvalidRegionId.CloudAssistant|Current region is not available.|The error message returned when the specified region is unavailable.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

