# CreateKeyPair {#CreateKeyPair .reference}

创建一对SSH密钥对。我们会为您保管密钥的公钥部分，并返回未加密的 PEM 编码的 `PKCS#8` 格式私钥。您需要自行妥善保管私钥部分。更多详情，请参阅[SSH 密钥对](../intl.zh-CN/产品简介/网络和安全性/SSH 密钥对.md#)。

## 描述 {#section_zjh_r4n_ydb .section}

除了调用CreateKeyPair创建密钥对之外，您还可以使用第三方工具创建密钥对，然后上传（[ImportKeyPair](intl.zh-CN/API 参考/镜像/ImportImage.md#)）到某一阿里云地域，其使用方法和我们为您创建的密钥对是一致的。

您在每个地域的密钥对数最高为500对。

## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：CreateKeyPair|
|RegionId|String|是|密钥对所在的地域ID。您可以调用[DescribeRegions](../intl.zh-CN/API 参考/地域/DescribeRegions.md#)查看最新的阿里云地域列表。|
|KeyPairName|String|是|密钥对名称。长度为\[2, 128\]个英文或中文字符。必须以大小字母或中文开头，不能以http://和https://开头。可以包含数字、半角冒号（:）、下划线（\_）或者连字符（-）。必须保持名称唯一性，支持所有的字符集编码格式。

|
|Tag.n.Key|String|否|密钥对的标签键。n的取值范围：\[1, 20\]。一旦传入该值，则不允许为空字符串。最多支持64个字符，不能以aliyun、acs:、http://或者https://开头。|
|Tag.n.Value|String|否|密钥对的标签值。n的取值范围：\[1, 20\]。一旦传入该值，可以为空字符串。最多支持128个字符，不能以aliyun、acs:、http://或者https://开头。|

## 返回参数 {#ResponseParameter .section}

|名称|类型|描述|
|:-|:-|:-|
|KeyPairName|String|密钥对名称。|
|KeyPairFingerPrint|String|密钥对的指纹。根据RFC4716定义的公钥指纹格式，采用MD5信息摘要算法。更多详情，请参阅 [RFC4716](http://tools.ietf.org/html/rfc4716)。|
|PrivateKeyBody|String|密钥对的私钥。PEM PKCS\#8格式的私钥部分。更多详情，请参阅*OpenSSL* [PKCS\#8](https://www.openssl.org/docs/apps/pkcs8.html)。|

## 示例 { .section}

**请求示例**

```
https://ecs.aliyuncs.com/?Action=CreateKeyPair
&RegionId=cn-qingdao
&KeyPairName=test
&<公共请求参数>
```

**返回示例**

**XML格式**

```
<CreateKeyPairResponse>
    <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
    <KeyPairName>test</KeyPairName>
    <KeyPairFingerPrint>89:f0:ba:62:ac:b8:aa:e1:61:5e:fd:81:69:86:6d:6b:f0:c0:5a:d7</KeyPairFingerPrint>
    <PrivateKeyBody>xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx</PrivateKeyBody>
</CreateKeyPairResponse>
```

**JSON格式**

```
{
    "RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E"
    "KeyPairName": "test"
    "KeyPairFingerPrint": "89:f0:ba:62:ac:b8:aa:e1:61:5e:fd:81:69:86:6d:6b:f0:c0:5a:d7"
    "PrivateKeyBody": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问[API错误中心](https://error-center.alibabacloud.com/status/product/Ecs)。

|错误代码|错误信息|HTTP状态码|说明|
|:---|:---|:------|:-|
|MissingParameter|The input parameter “RegionId” that is mandatory for processing this request is not supplied.|400|您必须指定`RegionId`参数。|
|InvalidKeyPairName.Malformed|Specified Key Pair name is not valid.|400|指定的`KeyPairName`不合法或者已重复。|
|QuotaExceed.KeyPair|The key pair quota exceeds.|403|您在每个地域的密钥对个数不能超过500对。|
|InvalidRegionId.NotFound|The specified RegionId does not exist.|404|指定的`RegionId`不存在。|

