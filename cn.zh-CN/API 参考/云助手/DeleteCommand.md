# DeleteCommand {#DeleteCommand .reference}

删除一条云助手命令。

## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：DeleteCommand|
|RegionId|String|是|地域 ID。您可以调用 [DescribeRegions](cn.zh-CN/API 参考/地域/DescribeRegions.md#) 查看最新的阿里云地域列表。|
|CommandId|String|是|命令 ID。您可以通过接口 [DescribeCommands](cn.zh-CN/API 参考/云助手/DescribeCommands.md#) 查询所有可用的 `CommandId`。|

## 返回参数 {#section_f54_lk5_xdb .section}

全是公共返回参数。参阅 [公共返回参数](cn.zh-CN/API 参考/快速入门/公共参数.md#commonResponseParameters)。

## 示例 { .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=DeleteCommand
&RegionId=cn-hangzhou
&InvokeId=c-f0902c0972984e31aaf2129fd48a9c6d
&<公共请求参数>
```

**正常返回示例** 

**XML 格式**

```
<DeleteCommandResponse>
    <RequestId>E69EF3CC-94CD-42E7-8926-F133B86387C0</RequestId>
</DeleteCommandResponse>
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
    <Code>InvalidInstance.NoClient</Code>
    <Message>The specified instances have no cloud assistant client installed.</Message>
</Error>
```

**JSON 格式** 

```
{
    "RequestId": "E69EF3CC-94CD-42E7-8926-F133B86387C0",
    "HostId": "ecs.aliyuncs.com"
    "Code": "InvalidInstance.NoClient"
    "Message": "The specified instances have no cloud assistant client installed."
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问 [API 错误中心](https://error-center.aliyun.com/status/product/Ecs)。

|错误代码|错误信息|HTTP 状态码|说明|
|:---|:---|:-------|:-|
|InvalidCmdId.NotFound|The specified commandId does not exist.|404|指定的 `CommandId` 不存在。|
|InvalidRegionId.NotFound|The RegionId provided does not exist in our items.|404|指定的 `RegionId` 不存在。|
|InternalError.Dispatch|An internal error occurred when dispath the request|500|内部错误，请稍后尝试。|

