# DescribeInvocationResults {#DescribeInvocationResults .reference}

查看云助手命令的执行结果，在指定ECS实例中的实际执行结果。

## 描述 {#section_nlv_qq4_ydb .section}

当您执行命令后，不代表命令一定成功运行，并且一定有预期的命令效果。您需要通过[DescribeInvocationResults](cn.zh-CN/API 参考/云助手/DescribeInvocationResults.md#)查看实际的具体执行结果，以实际输出结果为准。

## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：DescribeInvocationResults|
|RegionId|String|是|地域ID。您可以调用[DescribeRegions](../cn.zh-CN/API 参考/地域/DescribeRegions.md#)查看最新的阿里云地域列表。|
|InvokeId|String|是|命令执行ID。命令进程执行ID。您可以通过接口[DescribeInvocations](cn.zh-CN/API 参考/云助手/DescribeInvocations.md#)查询`InvokeId`。|
|InstanceId|String|否|实例ID。|
|PageNumber|Integer|否|当前页码，起始值：1默认值：1

|
|PageSize|Integer|否|分页查询时设置的每页行数，最大值：20默认值：10

|

## 返回参数 {#ResponseParameter .section}

|名称|类型|描述|
|:-|:-|:-|
|TotalCount|Integer|命令总个数|
|PageNumber|Integer|查询结果的页码|
|PageSize|Integer|每页行数|
|InvocationResults|Array|命令执行结果集（[`InvocationResultSetType`](#InvocationResultSetType)）|

**命令执行结果集InvocationResultSetType**

|名称|类型|描述|
|:-|:-|:-|
|InvocationResult|Array|实例执行结果类型（[`InvocationResultType`](#InvocationResultType)）（如果是一次性执行，则只有一个结果）|

**实例执行结果类型InvocationResultType**

|名称|类型|描述|
|:-|:-|:-|
|InvokeId|String|执行ID|
|InstanceId|String|实例ID|
|FinishedTime|String|命令进程的完成时间。如果命令进程出现超时情况，命令进程的完成时间以[CreateCommand](cn.zh-CN/API 参考/云助手/CreateCommand.md#)中指定的参数`TimedOut`为准|
|Output|String|命令进程完成后的实际结果，输出内容以Base64编码的形式传输|
|ExitCode|Integer|命令进程的退出码：-   Linux实例为Shell进程的退出码
-   Windows实例为Bat或者PowerShell进程的退出码

|

## 示例 { .section}

**请求示例**

```
https://ecs.aliyuncs.com/?Action=DescribeInvocationResults
&RegionId=cn-hangzhou
&InvokeId=t-7d2a745b412b4601b2d47f6a768d3a14
&<公共请求参数>
```

**正常返回示例**

**XML格式**

```
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

**JSON格式**

```
{
    "Invocation": {
        "TotalCount": 5,
        "PageNumber": 1,
        "InvocationResults": {
            "InvocationResult": [
                {
                    "FinishedTime": "2018-01-05 15:45:02",
                    "InstanceId": "i-uf614fhehhzmxdqw",
                    "Output": "MTU6NDU6MDEK",
	       “InvokeRecordStatus”：“Finished”,
                    "ExitCode": 0
                },
                {
                    "FinishedTime": "2018-01-05 15:40:02",
                    "InstanceId": "i-uf614fhehhzmxdqw",
		“InvokeRecordStatus”：“Finished”,
                    "Output": "",
                    "ExitCode": 0
                },
                {
                    "FinishedTime": "2018-01-05 15:30:02",
                    "InstanceId": "i-uf614fhehhzmxdqw",
                    "Output": "MTU6MzA6MDEK",
                    "ExitCode": 0
                },
                {
                    "FinishedTime": "2018-01-05 15:20:02",
                    "InstanceId": "i-uf614fhehhzmd3zj4k74",
                    "Output": "",
                    "ExitCode": 0
                },
                {
                    "FinishedTime": "2018-01-05 15:15:02",
                    "InstanceId": "i-uf614fhehhzmd3zj4k74",
“InvokeRecordStatus”：“Finished”,
                    "Output": "MTU6MTU6MDEK",
                    "ExitCode": 0
                }
            ]
        },
        "PageSize": 5
    },
    "RequestId": ""E69EF3CC-94CD-42E7-8926-F133B86387C0"
}
```

**异常返回示例**

**XML格式**

```
<Error>
    <RequestId>E69EF3CC-94CD-42E7-8926-F133B86387C0</RequestId>
    <HostId>ecs.aliyuncs.com</HostId>
    <Code>MissingParameter.RegionId</Code>
    <Message>The input parameter “RegionId” that is mandatory for processing this request is not supplied.</Message>
</Error>
```

**JSON格式**

```
{
    "RequestId": "E69EF3CC-94CD-42E7-8926-F133B86387C0",
    "HostId": "ecs.aliyuncs.com"
    "Code": "MissingParameter.RegionId"
    "Message": "The input parameter “RegionId” that is mandatory for processing this request is not supplied."
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问[API错误中心](https://error-center.aliyun.com/status/product/Ecs)。

|错误代码|错误信息|HTTP状态码|说明|
|:---|:---|:------|:-|
|MissingParameter.RegionId|The input parameter “RegionId” that is mandatory for processing this request is not supplied.|400|您必须指定必需参数`RegionId`，或者您暂时不能使用指定`RegionId`里的资源。|
|InvalidParam.pageNumber|The specified parameter is invalid.|403|指定的页码不合法。|
|InvalidParam.PageSize|The specified parameter is invalid.|403|指定的页面大小不合法。|
|InvalidRegionId.NotFound|The RegionId provided does not exist in our items.|404|指定的`RegionId`不存在。|
|InternalError.Dispatch|An internal error occurred when dispatch the request.|500|内部错误，请稍后尝试。|

