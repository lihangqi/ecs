# StopInvocation {#StopInvocation .reference}

停止一台或多台ECS实例中一条正在**进行中**（`Running`）的云助手命令进程。

## 描述 {#section_ult_wm4_ydb .section}

-   停止单次命令进程后，已经开始执行的实例会继续执行，未开始执行的实例将不再执行。
-   停止周期命令进程后，已经开始执行的命令将继续执行，但后续将不会再进行下一次的执行。

## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：StopInvocation|
|RegionId|String|是|地域ID。您可以调用[DescribeRegions](../cn.zh-CN/API 参考/地域/DescribeRegions.md#)查看最新的阿里云地域列表。|
|InvokeId|String|是|命令进程执行ID。您可以通过接口[DescribeInvocations](cn.zh-CN/API 参考/云助手/DescribeInvocations.md#)查询所有的`InvokeId`。|
|InstanceId.N|Array|否|需要停止执行命令的实例列表，最多能指定20台实例ID。`N`的取值范围为\[1, 20\]。|

## 返回参数 {#section_f54_lk5_xdb .section}

全是公共返回参数。参阅[公共返回参数](../cn.zh-CN/API 参考/快速入门/公共参数.md#commonResponseParameters)。

## 示例 { .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=StopInvocation
&RegionId=cn-hangzhou
&InvokeId=t-1fad2a8876de47068cc734d57703aa76
&<公共请求参数>
```

**正常返回示例** 

**XML格式**

```
<StopInvocationResponse>
    <RequestId>E69EF3CC-94CD-42E7-8926-F133B86387C0</RequestId>
</StopInvocationResponse>
```

**JSON格式**

```
{
    "RequestId":"E69EF3CC-94CD-42E7-8926-F133B86387C0",
}
```

**异常返回示例**

**XML格式**

```
<Error>
    <RequestId>E69EF3CC-94CD-42E7-8926-F133B86387C0</RequestId>
    <HostId>ecs.aliyuncs.com</HostId>
    <Code>InvalidInstance.NoClient</Code>
    <Message>The specified instances have no cloud assistant client installed.</Message>
</Error>
```

**JSON格式**

```
{
    "RequestId": "E69EF3CC-94CD-42E7-8926-F133B86387C0",
    "HostId": "ecs.aliyuncs.com",
    "Code": "InvalidInstance.NoClient",
    "Message": "The specified instances have no cloud assistant client installed."
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问[API错误中心](https://error-center.aliyun.com/status/product/Ecs)。

|错误代码|错误信息|HTTP状态码|说明|
|:---|:---|:------|:-|
|InvalidInvokeId.NotFound|The specified InvokeId does not exist.|400|指定的`InvokeId`不存在。|
|MissingParameter.RegionId|The input parameter “RegionId” that is mandatory for processing this request is not supplied.|400|您必须指定必需参数`RegionId`，或者您暂时不能使用指定`RegionId`里的资源。|
|MissingParameter.InvokeId|The input parameter “InvokeId” that is mandatory for processing this request is not supplied.|400|您必须指定必需参数`InvokeId`。|
|InvalidRegionId.NotFound|The RegionId provided does not exist in our items.|404|指定的`RegionId`不存在。|
|InternalError.Dispatch|An internal error occurred when dispath the request|500|内部错误，请稍后尝试。|

