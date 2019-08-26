# AttachKeyPair {#AttachKeyPair .reference}

绑定一个 SSH 密钥对到一台或多台 Linux 实例。

## 描述 {#section_bqq_wpn_ydb .section}

当您使用该接口时，需要注意：

-   Windows 实例不支持 SSH 密钥对。

-   绑定 SSH 密钥对后，将禁用用户名加密码的验证方式。

-   如果实例处于 **运行中**（`Running`）状态，重启实例（[RebootInstance](cn.zh-CN/API 参考/实例/RebootInstance.md#)）后，SSH 密钥对生效。

-   如果实例处于 **已停止**（`Stopped`）状态，启动实例（[StartInstance](cn.zh-CN/API 参考/实例/StartInstance.md#)）后，SSH 密钥对生效。

-   如果实例已经绑定了 SSH 密钥对，新的 SSH 密钥对自动替换原来的 SSH 密钥对。


## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：AttachKeyPair|
|RegionId|String|是|SSH 密钥对所在的地域 ID。您可以调用 [DescribeRegions](cn.zh-CN/API 参考/地域/DescribeRegions.md#) 查看最新的阿里云地域列表。|
|KeyPairName|String|是|SSH 密钥对名称。|
|InstanceIds|String|是|绑定 SSH 密钥对的实例 ID。取值可以由多台实例 ID 组成一个 JSON 数组，格式为 \["i-xxxxxxxxx", "i-yyyyyyyyy", … "i-zzzzzzzzz"\]，最多支持 50 个 ID，ID 之间用半角逗号（,）隔开。|

## 返回参数 {#section_f54_lk5_xdb .section}

全是公共返回参数。参阅 [公共参数](cn.zh-CN/API 参考/快速入门/公共参数.md#)。

## 示例 { .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=AttachKeyPair
&RegionId=cn-qingdao
&KeyPairName=test
&InstanceIds=["i-XXXXX"]
&<公共请求参数>
```

**返回示例** 

**XML 格式**

```
<AttachKeyPairResponse>
    <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</AttachKeyPairResponse>
```

 **JSON 格式** 

```
{
    "RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E"
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问 [API 错误中心](https://error-center.aliyun.com/status/product/Ecs)。

|错误代码|错误信息|HTTP 状态码|说明|
|:---|:---|:-------|:-|
|MissingParameter|The input parameter “RegionId” that is mandatory for processing this request is not supplied.|400|您需要指定参数 `RegionId`。或者您暂时无法使用该地域的资源。|
|DependencyViolation.WindowsInstance|The instance creating is window, cannot use ssh key pair to login|403|Windows 实例不支持 SSH 密钥对。|
|InvalidKeyPairName.NotFound|The specified KeyPairName does not exist in our records.|404|指定的 `KeyPairName` 不存在。|
|InvalidRegionId.NotFound|The specified RegionId does not exist.|404|指定的 `RegionId` 不存在。|

