# StopInvocation {#doc_api_Ecs_StopInvocation .reference}

调用StopInvocation停止一台或多台ECS实例中一条正在进行中（Running）的云助手命令进程。

## 接口说明 {#description .section}

-   停止单次命令进程后，已经开始执行的实例会继续执行，未开始执行的实例将不再执行。
-   停止周期命令进程后，已经开始执行的命令将继续执行，但后续将不会再进行下一次的执行。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=StopInvocation)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|InvokeId|String|是|t-7d2a745b412b4601b2d47f6a768d3\*\*\*|命令进程执行ID。您可以通过接口 [DescribeInvocations](~~64840~~) 查询所有的InvokeId。

 |
|RegionId|String|是|cn-hangzhou|地域ID。您可以调用 [DescribeRegions](~~25609~~) 查看最新的阿里云地域列表。

 |
|Action|String|否|StopInvocation|系统规定参数。取值：StopInvocation

 |
|InstanceId.N|RepeatList|否|i-uf614fhehhzmx\*\*\*|要停止执行命令的实例列表，最多能指定20台实例ID。N的取值范围为1~50。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=StopInvocation
&InvokeId=t-7d2a745b412b4601b2d47f6a768d3***
&RegionId=cn-hangzhou
&InstanceId.1=i-uf614fhehhzmx***
&<公共请求参数>
```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<StopInvocationResponse>
  <RequestId>E69EF3CC-94CD-42E7-8926-F133B86387C0</RequestId>
</StopInvocationResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"E69EF3CC-94CD-42E7-8926-F133B86387C0"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|500|InternalError.Dispatch|An error occurred when you dispatched the request.|发生未知错误。|
|404|InvalidInvokeId.NotFound|The specified invoke ID does not exist.|指定的InvokeId不存在。|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

