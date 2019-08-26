# DeleteKeyPairs {#DeleteKeyPairs .reference}

删除一对或者多对 SSH 密钥对。删除 SSH 密钥对后，我们不再为您保存该 SSH 密钥对，但是已经绑定的实例可以正常使用该 SSH 密钥对，其 SSH 密钥对名称仍然显示在实例详情中。

## 描述 {#section_kq4_trn_ydb .section}

调用该接口时，您需要注意：

-   删除 SSH 密钥对后，您将无法通过 [DescribeKeyPairs](intl.zh-CN/API 参考/SSH 密钥对/DescribeKeyPairs.md#) 查询该 SSH 密钥对。

-   查询实例信息时（[DescribeInstances](intl.zh-CN/API 参考/实例/DescribeInstances.md#)），会显示 SSH 密钥对名称（`KeyPairNames`），不再显示该 SSH 密钥对的其他信息。


## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：DeleteKeyPairs|
|RegionId|String|是|SSH 密钥对所在的地域。您可以调用 [DescribeRegions](intl.zh-CN/API 参考/地域/DescribeRegions.md#) 查看最新的阿里云地域列表。|
|KeyPairNames|String|是|SSH 密钥对名称。取值可以由多个 SSH 密钥对名称组成一个 JSON 数组，格式为 \["key-xxxxxxxxx", "key-yyyyyyyyy", … "key-zzzzzzzzz"\]，最多支持 100 对 SSH 密钥对，名称之间用半角逗号（,）隔开。|

## 返回参数 {#section_f54_lk5_xdb .section}

全是公共返回参数。参阅 [公共参数](intl.zh-CN/API 参考/快速入门/公共参数.md#)。

## 示例 { .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=DeleteKeyPairs
&RegionId=cn-qingdao
&KeyPairNames=test
&<公共请求参数>
```

**返回示例** 

**XML 格式**

```
<DeleteKeyPairsResponse>
    <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</DeleteKeyPairsResponse>
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
|MissingParameter|The input parameter RegionId that is mandatory for processing this request is not supplied.|400|您需要指定参数 `RegionId`。或者您暂时无法使用该地域的资源。|
|MissingParameter|The input parameter KeyPairName that is mandatory for processing this request is not supplied.|400|您需要指定参数 `KeyPairName`。|
|InvalidRegionId.NotFound|The specified RegionId does not exist.|404|指定的 `RegionId` 不存在。|

