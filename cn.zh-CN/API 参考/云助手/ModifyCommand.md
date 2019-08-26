# ModifyCommand {#ModifyCommand .reference}

修改一条云助手命令相关参数以及命令内容。

## 描述 {#section_s4q_vr4_ydb .section}

-   命令执行期间也允许修改，修改命令后，后续执行会按照新的命令内容执行。
-   您不能修改命令的类型，例如，如果命令是 Shell 命令（`RunShellScript`），则不能修改为 Bat 命令（`RunBatScript`）。

## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：ModifyCommand|
|RegionId|String|是|地域 ID。您可以调用 [DescribeRegions](cn.zh-CN/API 参考/地域/DescribeRegions.md#) 查看最新的阿里云地域列表。|
|CommandId|String|是|命令 ID。您可以通过接口 [DescribeCommands](cn.zh-CN/API 参考/云助手/DescribeCommands.md#) 查询所有可用的 `CommandId`。|
|Name|String|否|命令名称，支持全字符集。长度不得超过 30 个字符。|
|Description|String|否|命令描述，支持全字符集。长度不得超过100个字符。|

## 返回参数 {#section_f54_lk5_xdb .section}

全是公共返回参数。参阅 [公共返回参数](cn.zh-CN/API 参考/快速入门/公共参数.md#commonResponseParameters)。

## 示例 { .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=ModifyCommand
&RegionId=cn-hangzhou
&CommandId=c-e996287206324975b5fbe1dxxxxxxxxx
&NameId=Test
&TimeOut=120
&<公共请求参数>
```

**正常返回示例** 

**XML 格式**

```
<ModifyCommandResponse>
    <RequestId>E69EF3CC-94CD-42E7-8926-F133B86387C0</RequestId>
</ModifyCommandResponse>
```

 **JSON 格式** 

```
{
    "RequestId":"E69EF3CC-94CD-42E7-8926-F133B86387C0",
}
```

**异常返回示例** 

**XML 格式**

```
<Error>
    <RequestId>E69EF3CC-94CD-42E7-8926-F133B86387C0</RequestId>
    <HostId>ecs.aliyuncs.com</HostId>
    <Code>InvalidCmdId.NotFound</Code>
    <Message>The specified command ID does not exist.</Message>
</Error>
```

**JSON 格式** 

```
{
    "RequestId": "E69EF3CC-94CD-42E7-8926-F133B86387C0",
    "HostId": "ecs.aliyuncs.com"
    "Code": "InvalidCmdId.NotFound"
    "Message": "The specified command ID does not exist."
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问 [API 错误中心](https://error-center.aliyun.com/status/product/Ecs)。

|错误代码|错误信息|HTTP 状态码|说明|
|:---|:---|:-------|:-|
|MissingParameter.CommandId|The input parameter “CommandId” that is mandatory for processing this request is not supplied.|400|您必须指定必需参数 `CommandId`。|
|MissingParameter.RegionId|The input parameter “RegionId” that is mandatory for processing this request is not supplied.|400|您必须指定必需参数 `RegionId`，或者您暂时不能使用指定 `RegionId` 里的资源。|
|InvalidCmdId.NotFound|The specified CommandId does not exist.|404|指定的 `CommandId` 不存在。|
|InvalidRegionId.NotFound|The RegionId provided does not exist in our items.|404|指定的 `RegionId` 不存在。|
|InternalError.Dispatch|An internal error occurred when dispath the request|500|内部错误，请稍后尝试。|

