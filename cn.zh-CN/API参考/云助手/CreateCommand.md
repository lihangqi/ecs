# CreateCommand {#doc_api_Ecs_CreateCommand .reference}

调用CreateCommand新建一条云助手命令。

## 接口说明 {#description .section}

-   您可以创建以下类型的命令：
    -   Windows实例适用的Bat脚本（RunBatScript）
    -   Windows实例适用的PowerShell脚本（RunPowerShellScript）
    -   Linux实例适用的Shell脚本（RunShellScript）
-   您可以通过指定参数`TimeOut`为命令设置在ECS实例中执行时最大的超时时间，命令执行超时后，[云助手客户端](~~64921~~)会强制终止命令进程，即取消命令的PID。
    -   对于单次执行，超时后，该命令针对指定的ECS实例的执行状态（[InvokeRecordStatus](~~64845~~)\)变为执行失败（Failed）。
    -   对于周期执行：
        -   周期执行的超时时间对每一次执行记录均有效。
        -   某次执行超时后，该次执行记录的状态（[InvokeRecordStatus](~~64845~~)）变为执行失败（Failed）。
        -   上次执行超时与否不影响下一次执行。
-   在一个地域下，您最多可以保有100条云助手命令。您也可以[提交工单](https://selfservice.console.aliyun.com/ticket/createIndex.htm)调整保有量上限。
-   您可以通过指定参数`WorkingDir`为命令指定执行路径。对于Linux实例，默认在管理员root用户的home目录下，具体为/root目录。对于Windows实例，默认在云助手客户端进程所在目录，例如，C:\\ProgramData\\aliyun\\assist\\$\(version\)。
-   您可以通过指定参数`EnableParameter=true`启用自定义参数功能。在设置`CommandContent`时可以通过`{{$(parameter)}}`的形式表示自定义参数，并在运行命令（[InvokeCommand](~~64841~~)）时，传入自定义参数键值对。例如，您在创建命令时，创建了`echo {{name}}`命令，在 `InvokeCommand`时，通过`Parameter`参数传入键值对`<name, Jack>`。则自定义参数将自动替换命令，您会得到一条新的命令，并在实例中执行`echo Jack`。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=CreateCommand&type=RPC&version=2014-05-26)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|CommandContent|String|是|ZWNobyAxMjM=|命令Base64编码后的内容。

 -   该参数的值必须使用Base64编码后传输，且脚本内容的大小在Base64编码之后不能超过16KB。
-   命令内容支持使用自定义参数形式，具体通过指定参数`EnableParameter=true`启用自定义参数功能：
    -   自定义参数用`{{}}`包含的方式定义，在`{{}}`内参数名前后的空格以及换行符会被忽略
    -   自定义参数个数不能超过20个
    -   自定义参数名允许a-zA-Z0-9-\_的组合，不支持其余字符，参数名不区分大小写
    -   单个参数名不能超过64字节

 |
|Name|String|是|Test|命令名称，支持全字符集。长度不得超过128个字符。

 |
|RegionId|String|是|cn-hangzhou|地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。

 |
|Type|String|是|RunShellScript|命令的类型。取值范围：

 -   RunBatScript：创建一个在Windows实例中运行的 Bat 脚本
-   RunPowerShellScript：创建一个在Windows实例中运行的PowerShell脚本
-   RunShellScript：创建一个在Linux实例中运行的Shell脚本

 |
|Action|String|否|CreateCommand|系统规定参数。取值：CreateCommand

 |
|Description|String|否|Test1|命令描述，支持全字符集。长度不得超过512个字符。

 |
|EnableParameter|Boolean|否|false|创建的命令是否使用自定义参数。

 默认值：false

 |
|Timeout|Long|否|3600|您创建的命令在ECS实例中执行时最大的超时时间，单位为秒。当因为某种原因无法运行您创建的命令时，会出现超时现象。超时后，会强制终止命令进程，即取消命令的PID。

 默认值：3600

 |
|WorkingDir|String|否|/home/|您创建的命令在ECS实例中运行的目录。默认值：

 -   对于Linux实例，默认在管理员root用户的home目录下，具体为/root目录。
-   对于Windows实例，默认在云助手客户端进程所在目录，例如，C:\\ProgramData\\aliyun\\assist\\$\(version\)。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|CommandId|String|c-7d2a745b412b4601b2d47f6a768d3\*\*\*|命令ID

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=CreateCommand
&CommandContent=ZWNobyB7e25hbWV9fSA=
&Name=Test
&RegionId=cn-hangzhou
&Type=RunShellScript
&Description=Test1
&WorkingDir=/home/
&Timeout=3600
&EnableParameter=true
&<公共请求参数>
```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<CreateCommandResponse>
      <RequestId>E69EF3CC-94CD-42E7-8926-F133B86387C0</RequestId>
      <CommandId>c-7d2a745b412b4601b2d47f6a768d3***</CommandId>
</CreateCommandResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"E69EF3CC-94CD-42E7-8926-F133B86387C0",
	"CommandId":"c-7d2a745b412b4601b2d47f6a768d3***"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|500|InternalError.Dispatch|An error occurred when you dispatched the request.|发生未知错误。|
|403|InvalidCmdType.NotFound|The specified command type does not exist.|指定的命令类型不存在。|
|403|CmdName.ExceedLimit|The length of the command name exceeds the upper limit.|请精简您的命令名称。|
|403|CmdDesc.ExceedLimit|The length of the command description exceeds the upper limit.|请精简您的命令描述内容。|
|403|CmdCount.ExceedQuota|The total number of commands in the current region exceeds the quota.|当前地域下的云助手命令数量已超出限。|
|403|CmdParam.EmptyKey|You must specify the parameter names.|自定义参数的参数名不能为空。|
|403|CmdParam.InvalidParamName|Invalid parameter name. The name can contain only lowercase letters \(a to z\), uppercase letters \(A to Z\), numbers \(0 to 9\), hyphens \(-\), and underscores \(\_\).|自定义参数的参数名不合法，只允许a-zA-Z0-9-\_ 的组合。|
|403|CmdParamName.ExceedLimit|The maximum length of a parameter name is exceeded.|您的自定义参数的参数名长度超过限制。|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

