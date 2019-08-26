# CreateCommand {#doc_api_1105959 .reference}

Creates a cloud assistant command.

## Description {#description .section}

-   You can create commands of the following types:
    -   Bat scripts for Windows-based instances \(RunBatScript\)
    -   PowerShell scripts for Windows-based instances \(RunPowerShellScript\)
    -   Shell scripts for Linux-based instances \(RunShellScript\)
-   You can specify the TimeOut parameter to set the maximum timeout period for command invocations on ECS instances. When a command invocation times out, the [cloud assistant client](~~64921~~) will force the command process to stop.
    -   For one-time invocation: After an invocation times out, the state of the command invocation \([InvokeRecordStatus](~~64845~~)\) on the specified ECS instance becomes Failed.
    -   For periodic invocation:
        -   The timeout period of periodic invocation is effective for every invocation record.
        -   After an invocation times out, the state of the invocation record \([InvokeRecordStatus](~~64845~~)\) becomes Failed.
        -   The timeout of last invocation does not affect the next invocation.
-   You can use the WorkingDir parameter to specify the invocation path of the command. For Linux-based instances, the default path is /root. For Windows-based instances, the default path is the one where the cloud assistant client process is located, such as C:\\ProgramData\\aliyun\\assist\\$\(version\).
-   You can enable variables in a script by setting EnableParameter to true. Cloud assistant supports the format of `{{&(parameter)}}` in the CommandContent parameter, while you run the script via the InvokeCommand method, you can enter the value of variables. Imagine that you create a script of `echo {{name}}`, then you can set the Parameter to <name,Jack\> and the like in the InvokeCommand method, in the actual invocation, the cloud assistant uses `echo Jack`.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=CreateCommand) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|CommandContent|String|Yes|ZWNobyAxMjM=| The Base64-encoded content of the command. When you specify the Type parameter, you must specify this parameter. The parameter value must be Base64-encoded for transmission, and the size of the script after the Base64 encoding cannot exceed 16 KB.

 |
|Name|String|Yes|Test| The name of the command, which supports all the character sets. It can be a maximum of 128 characters in length.

 |
|RegionId|String|Yes|cn-hangzhou| The ID of the region. You can call [DescribeRegions](~~25609~~) to view the latest regions of Alibaba Cloud.

 |
|Type|String|Yes|RunShellScript| The type of the command. Valid values:

 -   RunBatScript: Bat script for Windows-based instances
-   RunPowerShellScript: PowerShell script for Windows-based instances
-   RunShellScript: Shell script for Linux-based instances

 |
|Action|String|No|CreateCommand| The operation that you want to perform. Set the value to CreateCommand.

 |
|Description|String|No|Test1| The description of the command, which supports all character sets. It can be a maximum of 512 characters in length.

 |
|EnableParameter|Boolean|No|false|Whether to use variables in a script or not. Default value: false.|
|Timeout|Long|No|3600| The value of the invocation timeout period of a command on ECS instances. Unit: seconds. When the command fails to run, the invocation times out, and the cloud assistant client forces to terminate the command process afterward.

 Default value: 3600.

 |
|WorkingDir|String|No|/home/| The directory where the created command runs on the ECS instances. Default value:

 -   For Linux-based instances, the default path is /root.
-   For Windows-based instances, the default path is the one where the cloud assistant client process is located, such as C:\\ProgramData\\aliyun\\assist\\$\(version\).

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|CommandId|String|c-7d2a745b412b4601b2d47f6a768d3a14| The ID of the command.

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=CreateCommand
&CommandContent=ZWNobyAxMjM= 
&Name=test
&RegionId=cn-hangzhou 
&Type=RunShellScript 
&Description=Test1
&WorkingDir=/home/
&Timeout=3600
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<CreateCommandResponse>
  <RequestId>E69EF3CC-94CD-42E7-8926-F133B86387C0</RequestId> 
  <CommandId>c-7d2a745b412b4601b2d47f6a768d3a14</CommandId>
</CreateCommandResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"E69EF3CC-94CD-42E7-8926-F133B86387C0",
	"CommandId":"c-7d2a745b412b4601b2d47f6a768d3a14"
}
```

## Error codes {#section_y1o_u9a_ges .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|500|InternalError.Dispatch|An error occurred when you dispatched the request.|The error message returned when an unknown error occurs.|
|403|InvalidCmdType.NotFound|The specified command type does not exist.|The error message returned when the specified command type does not exist.|
|403|CmdName.ExceedLimit|The length of the command name exceeds the upper limit.|The error message returned when the command name exceeds the maximum length. Use a shorter command name.|
|403|CmdDesc.ExceedLimit|The length of the command description exceeds the upper limit.|The error message returned when the command description exceeds the maximum length. Use a shorter command description.|
|403|CmdCount.ExceedQuota|The total number of commands in the current region exceeds the quota.|The error message returned when the number of cloud assistant commands in the region exceeds the upper limit.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

