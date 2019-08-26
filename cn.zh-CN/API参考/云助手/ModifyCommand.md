# ModifyCommand {#doc_api_Ecs_ModifyCommand .reference}

修改一条云助手命令相关参数以及命令内容。

## 接口说明 {#description .section}

命令执行期间也允许修改，修改命令后，后续执行会按照新的命令内容执行。

您不能修改命令的类型，例如，如果命令是 Shell 命令（RunShellScript），则不能修改为 Bat 命令（RunBatScript）。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=ModifyCommand)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|CommandId|String|是|c-4d34302d02424c5c8e10281e3a315a05|命令 ID。您可以通过接口 [DescribeCommands](~~64843~~) 查询所有可用的 CommandId。

 |
|RegionId|String|是|cn-hangzhou|地域 ID。您可以调用 [DescribeRegions](~~25609~~) 查看最新的阿里云地域列表。

 |
|Action|String|否|ModifyCommand|系统规定参数。取值：ModifyCommand

 |
|CommandContent|String|否|c2VydmljZSB0b21jYXQgc3RhcnQ=|命令内容。

 |
|Description|String|否|UserGuide|命令描述，支持全字符集。长度不得超过100个字符。

 |
|Name|String|否|AlibabaCommand|命令名称，支持全字符集。长度不得超过 30 个字符。

 |
|Timeout|Long|否|120|超时时间。

 |
|WorkingDir|String|否|/home/|执行路径。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

https://ecs.aliyuncs.com/?Action=ModifyCommand
&CommandId=c-4d34302d02424c5c8e10281e3a315a05
&RegionId=cn-hangzhou
&Name=AlibabaCommand
&Description=UserGuide
&CommandContent=c2VydmljZSB0b21jYXQgc3RhcnQ=
&WorkingDir=/home/
&Timeout=120
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ModifyCommandResponse>
    "RequestId": "0DE9B41E-EF0D-40A0-BB43-37749C5BDA9C"
</ModifyCommandResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"0DE9B41E-EF0D-40A0-BB43-37749C5BDA9C"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|404|InvalidCmdType.NotFound|The specified command type does not exist.|指定的命令类型不存在。|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Ecs)

