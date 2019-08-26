# DescribeInvocationResults {#doc_api_Ecs_DescribeInvocationResults .reference}

调用DescribeInvocationResults查看云助手命令的执行结果，在指定ECS实例中的实际执行结果。

## 接口说明 {#description .section}

当您执行命令后，不代表命令一定成功运行，并且一定有预期的命令效果。您需要通过 [DescribeInvocationResults](~~64845~~) 查看实际的具体执行结果，以实际输出结果为准。 您可以查询最近两周的执行信息。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=DescribeInvocationResults)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|RegionId|String|是|cn-hangzhou|地域ID。您可以调用 [DescribeRegions](~~25609~~) 查看最新的阿里云地域列表。

 |
|Action|String|否|DescribeInvocationResults|系统规定参数。取值：DescribeInvocationResults

 |
|CommandId|String|否|c-4d34302d02424c5c8e10281e3a315\*\*\*|命令ID。

 |
|InstanceId|String|否|i-uf614fhehhzmx\*\*\*|实例ID。

 |
|InvokeId|String|否|t-7d2a745b412b4601b2d47f6a768d3\*\*\*|命令执行ID。命令进程执行ID。您可以通过接口 [DescribeInvocations](~~64840~~) 查询InvokeId。

 |
|InvokeRecordStatus|String|否|Finished|命令执行状态。

 |
|PageNumber|Long|否|1|当前页码，起始值：1

 默认值：1

 |
|PageSize|Long|否|5|分页查询时设置的每页行数，最大值：50

 默认值：10

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|Invocation| | |命令执行

 |
|InvocationResults| | |命令执行结果集

 |
|CommandId|String|c-4d34302d02424c5c8e10281e3a315\*\*\*|命令ID

 |
|ExitCode|Long|0|命令进程的退出码：

 -   Linux实例为Shell进程的退出码
-   Windows实例为Bat或者PowerShell进程的退出码

 |
|FinishedTime|String|2018-01-05 15:45:02|命令进程的完成时间。如果命令进程出现超时情况，命令进程的完成时间以 [CreateCommand](~~64844~~) 中指定的参数TimedOut为准

 |
|InstanceId|String|i-uf614fhehhzmx\*\*\*|实例ID

 |
|InvokeId|String|t-7d2a745b412b4601b2d47f6a768d3\*\*\*|命令执行ID。命令进程执行ID。您可以通过接口 [DescribeInvocations](~~64840~~) 查询InvokeId。

 |
|InvokeRecordStatus|String|Finished|命令执行状态

 |
|Output|String|MTU6MzA6MDEK|命令进程完成后的实际结果，输出内容以Base64编码的形式传输

 |
|PageNumber|Long|1|当前页码，起始值：1

 默认值：1

 |
|PageSize|Long|5|分页查询时设置的每页行数，最大值：20

 默认值：10

 |
|TotalCount|Long|5|命令总个数

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=DescribeInvocationResults
&RegionId=cn-hangzhou
&InvokeId=t-7d2a745b412b4601b2d47f6a768d3***
&InstanceId=i-uf614fhehhzmx***
&CommandId=c-4d34302d02424c5c8e10281e3a315***
&InvokeRecordStatus=Finished
&PageNumber=1
&PageSize=5
&<公共请求参数>
```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeInvocationResultsResponse>
  <TotalCount>5</TotalCount>
  <PageNumber>1</PageNumber>
  <PageSize>5</PageSize>
  <InvocationResults>
    <InvocationResult>
      <FinishedTime>2018-01-05 15:45:02</FinishedTime>
      <InstanceId>i-uf614fhehhzmx***</InstanceId>
      <Output>MTU6NDU6MDEK</Output>
      <InvokeRecordStatus> Finished</InvokeRecordStatus>
      <ExitCode>0</ExitCode>
    </InvocationResult>
    <InvocationResult>
      <FinishedTime>2018-01-05 15:40:02</FinishedTime>
      <InstanceId>i-uf614fhehhzmx***</InstanceId>
      <Output/>
      <InvokeRecordStatus> Finished</InvokeRecordStatus>
      <ExitCode>0</ExitCode>
    </InvocationResult>
    <InvocationResult>
      <FinishedTime>2018-01-05 15:30:02</FinishedTime>
      <InstanceId>i-uf614fhehhzmx***</InstanceId>
      <Output>MTU6MzA6MDEK</Output>
      <ExitCode>0</ExitCode>
    </InvocationResult>
    <InvocationResult>
      <FinishedTime>2018-01-05 15:20:02</FinishedTime>
      <InstanceId>i-uf614fhehhzmx***</InstanceId>
      <Output/>
      <ExitCode>0</ExitCode>
    </InvocationResult>
    <InvocationResult>
      <FinishedTime>2018-01-05 15:15:02</FinishedTime>
      <InstanceId>i-uf614fhehhzmx***</InstanceId>
      <Output>MTU6MTU6MDEK</Output>
      <ExitCode>0</ExitCode>
    </InvocationResult>
  </InvocationResults>
  <RequestId>"E69EF3CC-94CD-42E7-8926-F133B86387C0</RequestId>
</DescribeInvocationResultsResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"E69EF3CC-94CD-42E7-8926-F133B86387C0",
	"Invocation":{
		"PageNumber":1,
		"TotalCount":5,
		"InvocationResults":{
			"InvocationResult":[
				{
					"InvokeRecordStatus":"Finished",
					"FinishedTime":"2018-01-05 15:45:02",
					"ExitCode":0,
					"InstanceId":"i-uf614fhehhzmx***",
					"Output":"MTU6NDU6MDEK"
				},
				{
					"InvokeRecordStatus":"Finished",
					"FinishedTime":"2018-01-05 15:40:02",
					"ExitCode":0,
					"InstanceId":"i-uf614fhehhzmx***",
					"Output":""
				},
				{
					"FinishedTime":"2018-01-05 15:30:02",
					"ExitCode":0,
					"InstanceId":"i-uf614fhehhzmx***",
					"Output":"MTU6MzA6MDEK"
				},
				{
					"FinishedTime":"2018-01-05 15:20:02",
					"ExitCode":0,
					"InstanceId":"i-uf614fhehhzmd3zj4***",
					"Output":""
				},
				{
					"InvokeRecordStatus":"Finished",
					"FinishedTime":"2018-01-05 15:15:02",
					"ExitCode":0,
					"InstanceId":"i-uf614fhehhzmd3zj4***",
					"Output":"MTU6MTU6MDEK"
				}
			]
		},
		"PageSize":5
	}
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|500|InternalError.Dispatch|An error occurred when you dispatched the request.|发生未知错误。|
|403|InvalidParam.PageNumber|The specified parameter is invalid.|指定的参数无效。|
|403|InvalidParam.PageSize|The specified parameter is invalid.|指定的参数无效。|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

