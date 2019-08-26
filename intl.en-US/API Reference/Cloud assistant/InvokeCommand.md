# InvokeCommand {#doc_api_1101312 .reference}

Triggers a cloud assistant command on one or more ECS instances.

## Description {#description .section}

-   You can call the InvokeCommand operation in a region up to 5000 times a day. To adjust the maximum number of daily calls, [submit a ticket](https://workorder-intl.console.aliyun.com/#/ticket/createIndex).
-   The target instance type must be [VPC](~~34217~~).
-   The target instance must be in the Running state.
-   The target instance must be pre-installed with the [cloud assistant client](~~64921~~).
-   Before you run PowerShell commands, make sure that the target Windows-based instance has the PowerShell feature configured.
-   One-time invocations will run the commands only once.
-   Periodic invocations will run the commands at the frequency specified by the Frequency parameter. The result of previous invocation does not affect the next invocation.
-   Periodic invocation can only be scheduled in UTC+8. If the system time of your ECS instances are not UTC+8, make sure that you have made adjustments to ensure that your commands are executed at the correct time. For more information, see [Time setting: Synchronize NTP servers and change time zone for Linux instances](~~92803~~) or [Time setting: Synchronize NTP servers for Windows instances](~~51890~~).
-   You can specify multiple ECS instances in this command. When one of these instances does not comply with the invocation conditions, you need to specify another instance.
-   Command invocations may fail because of target instance status exceptions, network exceptions, or cloud assistant client exceptions. If an invocation fails, no invocation information is generated.
-   If you added `EnableParameter=true` while creating a script, you should specify value for the variables in the InvokeCommand method.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=InvokeCommand) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|CommandId|String|Yes|c-e996287206324975b5fbe1dxxxxxxxxx| The ID of the command. You can call [DescribeCommands](~~64843~~) to view all available command IDs.

 |
|InstanceId.N|RepeatList|Yes|i-bp185dy2o3o6nxxxxxxx| The list of instances where the command need to be executed. You can specify up to 50 instance IDs in each request. Valid values of N: 1 to 50.

 |
|RegionId|String|Yes|cn-hangzhou| The ID of the region. You can call [DescribeRegions](~~25609~~) to view the latest regions of Alibaba Cloud.

 |
|Action|String|No|InvokeCommand| The operation that you want to perform. Set the value to InvokeCommand.

 |
|Frequency|String|No|0 \*/20 \* \* \* \*| The frequency at which a periodic task is invoked. The frequency cannot be less than 10 seconds. When the Timed parameter is set to True, you must specify the Frequency parameter. The value of this parameter is expressed in Cron. For more information, see [Cron expressions](~~64769~~).

 |
|Parameters|Json|No|\{"name":"Jack", "accessKey":"LTAIdyv\*\*\*\*\*\*aRY"\}|Specifies value for variables previsouly added in the script. The number of varaibles cannot be greater than 10. Use the format of `{"key":"value"}`to set the values. Note that: -   The key can support up to 64 characters, but it cannot be a null string.
-   The value can be a null string, which indicates that no values is set for this invocation.
-   After Base-64 encoded, the collective length of the Parameters and the CommandContent cannot exceed 16 KB.

 |
|Timed|Boolean|No|true| Indicates whether the command invocation is periodic. Default value: False.

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|InvokeId|String|t-7d2a745b412b4601b2d47f6a768d3a14| The invocation ID of the command.

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=InvokeCommand
&CommandId=c-e996287206324975b5fbe1dxxxxxxxxx 
&InstanceId.1=i-bp185dy2o3o6nxxxxxxx
&RegionId=cn-hangzhou
&Timed=true
&Frequency=0 */20 * * * * 
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<InvokeCommandResponse>
  <RequestId>E69EF3CC-94CD-42E7-8926-F133B86387C0</RequestId>
  <InvokeId>t-7d2a745b412b4601b2d47f6a768d3a14</InvokeId> 
</InvokeCommandResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"E69EF3CC-94CD-42E7-8926-F133B86387C0",
	"InvokeId":"t-7d2a745b412b4601b2d47f6a768d3a14"
}
```

## Error codes {#section_k38_85k_vwt .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|500|InternalError.Dispatch|An error occurred when you dispatched the request.|The error message returned when an unknown error occurs.|
|404|InvalidInstance.NotFound|The specified instance does not exist.|The error message returned when the specified instance does not exist.|
|403|MissingParam.Frequency|The frequency must be specified when you create a timed task.|The error message returned when no frequency is set for the periodic task.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

