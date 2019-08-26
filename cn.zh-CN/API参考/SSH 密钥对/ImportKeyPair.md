# ImportKeyPair {#doc_api_Ecs_ImportKeyPair .reference}

调用ImportKeyPair导入由其他工具产生的 RSA 密钥对的公钥部分。导入密钥对后，我们会为您保管公钥部分，您需要自行妥善保存密钥对的私钥部分。

## 接口说明 {#description .section}

调用该接口时，您需要注意，您在每个地域的密钥对数最高为 500 对。

导入的密钥对的必须支持下列任一种加密方式：

-   `rsa`
-   `dsa`
-   `ssh-rsa`
-   `ssh-dss`
-   `ecdsa`
-   `ssh-rsa-cert-v00@openssh.com`
-   `ssh-dss-cert-v00@openssh.com`
-   `ssh-rsa-cert-v01@openssh.com`
-   `ssh-dss-cert-v01@openssh.com`
-   `ecdsa-sha2-nistp256-cert-v01@openssh.com`
-   `ecdsa-sha2-nistp384-cert-v01@openssh.com`
-   `ecdsa-sha2-nistp521-cert-v01@openssh.com`

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=ImportKeyPair)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|KeyPairName|String|是|FinanceJoshuaV24|密钥对名称。必须保持名称唯一性。 长度为2~128个英文或中文字符。必须以大小字母或中文开头，不能以 http:// 和 https:// 开头。可以包含数字、半角冒号（:）、下划线（\_）或者连字符（-）。

 |
|PublicKeyBody|String|是|xxxxxxxxxxxxxx|密钥对的公钥内容。

 |
|RegionId|String|是|cn-hangzhou|地域 ID。您可以调用 [DescribeRegions](~~25609~~) 查看最新的阿里云地域列表。

 |
|Action|String|否|ImportKeyPair|系统规定参数。取值：ImportKeyPair

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|KeyPairFingerPrint|String|89:f0:ba:62:ac:b8:aa:e1:61:5e:fd:81:69:86:6d:6b:f0:c0:5a:\*\*|密钥对的指纹。根据 RFC4716 定义的公钥指纹格式，采用 MD5 信息摘要算法。

 |
|KeyPairName|String|FinanceJoshauV24|密钥对名称。

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

https://ecs.aliyuncs.com/?Action=ImportKeyPair
&RegionId=cn-qingdao
&PublicKeyBody=xxxxxxxxxxxxxx
&KeyPairName=test
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ImportKeyPairResponse>
  <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
  <KeyPairName>test</KeyPairName>
  <KeyPairFingerPrint>89:f0:ba:62:ac:b8:aa:e1:61:5e:fd:81:69:86:6d:6b:f0:c0:5a:**</KeyPairFingerPrint>
</ImportKeyPairResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E",
	"KeyPairFingerPrint":"89:f0:ba:62:ac:b8:aa:e1:61:5e:fd:81:69:86:6d:6b:f0:c0:5a:**",
	"KeyPairName":"test"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InvalidKeyPairName.Malformed|Specified Key Pair name is not valid.|密钥对名称不合法,|
|403|QuotaExceed.KeyPair|The key pair quota exceeds.|密钥对数量已达上限,|
|400|InvalidPublicKeyBody.Malformed|The PublicKeyBody format is not supported.|公钥格式不支持,|
|400|MissingParameter|The input parameter "PublicKeyBody" that is mandatory for processing this request is not supplied.|未提供必需的 PublicKeyBody。|
|400|KeyPair.AlreadyExist|The key pair already exist.|密钥对已存在，请不要重复添加。|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

