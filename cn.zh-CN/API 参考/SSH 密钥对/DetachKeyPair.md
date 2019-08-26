# DetachKeyPair {#DetachKeyPair .reference}

为一台或者多台 Linux 实例解绑 SSH 密钥对。

## 描述 {#section_a1k_4qn_ydb .section}

使用该接口时，请注意：

-   解绑 SSH 密钥对后，您需要重启实例（[RebootInstance](intl.zh-CN/API 参考/实例/RebootInstance.md#)）使更改生效。

-   解绑 SSH 密钥对后，实例默认使用用户名和密码的验证方式。


## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：DetachKeyPair|
|RegionId|String|是|SSH 密钥对所在的地域 ID。您可以调用 [DescribeRegions](intl.zh-CN/API 参考/地域/DescribeRegions.md#) 查看最新的阿里云地域列表。|
|KeyPairName|String|是|SSH 密钥对名称。|
|InstanceIds|String|否|解绑 SSH 密钥对的实例 ID。取值可以由多台实例 ID 组成一个 JSON 数组，格式为 \["i-xxxxxxxxx", "i-yyyyyyyyy", … "i-zzzzzzzzz"\]，最多支持 50 个 ID，ID 之间用半角逗号（,）隔开。|

## 返回参数 {#section_f54_lk5_xdb .section}

全是公共返回参数。参阅 [公共参数](intl.zh-CN/API 参考/快速入门/公共参数.md#)。

## 示例 { .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=DetachKeyPair
&RegionId=cn-qingdao
&InstanceIds=["i-xxxxxxx", "i-yyyyyyy"]
&KeyPairName=test
&<公共请求参数>
```

**返回示例** 

**XML 格式**

```
<DetachKeyPairResponse>
    <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</DetachKeyPairResponse>
```

 **JSON 格式** 

```
{
    "RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E"
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问 [API 错误中心](https://error-center.alibabacloud.com/status/product/Ecs)。

|错误代码|错误信息|HTTP 状态码|说明|
|:---|:---|:-------|:-|
|MissingParameter|The input parameter “RegionId” that is mandatory for processing this request is not supplied.|400|您需要指定参数 `RegionId`。或者您暂时无法使用该地域的资源。|
|DependencyViolation.WindowsInstance|The instance creating is windows, cannot use ssh key pair to login|403|Windows 实例不支持 SSH 密钥对。|
|InvalidKeyPairName.NotFound|The specified KeyPairName does not exist.|404|指定的 `KeyPairName` 不存在。|
|InvalidRegionId.NotFound|The specified RegionId does not exist.|404|指定的 `RegionId` 不存在。|

