# ModifyCommand {#ModifyCommand .reference}

Modifies the parameters and content of a cloud assistant command.

## Description {#section_s4q_vr4_ydb .section}

-   You can modify a command during its invocation. After the modification, the new command content applies to subsequent invocations.
-   You cannot modify the command type. For example, you cannot change a Shell command \(`RunShellScript`\) to a Bat command \(`RunBatScript`\).

## Request parameters {#RequestParameter .section}

|Name|Type|Required|Description|
|:---|:---|:-------|:----------|
|Action|String|Yes|The name of this interface. Value: ModifyCommand.|
|RegionId|String|Yes|The region ID. For more information, call [DescribeRegions](reseller.en-US/API Reference/Regions/DescribeRegions.md#) to obtain the latest region list.|
|CommandId|String|Yes|Command ID. You can check all the available `CommandId` by calling the [DescribeCommands](reseller.en-US/API Reference/Cloud assistant/DescribeCommands.md#) API.|
|Name|String|No|Command name. Supporting all the character encoding sets.|
|Description|String|No|Command description. Supporting all the character encoding sets.|
|WorkingDir|String|No|The path where the command is performed.  Default value:-   For Linux instances, commands are performed in the `/root` directory.
-   For Windows instances, commands are performed in the directory where the [cloud assistant client](../../../../reseller.en-US/User Guide/Cloud Assistant Client.md#) process is located, such as `C:\ProgramData\aliyun\assist\$(version)`.

|
|TimeOut|Integer|No|The invocation timeout value of a command on ECS instances. The unit is seconds. When your command fails to run for some reason, the invocation may time out, after which the cloud assistant client forces the command process to stop by canceling the command PID. The parameter value must be greater than or equal to `60`. If the value is smaller than `60`, the timeout value is 60 seconds by default.Default value: 3600.

|

## Response parameters {#section_f54_lk5_xdb .section}

All parameters are common response parameters. For more information, see [Common parameters](reseller.en-US/API Reference/Getting started/Common parameters.md#commonResponseParameters).

## Examples { .section}

**Request parameters** 

```
https://ecs.aliyuncs.com/?Action=ModifyCommand
&RegionId=cn-hangzhou
&CommandId=c-e996287206324975b5fbe1dxxxxxxxxx
&NameId=Test
&TimeOut=120
<Common Request Parameters>
```

**Success response example** 

**XML format**

```
<ModifyCommandResponse>
    <RequestId>540CFF28-407A-40B5-B6A5-73Bxxxxxxxxx</RequestId>
</ModifyCommandResponse>
```

 **JSON format** 

```
{
        "RequestId":"540CFF28-407A-40B5-B6A5-73Bxxxxxxxxx",
}
```

**Error response example** 

**XML format**

```
<Error>
    <RequestId>540CFF28-407A-40B5-B6A5-74Bxxxxxxxxx</RequestId>
    <HostId>ecs.aliyuncs.com</HostId>
    <Code>InvalidInstance.NoClient</Code>
    <Message>The specified instances have no cloud assistant client installed.</Message>
</Error>
```

 **JSON format** 

```
{
        "RequestId": "540CFF28-407A-40B5-B6A5-74Bxxxxxxxxx",
        "HostId": "ecs.aliyuncs.com"
        "Code": "InvalidInstance.NoClient"
        "Message": "The specified instances have no cloud assistant client installed."
}
```

## Error codes {#ErrorCode .section}

|Error code|Error message|HTTP status code|Meaning|
|:---------|:------------|:---------------|:------|
|MissingParameter.CommandId|The input parameter “CommandId” that is mandatory for processing this request is not supplied.|400|You must specify the required parameter of `CommandId`.|
|MissingParameter.RegionId|The input parameter “RegionId” that is mandatory for processing this request is not supplied.|400|You must specify the required parameter of `RegionId`, or you cannot use the resources in the specified region \(`RegionId`\).|
|InvalidCmdId.NotFound|The specified CommandId does not exist.|404|The specified `CommandId` does not exist.|
|InvalidRegionId.NotFound|The RegionId provided does not exist in our items.|404|The specified `RegionId` does not exist.|
|InternalError.Dispatch|An internal error occurred when dispath the request.|500|Internal error. Please try again later.|

