# InvokeCommand {#InvokeCommand .reference}

为一台或多台ECS实例触发一条云助手命令。

## 描述 {#section_amn_fm4_ydb .section}

当您使用该接口时，请注意：

-   在一个阿里云地域下，您每天最多能运行500次云助手命令。
-   目标实例的网络类型必须是[专有网络VPC](../../../../../cn.zh-CN/产品简介/什么是专有网络.md#)。
-   目标实例的状态必须为 **运行中**（`Running`）。
-   目标实例必须预先安装 [云助手客户端](../cn.zh-CN/用户指南/云助手客户端.md#)。
-   执行类型为PowerShell的命令时，您需要确保目标ECS Windows实例已经配置了PowerShell模块。
-   对于单次执行（`Timed=False`），只执行一次命令。
-   对于周期执行（`Timed=True`），云助手将根据参数`Frequency`指定的时间频率定时执行。上次的执行结果不对下一次执行产生任何影响。
-   周期执行的时间设置基准为UTC +08:00，且该时间以实例的系统时间为准，您需要确保您的ECS实例的时间或者时区与您预期的时间一致。

    更多关于时区的详情，Linux 实例请参阅 [修改 ECS Linux 实例时区与设置 NTP 服务](https://help.aliyun.com/document_detail/42528.html)，Windows 实例请参阅 [同步 Windows 实例的时钟](https://help.aliyun.com/document_detail/51890.html)。

-   您可以选择多台ECS实例，若其中某台实例不满足执行条件时，您需要重新选择。
-   命令的执行可能会因为目标实例的状态异常、网络异常或云助手客户端异常而出现无法执行的情况，无法执行时不会生成执行信息。

## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：InvokeCommand|
|RegionId|String|是|地域ID。您可以调用 [DescribeRegions](cn.zh-CN/API 参考/地域/DescribeRegions.md#) 查看最新的阿里云地域列表。|
|InstanceId.N|Array|是|需要执行命令的实例列表，最多能指定20台实例ID。`N`的取值范围为\[1, 20\]。|
|CommandId|String|是|命令 ID。您可以通过接口 [DescribeCommands](cn.zh-CN/API 参考/云助手/DescribeCommands.md#) 查询所有可用的`CommandId`。|
|Timed|Boolean|否|命令是否为周期执行。默认值：False

|
|Frequency|String|否|周期任务的执行周期，两次周期任务的时间间隔不能低于10秒。当参数 [`Timed`](#Timed) 的值为`True`时，参数`Frequency`为必需参数。该参数取值遵循Cron表达式，参阅 [Cron 表达式](https://help.aliyun.com/document_detail/64769.html)[Cron 表达式](https://www.alibabacloud.com/help/faq-detail/64769.htm)。

|

## 返回参数 {#ResponseParameter .section}

|名称|类型|描述|
|:-|:-|:-|
|InvokeId|String|命令执行ID|

## 示例 { .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=InvokeCommand
&RegionId=cn-hangzhou
&InstanceId.1=i-bp185dy2o3o6nxxxxxxx
&InstanceId.2=i-bsdn5dy2o845sxxxxxxx
&CommandId=c-e996287206324975b5fbe1dxxxxxxxxx
&Timed=true&Frequency=0 0-5 14 * * ?
&<公共请求参数>
```

**正常返回示例** 

**XML格式**

```
<InvokeCommandResponse>
    <RequestId>E69EF3CC-94CD-42E7-8926-F133B86387C0</RequestId>
    <InvokeId>t-7d2a745b412b4601b2d47f6a768d3a14</InvokeId>
</InvokeCommandResponse>
```

**JSON格式** 

```
{
    "RequestId":"E69EF3CC-94CD-42E7-8926-F133B86387C0",
    "InvokeId":"t-7d2a745b412b4601b2d47f6a768d3a14"
}
```

**异常返回示例** 

**XML格式**

```
<Error>
    <RequestId>E69EF3CC-94CD-42E7-8926-F133B86387C0</RequestId>
    <HostId>ecs.aliyuncs.com</HostId>
    <Code>MissingParameter.CommandId</Code>
    <Message>The input parameter “CommandId” that is mandatory for processing this request is not supplied.</Message>
</Error>
```

**JSON格式** 

```
{
    "RequestId": "E69EF3CC-94CD-42E7-8926-F133B86387C0",
    "HostId": "ecs.aliyuncs.com"
    "Code": "MissingParameter.CommandId"
    "Message": "The input parameter “CommandId” that is mandatory for processing this request is not supplied."
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问 [API 错误中心](https://error-center.aliyun.com/status/product/Ecs)。

|错误代码|错误信息|HTTP状态码|说明|
|:---|:---|:------|:-|
|InvalidInstanceStatus|The specified instance’s status can not execute this operation|400|指定实例的状态必须为运行中；或者指定实例的网络状态异常。|
|MissingParameter.CommandId|The input parameter “CommandId” that is mandatory for processing this request is not supplied.|400|您必须指定必需参数`CommandId`。|
|MissingParameter.InstanceIds|The input parameter “InstanceIds” that is mandatory for processing this request is not supplied.|400|您必须指定必需参数`InstanceId.N`。|
|MissingParameter.RegionId|The input parameter “RegionId” that is mandatory for processing this request is not supplied.|400|您必须指定必需参数`RegionId`，或者您暂时不能使用指定`RegionId`里的资源。|
|MissingParameter.Frequency|The frequency parameter must exist when create a timed Invocation.|400|当参数`Timed`的值为`True`时，您必须指定参数`Frequency`。|
|InvalidParam.Frequency|The specified frequency is invalid.|403|指定的 `Frequency` 不合法。|
|InstanceIds.ExceedLimit|The number of instance IDs exceeds the upper limit.|403|最多能指定20台实例ID。|
|Invocation.ExceedQuota|The invocation quota in the current region has been reached for today.|403|在一个阿里云地域下，您每天最多能运行500次云助手命令。|
|InvalidCmdId.NotFound|The specified commandId does not exist.|404|指定的`CommandId`不存在。|
|InvalidInstance.NotFound|The specified instances does not exist.|404|指定的`InstanceId`不存在。|
|InvalidRegionId.NotFound|The RegionId provided does not exist in our items.|404|指定的`RegionId`不存在。|
|InternalError.Dispatch|An internal error occurred when dispatching your request.|500|内部错误，请稍后尝试。|

