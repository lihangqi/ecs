# DescribeInvocations {#DescribeInvocations .reference}

查询一台ECS实例中的云助手命令执行列表及状态。

## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：DescribeInvocations|
|RegionId|String|是|ECS 实例所在的地域 ID。您可以调用[DescribeRegions](../cn.zh-CN/API 参考/地域/DescribeRegions.md#)查看最新的阿里云地域列表。|
|InvokeId|String|否|命令进程执行 ID。|
|CommandId|String|否|命令 ID。您可以通过接口 [DescribeCommands](cn.zh-CN/API 参考/云助手/DescribeCommands.md#) 查询所有可用的 `CommandId`。|
|CommandName|String|否|命令名称。|
|Type|String|否|命令类型。取值范围：-   RunBatScript：查询的命令进程为是一个在 Windows 实例中运行的 Bat 脚本
-   RunPowerShellScript：查询的命令进程为是一个在 Windows 实例中运行的 PowerShell 脚本
-   RunShellScript：查询的命令进程为是一个在 Linux 实例中运行的 Shell 脚本

|
|Timed|Boolean|否|命令是否为周期执行。默认值：False|
|InvokeStatus|String|否|指定的命令总的执行状态。总的执行状态取决于指定命令管理的所有目标实例中的命令进程执行状态 `InstanceInvokeStatus`。取值范围：-   Running：命令进程进行中
    -   **周期执行**：未手动停止周期执行命令前，命令进程一直为 **进行中**（`Running`）。
    -   **单次执行**：指定命令管理的所有目标实例中一旦有 **进行中**（`Running`）的命令进程，总的执行状态为 **进行中**（`Running`）。
-   Finished：命令进程执行完成
    -   **周期执行**：命令进程不可能为 **执行完成**（`Finished`）。
    -   **单次执行**：指定命令管理的所有目标实例全部执行完成，总的执行状态为 **执行完成**（`Finished`）。

或者 **手动停止**（`Stopped`）部分目标实例的命令进程，其余目标实例全部执行完成，总的执行状态为 **执行完成**（`Finished`）。

-   Failed：命令进程执行失败，命令进程出现超时情况或者其他异常
    -   **周期执行**：命令进程不可能为 **执行失败**（`Failed`）。
    -   **单次执行**：指定命令管理的所有目标实例全部执行失败，总的执行状态为 **执行失败**（`Failed`）。
-   PartialFailed：命令进程执行部分失败
    -   **周期执行**：命令进程不可能为 **部分失败**（`PartialFailed`）。
    -   **单次执行**：指定命令管理的所有目标实例中个别有 **执行失败**（`Failed`）的命令进程，总的执行状态为 **部分失败**（`PartialFailed`）。
-   Stopped：命令进程被手动停止

|
|InstanceId|String|否|实例 ID。当您传入了该参数，将查询该实例所有的命令执行记录。|
|PageNumber|Integer|否|当前页码，起始值：1默认值：1

|
|PageSize|Integer|否|分页查询时设置的每页行数，最大值：50默认值：10

|

## 返回参数 {#ResponseParameter .section}

|名称|类型|描述|
|:-|:-|:-|
|TotalCount|Integer|命令总个数。|
|PageNumber|Integer|查询结果的页码。|
|PageSize|Integer|每页行数。|
|Invocations|Array|命令执行记录集类型（[`InvocationSetType`](#)）。|

 **命令执行记录集类型 InvocationSetType** 

|名称|类型|描述|
|:-|:-|:-|
|Invocation|Array|命令执行类型（[`InvocationType`](#)）。|

 **命令执行类型 InvocationType** 

|名称|类型|描述|
|:-|:-|:-|
|InvokeId|String|命令执行ID。|
|CommandId|String|命令 ID。|
|CommandName|String|命令名称。|
|InvokeStatus|String|指定的命令总的执行状态。总的执行状态取决于指定命令管理的所有目标实例中的命令进程执行状态 `InstanceInvokeStatus`。取值范围：-   Running：命令进程进行中。
    -   **周期执行**：未手动停止周期执行命令前，命令进程一直为 **进行中**（`Running`）。
    -   **单次执行**：指定命令管理的所有目标实例中一旦有 **进行中**（`Running`）的命令进程，总的执行状态为 **进行中**（`Running`）。
-   Finished：命令进程执行完成。
    -   **周期执行**：命令进程不可能为 **执行完成**（`Finished`）。
    -   **单次执行**：指定命令管理的所有目标实例全部执行完成，总的执行状态为 **执行完成**（`Finished`）。

或者 **手动停止**（`Stopped`）部分目标实例的命令进程，其余目标实例全部执行完成，总的执行状态为 **执行完成**（`Finished`）。

-   Failed：命令进程执行失败，命令进程出现超时情况或者其他异常。
    -   **周期执行**：命令进程不可能为 **执行失败**（`Failed`）。
    -   **单次执行**：指定命令管理的所有目标实例全部执行失败，总的执行状态为 **执行失败**（`Failed`）。
-   PartialFailed：命令进程执行部分失败。
    -   **周期执行**：命令进程不可能为 **部分失败**（`PartialFailed`）。
    -   **单次执行**：指定命令管理的所有目标实例中个别有 **执行失败**（`Failed`）的命令进程，总的执行状态为 **部分失败**（`PartialFailed`）。
-   Stopped：命令进程被手动停止 。

|
|CommandType|String|命令类型。|
|Timed|Boolean|是否为周期执行。|
|Frequency|String|周期任务的执行周期。该参数值结构以 [Cron 表达式](https://help.aliyun.com/document_detail/64769.html) 为准。

|
|InvokeInstances|Array|执行目标实例集类型（[`InvokeInstanceSetType`](#)）。|

 **执行目标实例集类型 InvokeInstanceSetType** 

|名称|类型|描述|
|:-|:-|:-|
|InvokeInstance|Array|目标实例执行状态类型（[`InvokeInstanceType`](#)）。|

 **目标实例执行状态类型 InvokeInstanceType** 

|名称|类型|描述|
|:-|:-|:-|
|InstanceId|String|实例ID。|
|InstanceInvokeStatus|String|指定实例的命令进程状态。-   Running：命令进程进行中。
    -   **周期执行**：未手动停止周期执行命令前，命令进程一直为 **进行中**（`Running`）。
    -   **单次执行**：指定实例的命令进程状态为 **进行中**（`Running`）。
-   Finished：命令进程执行完成。
    -   **周期执行**：命令进程不可能为 **执行完成**（`Finished`）。
    -   **单次执行**：指定实例的命令进程状态为 **执行完成**（`Finished`）。
-   Failed：命令进程执行失败，命令进程出现超时情况或者其他异常。
    -   **周期执行**：命令进程不可能为 **执行失败**（`Failed`）。
    -   **单次执行**：指定实例的命令进程状态为 **执行失败**（`Failed`）。
-   Stopped：命令进程被手动停止 。

|

## 示例 { .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=DescribeInvocations
&RegionId=cn-hangzhou
&<公共请求参数>
```

**正常返回示例** 

**XML 格式**

```
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
                <Frequency> </Frequency>
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

**JSON 格式** 

```
{
    "TotalCount": 2,
    "PageNumber": 1,
    "PageSize": 10,
    "Invocations": {
        "Invocation": [
            {
                "InvokeStatus": "Running",
                "InvokeId": "t-7d2a745b412b4601b2d47f6a768d3b53",
                "CommandName": "Test1",
                "CommandType": "RunShellScript",
                "Frequency": "0 */20 * * * *",
                "InvokeInstances": {
                    "InvokeInstance": [
                        {
                            "InstanceId": "i-uf614fhehhzmx",
                            "InstanceInvokeStatus": "Finished"
                        },
                        {
                            "InstanceId": "i-uf64isakb713x",
                            "InstanceInvokeStatus": "Running"
                        }
                    ]
                },
                "Timed": true,
                "CommandId": "c-7d2a745b412b4601b2d47f6a768d3a14"
            },
            {
                "InvokeStatus": "Finished",
                "InvokeId": ">t-7d2a745b412b4601b2d47f6a768d3b55",
                "CommandName": "Test3",
                "CommandType": "RunShellScript",
                "InvokeInstances": {
                    "InvokeInstance": [
                        {
                            "InstanceId": "i-uf614fhehhzmx",
                            "InstanceInvokeStatus": "Finished"
                        },
                        {
                            "InstanceId": "i-uf64isakb713x",
                            "InstanceInvokeStatus": "Finished"
                        }
                    ]
                },
                "Timed": false,
                "CommandId": "c-7d2a745b412b4601b2d47f6a768d3a16"
            } 
        ]
    },
    "RequestId": "E69EF3CC-94CD-42E7-8926-F133B86387C0"
}
```

**异常返回示例** 

**XML 格式**

```
<Error>
    <RequestId>E69EF3CC-94CD-42E7-8926-F133B86387C0</RequestId>
    <HostId>ecs.aliyuncs.com</HostId>
    <Code>MissingParameter.RegionId</Code>
    <Message>The input parameter “RegionId” that is mandatory for processing this request is not supplied.</Message>
</Error>
```

**JSON 格式** 

```
{
    "RequestId": "E69EF3CC-94CD-42E7-8926-F133B86387C0",
    "HostId": "ecs.aliyuncs.com"
    "Code": "MissingParameter.RegionId"
    "Message": "The input parameter “RegionId” that is mandatory for processing this request is not supplied."
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问 [API 错误中心](https://error-center.aliyun.com/status/product/Ecs)。

|错误代码|错误信息|HTTP 状态码|说明|
|:---|:---|:-------|:-|
|MissingParameter.RegionId|The input parameter “RegionId” that is mandatory for processing this request is not supplied.|400|您必须指定必需参数 `RegionId`，或者您暂时不能使用指定 `RegionId` 里的资源。|
|InvalidParam.pageNumber|The specified parameter is invalid.|403|指定的页码不合法。|
|InvalidParam.PageSize|The specified parameter is invalid.|403|指定的页面大小不合法。|
|InvalidRegionId.NotFound|The RegionId provided does not exist in our items.|404|指定的 `RegionId` 不存在。|
|InternalError.Dispatch|An internal error occurred when dispath the request|500|内部错误，请稍后尝试。|

