# ImportKeyPair {#ImportKeyPair .reference}

导入由其他工具产生的 RSA 密钥对的公钥部分。导入密钥对后，我们会为您保管公钥部分，您需要自行妥善保存密钥对的私钥部分。

## 描述 {#section_qqb_kpn_ydb .section}

调用该接口时，您需要注意：

-   您在每个地域的密钥对数最高为 500 对。

-   导入的密钥对的必须支持下列任一种加密方式：

    -   rsa
    -   dsa
    -   ssh-rsa
    -   ssh-dss
    -   ecdsa
    -   ssh-rsa-cert-v00@openssh.com
    -   ssh-dss-cert-v00@openssh.com
    -   ssh-rsa-cert-v01@openssh.com
    -   ssh-dss-cert-v01@openssh.com
    -   ecdsa-sha2-nistp256-cert-v01@openssh.com
    -   ecdsa-sha2-nistp384-cert-v01@openssh.com
    -   ecdsa-sha2-nistp521-cert-v01@openssh.com

## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：ImportKeyPair|
|RegionId|String|是|地域 ID。您可以调用 [DescribeRegions](intl.zh-CN/API 参考/地域/DescribeRegions.md#) 查看最新的阿里云地域列表。|
|PublicKeyBody|String|是|密钥对的公钥内容。|
|KeyPairName|String|是|密钥对名称。必须保持名称唯一性。-   长度为 \[2, 128\] 个字符。
-   必须以大小字母或中文开头，可包含数字、小数点（.）、下划线（\_）或者短横线（-）。
-   支持所有的字符集编码格式。
-   不能以 http:// 和 https:// 开头。

|

## 返回参数 {#ResponseParameter .section}

|名称|类型|描述|
|:-|:-|:-|
|KeyPairName|String|密钥对名称。|
|KeyPairFingerPrint|String|密钥对的指纹。根据 RFC4716 定义的公钥指纹格式，采用 MD5 信息摘要算法。更多详情，请参阅 [RFC4716](http://tools.ietf.org/html/rfc4716)。|

## 示例 { .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=ImportKeyPair
&RegionId=cn-qingdao
&PublicKeyBody=xxxxxxxxxxxxxx
&KeyPairName=test
&<公共请求参数>
```

**返回示例** 

**XML 格式**

```
<ImportKeyPairResponse>
    <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
    <KeyPairName>test</KeyPairName>
    <KeyPairFingerPrint> 89:f0:ba:62:ac:b8:aa:e1:61:5e:fd:81:69:86:6d:6b:f0:c0:5a:d7</KeyPairFingerPrint>
</ImportKeyPairResponse>
```

 **JSON 格式** 

```
{
    "RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E"
    "KeyPairName": "test"
    "KeyPairFingerPrint": "89:f0:ba:62:ac:b8:aa:e1:61:5e:fd:81:69:86:6d:6b:f0:c0:5a:d7"
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问 [API 错误中心](https://error-center.alibabacloud.com/status/product/Ecs)。

|错误代码|错误信息|HTTP 状态码|说明|
|:---|:---|:-------|:-|
|MissingParameter|The input parameter “RegionId” that is mandatory for processing this request is not supplied.|400|您必须指定 `RegionId`参数。|
|InvalidPublicKeyBody.Malformed|The PublicKeyBody format is not supported.|400|指定的 `PublicKeyBody` 格式不正确。|
|InvalidKeyPairName.Malformed|Specified Key Pair name is not valid.|400|指定的 `KeyPairName`不合法或者已重复。|
|InvalidRegionId.NotFound|The specified RegionId does not exist.|404|指定的 `RegionId` 不存在。|

