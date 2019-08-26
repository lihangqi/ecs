# AttachKeyPair {#doc_api_999669 .reference}

绑定一个 SSH 密钥对到一台或多台 Linux 实例。

## 描述 {#description .section}

当您使用该接口时，需要注意：

-   Windows 实例不支持 SSH 密钥对。
-   绑定 SSH 密钥对后，将禁用用户名加密码的验证方式。
-   如果实例处于 运行中（Running）状态，重启实例（[RebootInstance](~~25502~~)）后，SSH 密钥对生效。
-   如果实例处于 已停止（Stopped）状态，启动实例（[StartInstance](~~25500~~)）后，SSH 密钥对生效。
-   如果实例已经绑定了 SSH 密钥对，新的 SSH 密钥对自动替换原来的 SSH 密钥对。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=AttachKeyPair)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|InstanceIds|String|是|\["i-xxxxxxxxx", "i-yyyyyyyyy", … "i-zzzzzzzzz"\]|绑定 SSH 密钥对的实例 ID。取值可以由多台实例 ID 组成一个 JSON 数组，最多支持 50 个 ID，ID 之间用半角逗号（,）隔开。

 |
|KeyPairName|String|是|FinanceJoshuaV25|SSH 密钥对名称。

 |
|RegionId|String|是|cn-hangzhou|SSH 密钥对所在的地域 ID。您可以调用 [DescribeRegions](~~25609~~) 查看最新的阿里云地域列表。

 |
|Action|String|否|AttachKeyPair|系统规定参数。取值：AttachKeyPair

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|FailCount|String|0|绑定密钥对失败的实例数量。

 |
|KeyPairName|String|FinanceJoshuaV25|密钥对的名称。

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。

 |
|Results| | |绑定密钥对是否成功或失败的结果集合。

 |
|└Code|String|200|传递的操作状态码，其中200表示操作成功。

 |
|└InstanceId|String|i-instanceid1|实例ID。

 |
|└Message|String|successful|传递的操作信息，当code=200时，message为successful。

 |
|└Success|String|true|此次操作是否成功。

 |
|TotalCount|String|2|绑定密钥对的实例总数量

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

https://ecs.aliyuncs.com/?Action=AttachKeyPair
&InstanceIds=["i-xxxxxxxxx", "i-yyyyyyyyy", … "i-zzzzzzzzz"]
&KeyPairName=FinanceJoshuaV25
&RegionId=cn-hangzhou
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<AttachKeyPairResponse>
  <TotalCount>2</TotalCount>
  <RequestId>4ADF7A06-66BD-4FBF-A2ED-2364E41D8C06</RequestId>
  <Results>
    <Result>
      <Message>successful</Message>
      <InstanceId>i-m5eg7be9ndloji64jknv</InstanceId>
      <Success>true</Success>
      <Code>200</Code>
    </Result>
    <Result>
      <Message>successful</Message>
      <InstanceId>i-m5e25x2mwr0hk33dwv0h</InstanceId>
      <Success>true</Success>
      <Code>200</Code>
    </Result>
  </Results>
  <FailCount>0</FailCount>
</AttachKeyPairResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"TotalCount":2,
	"RequestId":"4ADF7A06-66BD-4FBF-A2ED-2364E41D8C06",
	"Results":{
		"Result":[
			{
				"Message":"successful",
				"InstanceId":"i-m5eg7be9ndloji64jknv",
				"Success":true,
				"Code":"200"
			},
			{
				"Message":"successful",
				"InstanceId":"i-m5e25x2mwr0hk33dwv0h",
				"Success":true,
				"Code":"200"
			}
		]
	},
	"FailCount":0
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|403|DependencyViolation.WindowsInstance|The instance creating is windows, cannot use ssh key pair to login|指定的windows实例不支持解绑keypair。|
|400|DependencyViolation.IoOptimize|The specified parameter InstanceIds is not valid.|指定的实例 ID 不合法。|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Ecs)

