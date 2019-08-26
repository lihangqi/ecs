# DeleteKeyPairs {#doc_api_999672 .reference}

删除一对或者多对 SSH 密钥对。删除 SSH 密钥对后，我们不再为您保存该 SSH 密钥对，但是已经绑定的实例可以正常使用该 SSH 密钥对，其 SSH 密钥对名称仍然显示在实例详情中。

## 描述 {#description .section}

调用该接口时，您需要注意：

-   删除 SSH 密钥对后，您将无法通过 [DescribeKeyPairs](~~51773~~) 查询该 SSH 密钥对。
-   查询实例信息时（[DescribeInstances](~~25506~~)），会显示 SSH 密钥对名称（KeyPairNames），不再显示该 SSH 密钥对的其他信息。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=DeleteKeyPairs)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|KeyPairNames|String|是|\["key-xxxxxxxxx", "key-yyyyyyyyy", … "key-zzzzzzzzz"\]|SSH 密钥对名称。取值可以由多个 SSH 密钥对名称组成一个 JSON 数组，最多支持 100 对 SSH 密钥对，名称之间用半角逗号（,）隔开。

 |
|RegionId|String|是|cn-hangzhou|SSH 密钥对所在的地域。您可以调用 [DescribeRegions](~~25609~~) 查看最新的阿里云地域列表。

 |
|Action|String|否|DeleteKeyPairs|系统规定参数。取值：DeleteKeyPairs

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。无论调用接口成功与否，我们都会返回请求 ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

https://ecs.aliyuncs.com/?Action=DeleteKeyPairs
&RegionId=cn-qingdao
&KeyPairNames=test
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DeleteKeyPairsResponse>
  <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</DeleteKeyPairsResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|MissingParameter|The input parameter "KeyPairNames" that is mandatory for processing this request is not supplied.|未提供必需的 KeyPairNames。|
|400|InvalidKeyPairNames.ValueNotSupported|The specified parameter "KeyPairNames" is not valid.|密钥对名称不合法,|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Ecs)

