# DescribeInvocations {#doc_api_Ecs_DescribeInvocations .reference}

查询云助手命令的执行列表和状态。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=DescribeInvocations)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|RegionId|String|是|cn-hangzhou|ECS 实例所在的地域 ID。您可以调用 [DescribeRegions](~~25609~~) 查看最新的阿里云地域列表。

 |
|Action|String|否|DescribeInvocations|系统规定参数。取值：DescribeInvocations

 |
|CommandId|String|否|c-4d34302d02424c5c8e10281e3a315a05|命令 ID。您可以通过接口 [DescribeCommands](~~64843~~) 查询所有可用的 CommandId。

 |
|CommandName|String|否|Test1|命令名称。

 |
|CommandType|String|否|RunShellScript|命令类型。

 |
|InstanceId|String|否|i-uf614fhehhzxx|实例 ID。当您传入了该参数，将查询该实例所有的命令执行记录。

 |
|InvokeId|String|否|t-7d2a745b412b4601b2d47f6a768d3b53|命令进程执行 ID。

 |
|InvokeStatus|String|否|Finished|指定的命令总的执行状态。总的执行状态取决于指定命令管理的所有目标实例中的命令进程执行状态 InstanceInvokeStatus。取值范围：

 -   Running：命令进程进行中
    -   周期执行：未手动停止周期执行命令前，命令进程一直为 进行中（Running）。
    -   单次执行：指定命令管理的所有目标实例中一旦有 进行中（Running）的命令进程，总的执行状态为 进行中（Running）。
-   Finished：命令进程执行完成
    -   周期执行：命令进程不可能为 执行完成（Finished）。
    -   单次执行：指定命令管理的所有目标实例全部执行完成，总的执行状态为 执行完成（Finished）。 或者 手动停止（Stopped）部分目标实例的命令进程，其余目标实例全部执行完成，总的执行状态为 执行完成（Finished）。
-   Failed：命令进程执行失败，命令进程出现超时情况或者其他异常
    -   周期执行：命令进程不可能为 执行失败（Failed）。
    -   单次执行：指定命令管理的所有目标实例全部执行失败，总的执行状态为 执行失败（Failed）。
-   PartialFailed：命令进程执行部分失败
    -   周期执行：命令进程不可能为 部分失败（PartialFailed）。
    -   单次执行：指定命令管理的所有目标实例中个别有 执行失败（Failed）的命令进程，总的执行状态为 部分失败（PartialFailed）。
-   Stopped：命令进程被手动停止

 |
|PageNumber|Long|否|1|当前页码，起始值：1

 默认值：1

 |
|PageSize|Long|否|10|分页查询时设置的每页行数，最大值：50

 默认值：10

 |
|Timed|Boolean|否|true|命令是否为周期执行。默认值：False

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|Invocations| | |命令执行记录集类型（InvocationSetType）。

 |
|└CommandContent|String|ZWNobyBKYWNr|返回本次执行的命令内容。如果您使用了自定义参数，则返回添加了自定义参数后的命令内容。

 |
|└CommandId|String|c-4d34302d02424c5c8e10281e3a315a05|命令 ID。

 |
|└CommandName|String|Test1|命令名称。

 |
|└CommandType|String|RunShellScript|命令类型。

 |
|└Frequency|String|0 \*/20 \* \* \* \*|周期任务的执行周期。 该参数值结构以 [Cron 表达式](~~64769~~) 为准。

 |
|└InvokeId|String|t-7d2a745b412b4601b2d47f6a768d3b53|命令执行ID。

 |
|└InvokeInstances| | |执行目标实例集类型（InvokeInstanceSetType）。

 |
|└InstanceId|String|i-uf614fhehhzxx|实例ID。

 |
|└InstanceInvokeStatus|String|Finished|指定实例的命令进程状态。

 -   Running：命令进程进行中。
    -   周期执行：未手动停止周期执行命令前，命令进程一直为 进行中（Running）。
    -   单次执行：指定实例的命令进程状态为 进行中（Running）。
-   Finished：命令进程执行完成。
    -   周期执行：命令进程不可能为 执行完成（Finished）。
    -   单次执行：指定实例的命令进程状态为 执行完成（Finished）。
-   Failed：命令进程执行失败，命令进程出现超时情况或者其他异常。
    -   周期执行：命令进程不可能为 执行失败（Failed）。
    -   单次执行：指定实例的命令进程状态为 执行失败（Failed）。
-   Stopped：命令进程被手动停止 。

 |
|└InvokeStatus|String|Finished|指定的命令总的执行状态。总的执行状态取决于指定命令管理的所有目标实例中的命令进程执行状态 InstanceInvokeStatus。取值范围：

 -   Running：命令进程进行中。
    -   周期执行：未手动停止周期执行命令前，命令进程一直为 进行中（Running）。
    -   单次执行：指定命令管理的所有目标实例中一旦有 进行中（Running）的命令进程，总的执行状态为 进行中（Running）。
-   Finished：命令进程执行完成。
    -   周期执行：命令进程不可能为 执行完成（Finished）。
    -   单次执行：指定命令管理的所有目标实例全部执行完成，总的执行状态为 执行完成（Finished）。 或者 手动停止（Stopped）部分目标实例的命令进程，其余目标实例全部执行完成，总的执行状态为 执行完成（Finished）。
-   Failed：命令进程执行失败，命令进程出现超时情况或者其他异常。
    -   周期执行：命令进程不可能为 执行失败（Failed）。
    -   单次执行：指定命令管理的所有目标实例全部执行失败，总的执行状态为 执行失败（Failed）。
-   PartialFailed：命令进程执行部分失败。
    -   周期执行：命令进程不可能为 部分失败（PartialFailed）。
    -   单次执行：指定命令管理的所有目标实例中个别有 执行失败（Failed）的命令进程，总的执行状态为 部分失败（PartialFailed）。
-   Stopped：命令进程被手动停止 。

 |
|└Parameters|String|\{"name":"Jack"\}|以JSON字符串的形式，返回本次执行传入的自定义参数。如果您的命令禁用了自定义参数功能，则返回空字符串。

 |
|└Timed|Boolean|false|是否为周期执行。

 |
|PageNumber|Long|1|查询结果的页码。

 |
|PageSize|Long|10|每页行数。

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。

 |
|TotalCount|Long|2|命令总个数。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

https://ecs.aliyuncs.com/?Action=DescribeInvocations
&RegionId=cn-hangzhou
&InvokeId=t-7d2a745b412b4601b2d47f6a768d3b53
&CommandId=c-4d34302d02424c5c8e10281e3a315a05
&CommandName=Test1
&CommandType=RunShellScript
&Timed=true
&InvokeStatus=Finished
&InstanceId=i-uf614fhehhzxx
&PageNumber=1
&PageSize=10
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeInvocationsResponse>
  <TotalCount>2</TotalCount>
  <PageNumber>1</PageNumber>
  <PageSize>10</PageSize>
  <Invocations>
    <Invocation>
      <InvokeStatus>Running</InvokeStatus>
      <InvokeId>t-7d2a745b412b4601b2d47f6a768d3b53</InvokeId>
      <CommandContent>ZWNobyBKYWNr</CommandContent>
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
      <Parameters>{"name":"Jack"}</Parameters>
      <Timed>True</Timed>
      <CommandId>c-7d2a745b412b4601b2d47f6a768d3a14</CommandId>
    </Invocation>
    <Invocation>
      <InvokeStatus>Finished</InvokeStatus>
      <InvokeId>t-7d2a745b412b4601b2d47f6a768d3b55</InvokeId>
      <CommandContent>ZWNobyBuYW1l</CommandContent>
      <CommandName>Test3</CommandName>
      <CommandType>RunShellScript</CommandType>
      <Frequency/>
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
      <Parameters/>
      <Timed>False</Timed>
      <CommandId>c-7d2a745b412b4601b2d47f6a768d3a16</CommandId>
    </Invocation>
  </Invocations>
  <RequestId>E69EF3CC-94CD-42E7-8926-F133B86387C0</RequestId>
</DescribeInvocationsResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"PageNumber":1,
	"Invocations":{
		"Invocation":[
			{
				"Parameters":"{\"name\":\"Jack\"}",
				"CommandContent":"ZWNobyBKYWNr",
				"CommandType":"RunShellScript",
				"CommandName":"Test1",
				"InvokeStatus":"Running",
				"InvokeId":"t-7d2a745b412b4601b2d47f6a768d3b53",
				"CommandId":"c-7d2a745b412b4601b2d47f6a768d3a14",
				"Timed":true,
				"InvokeInstances":{
					"InvokeInstance":[
						{
							"InstanceInvokeStatus":"Finished",
							"InstanceId":"i-uf614fhehhzmx"
						},
						{
							"InstanceInvokeStatus":"Running",
							"InstanceId":"i-uf64isakb713x"
						}
					]
				},
				"Frequency":"0 */20 * * * *"
			},
			{
				"Parameters":"",
				"CommandContent":"ZWNobyBuYW1l",
				"CommandType":"RunShellScript",
				"CommandName":"Test3",
				"InvokeStatus":"Finished",
				"InvokeId":">t-7d2a745b412b4601b2d47f6a768d3b55",
				"CommandId":"c-7d2a745b412b4601b2d47f6a768d3a16",
				"Timed":false,
				"InvokeInstances":{
					"InvokeInstance":[
						{
							"InstanceInvokeStatus":"Finished",
							"InstanceId":"i-uf614fhehhzmx"
						},
						{
							"InstanceInvokeStatus":"Finished",
							"InstanceId":"i-uf64isakb713x"
						}
					]
				}
			}
		]
	},
	"TotalCount":2,
	"PageSize":10,
	"RequestId":"E69EF3CC-94CD-42E7-8926-F133B86387C0"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|500|InternalError.Dispatch|An error occurred when you dispatched the request.|发生未知错误。|
|403|InvalidParam.PageNumber|The specified parameter is invalid.|指定的参数无效。|
|403|InvalidParam.PageSize|The specified parameter is invalid.|指定的参数无效。|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Ecs)

