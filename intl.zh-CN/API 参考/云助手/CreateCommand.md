# CreateCommand {#CreateCommand .reference}

新建一条 [云助手](../intl.zh-CN/产品简介/云助手/云助手概述.md#) 命令。

## 描述 {#section_iyx_fl4_ydb .section}

-   您可以创建以下类型的命令：
    -   Windows 实例适用的 Bat 脚本（`RunBatScript`）
    -   Windows 实例适用的 PowerShell 脚本（`RunPowerShellScript`）
    -   Linux 实例适用的 Shell 脚本（`RunShellScript`）
-   您可以通过指定参数 `TimeOut` 为命令设置在 ECS 实例中执行时最大的超时时间，命令执行超时后，[云助手客户端](../intl.zh-CN/用户指南/云助手客户端.md#) 会强制终止命令进程，即取消命令的 PID。
    -   对于单次执行，超时后，该命令针对指定的 ECS 实例的执行状态（[`InvokeRecordStatus`](intl.zh-CN/API 参考/云助手/DescribeInvocationResults.md#InvokeRecordStatusRequest)）变为 **执行失败**（`Failed`）。
    -   对于周期执行：
        -   周期执行的超时时间对每一次执行记录均有效。
        -   某次执行超时后，该次执行记录的状态（[`InvokeRecordStatus`](intl.zh-CN/API 参考/云助手/DescribeInvocationResults.md#InvokeRecordStatusRequest)）变为 **执行失败**（`Failed`）。
        -   上次执行超时与否不影响下一次执行。
-   您可以通过指定参数 `WorkingDir` 为命令指定执行路径。对于 Linux 实例，默认在管理员 root 用户的 home 目录下，具体为 `/root` 目录。对于 Windows 实例，默认在云助手客户端进程所在目录，例如，`C:\ProgramData\aliyun\assist\$(version)`。
-   在一个地域下，您最多能创建 100 条云助手命令。

## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：CreateCommand|
|RegionId|String|是|地域 ID。您可以调用 [DescribeRegions](intl.zh-CN/API 参考/地域/DescribeRegions.md#) 查看最新的阿里云地域列表。|
|Name|String|是|命令名称，支持全字符集。长度不得超过 30 个字符。|
|Type|String|是|命令的类型。取值范围：-   RunBatScript：创建一个在 Windows 实例中运行的 Bat 脚本
-   RunPowerShellScript：创建一个在 Windows 实例中运行的 PowerShell 脚本
-   RunShellScript：创建一个在 Linux 实例中运行的 Shell 脚本

|
|Description|String|否|命令描述，支持全字符集。长度不得超过100个字符。|
|CommandContent|String|否|命令 Base64 编码后的内容。当您传入请求参数 `Type` 后，必须同时传入该参数。该参数的值必须使用 Base64 编码后传输，且脚本内容的大小在 Base64 编码之后不能超过 16 KB。|
|WorkingDir|String|否|您创建的命令在 ECS 实例中运行的目录。默认值：-   对于 Linux 实例，默认在管理员 root 用户的 home 目录下，具体为 `/root` 目录。
-   对于 Windows 实例，默认在云助手客户端进程所在目录，例如，`C:\ProgramData\aliyun\assist\$(version)`。

|
|TimeOut|Integer|否|您创建的命令在 ECS 实例中执行时最大的超时时间，单位为秒。当因为某种原因无法运行您创建的命令时，会出现超时现象；超时后，会强制终止命令进程，即取消命令的 PID。默认值：3600

|

## 返回参数 {#ResponseParameter .section}

|名称|类型|描述|
|:-|:-|:-|
|CommandId|String|命令 ID|

## 示例 { .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=CreateCommand
&RegionId=cn-hangzhou
&Name=Test
&Type=RunShellScript
&CommandContent=ZWNobyAxMjM=
&<公共请求参数>
```

**正常返回示例** 

**XML 格式**

```
<CreateCommandResponse>
    <RequestId>E69EF3CC-94CD-42E7-8926-F133B86387C0</RequestId>
    <CommandId>c-7d2a745b412b4601b2d47f6a768d3a14</CommandId>
</CreateCommandResponse>
```

**JSON 格式** 

```
{
    "RequestId":"E69EF3CC-94CD-42E7-8926-F133B86387C0",
    "CommandId":"c-7d2a745b412b4601b2d47f6a768d3a14"
}
```

**异常返回示例** 

**XML 格式**

```
<Error>
    <RequestId>E69EF3CC-94CD-42E7-8926-F133B86387C0</RequestId>
    <HostId>ecs.aliyuncs.com</HostId>
    <Code>MissingParameter.Name</Code>
    <Message>The input parameter “Name” that is mandatory for processing this request is not supplied.</Message>
</Error>
```

**JSON 格式** 

```
{
    "RequestId": "E69EF3CC-94CD-42E7-8926-F133B86387C0",
    "HostId": "ecs.aliyuncs.com"
    "Code": "MissingParameter.Name"
    "Message": "The input parameter “Name” that is mandatory for processing this request is not supplied."
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问 [API 错误中心](https://error-center.alibabacloud.com/status/product/Ecs)。

|错误代码|错误信息|HTTP 状态码|说明|
|:---|:---|:-------|:-|
|Invalid.CommandContent|The specified CommandContent is not valid or exceed max|400|参数 `CommandContent`不合法，或者参数 `CommandContent` 的值的原始内容超过了 16 KB。|
|MissingParameter.Name|The input parameter “Name” that is mandatory for processing this request is not supplied.|400|您必须指定必需参数 `Name`。|
|MissingParameter.RegionId|The input parameter “RegionId” that is mandatory for processing this request is not supplied.|400|您必须指定必需参数 `RegionId`，或者您暂时不能使用指定 RegionId 里的资源。|
|MissingParameter.Type|The input parameter “Type” that is mandatory for processing this request is not supplied.|400|您必须指定必需参数 `Type`。|
|CmdContent.ExceedLimit|The length of the command content exceeds the upper limit.|403|脚本内容的大小在 Base64 编码之后不能超过 16 KB。|
|CmdName.ExceedLimit|The length of the command name exceeds the upper limit.|403|命令名称长度不得超过 30 个字符。|
|CmdDesc.ExceedLimit|The length of the command description exceeds the upper limit.|403|命令描述长度不得超过 100 个字符。|
|CmdCount.ExceedQuota|The total number of commands in the current region exceeds the quota.|403|在一个地域下，您最多能创建 100 条云助手命令。|
|InvalidCmdType.NotFound|The specified command type does not exist|404|指定的参数 `Type` 不存在。|
|InvalidRegionId.NotFound|The RegionId provided does not exist in our items.|404|指定的参数 `RegionId`不存在。|
|InternalError.Dispatch|An internal error occurred when dispath the request|500|内部错误，请稍后尝试。|

