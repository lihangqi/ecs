# InvokeCommand {#doc_api_Ecs_InvokeCommand .reference}

调用InvokeCommand为一台或多台ECS实例触发一条云助手命令。

## 接口说明 {#description .section}

-   在一个阿里云地域下，您每天能调用 5000 次 InvokeCommand 接口。如果您想调整调用次数上限，请 [提交工单](https://selfservice.console.aliyun.com/ticket/createIndex.htm) 申请。
-   目标实例的网络类型必须是 [专有网络VPC](~~34217~~)。
-   目标实例的状态必须为 运行中（Running）。
-   目标实例必须预先安装 [云助手客户端](~~64921~~)。
-   执行类型为 PowerShell 的命令时，您需要确保目标 ECS Windows实例已经配置了 PowerShell 模块。
-   对于单次执行（Timed=False），只执行一次命令。
-   对于周期执行（Timed=True），云助手将根据参数 Frequency 指定的时间频率定时执行。上次的执行结果不对下一次执行产生任何影响。
-   周期执行的时间设置基准为UTC +0，且该时间以实例的系统时间为准，您需要确保您的 ECS 实例的时间或者时区与您预期的时间一致。 更多关于时区的详情，Linux 实例请参见 [时间设置：设置Linux实例时区和NTP服务](~~92803~~)，Windows 实例请参见 [时间设置：设置Windows实例NTP服务](~~51890~~)。
-   您可以选择多台ECS实例，若其中某台实例不满足执行条件时，您需要重新选择。
-   命令的执行可能会因为目标实例的状态异常、网络异常或云助手客户端异常而出现无法执行的情况，无法执行时不会生成执行信息。
-   当您创建命令时启用了自定义参数功能，需要在执行命令时传入自定义参数（Parameters）。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=InvokeCommand)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|CommandId|String|是|c-e996287206324975b5fbe1d\*\*\*\*\*\*\*\*|命令 ID。您可以通过接口 [DescribeCommands](~~64843~~) 查询所有可用的 CommandId。

 |
|InstanceId.N|RepeatList|是|i-bp185dy2o3o6n\*\*\*\*\*\*|需要执行命令的实例列表，最多能指定 50 台实例 ID。N 的取值范围为1~50。

 |
|RegionId|String|是|cn-hangzhou|地域ID。您可以调用 [DescribeRegions](~~25609~~) 查看最新的阿里云地域列表。

 |
|Action|String|否|InvokeCommand|系统规定参数。取值：InvokeCommand

 |
|Frequency|String|否|0 \*/20 \* \* \* \*|周期任务的执行周期，两次周期任务的时间间隔不能低于10秒。当参数 Timed 的值为 True 时，参数 Frequency 为必需参数。 该参数取值遵循Cron表达式，参见 [Cron 表达式](~~64769~~)。

 |
|Parameters|Json|否|\{"name":"Jack", "accessKey":"LTAIdyv\*\*\*\*\*\*aRY"\}|启用自定义参数功能时，执行命令时传入的自定义参数的键值对。自定义参数的个数范围：0~10

 -   Map的键不允许为空字符串，最多支持64个字符。
-   Map的值允许为空字符串。
-   自定义参数与原始命令内容在Base64编码后，综合长度不能超过16KB。
-   设置的自定义参数名集合必须为创建命令时定义的参数集的子集。对于未传入的参数，您可以使用空字符串代替。

 您可以取消设置该参数从而禁用自定义参数。

 |
|Timed|Boolean|否|true|命令是否为周期执行。 默认值：False

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|InvokeId|String|t-7d2a745b412b4601b2d47f6a768d3\*\*\*|命令执行ID

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=InvokeCommand
&CommandId=c-e996287206324975b5fbe1d********
&InstanceId.1=i-bp185dy2o3o6n******
&RegionId=cn-hangzhou
&Timed=true
&Frequency=0 */20 * * * *
&Parameters={"name":"Jack"}
&<公共请求参数>
```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<InvokeCommandResponse>
  <RequestId>E69EF3CC-94CD-42E7-8926-F133B86387C0</RequestId>
  <InvokeId>t-7d2a745b412b4601b2d47f6a768d3***</InvokeId>
</InvokeCommandResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"E69EF3CC-94CD-42E7-8926-F133B86387C0",
	"InvokeId":"t-7d2a745b412b4601b2d47f6a768d3***"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|500|InternalError.Dispatch|An error occurred when you dispatched the request.|发生未知错误。|
|404|InvalidInstance.NotFound|The specified instance does not exist.|指定的实例不存在。|
|403|MissingParam.Frequency|The frequency must be specified when you create a timed task.|请为周期任务设置执行频率。|
|404|Parameter.Disabled|Parameters cannot be passed in when the command customization function is disabled.|当您禁用命令自定义参数功能时，请不要传递自定义参数。|
|403|ParameterCount.ExceedLimit|The maximum number of parameters is exceeded.|您的自定义参数个数超过限制。|
|403|ParameterKey.ExceedLimit|The maximum length of a parameter name is exceeded.|您的自定义参数的参数名长度超过限制。|
|403|CmdContent.ExceedLimit|The maximum length of a command is exceeded.|您的命令内容过长，请精简您的命令内容。|
|403|ParameterKey.Duplicate|Parameter names cannot be duplicated.|请不要传递重复的参数名。|
|403|Parameter.NotMatched|The passed-in parameters do not match the parameters defined when you created the command.|传入的自定义参数与创建命令时定义的自定义参数不匹配。|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

