# DeleteNetworkInterface {#DeleteNetworkInterface .reference}

删除弹性网卡（ENI）。

## 描述 {#section_tyd_kj4_ydb .section}

-   弹性网卡必须处于可用（`Available`）状态。
-   如果弹性网卡已经附加到 ECS 实例，必须先从实例分离（[DetachNetworkInterface](intl.zh-CN/API参考/弹性网卡/DetachNetworkInterface.md#)），才能删除弹性网卡。
-   删除弹性网卡之后：
    -   弹性网卡的主私有 IP 地址（`PrimaryIpAddress`）自动释放。
    -   被删除的弹性网卡退出所属的所有安全组。

## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：DeleteNetworkInterface|
|RegionId|String|是|所在地域 ID。您可以调用 [DescribeRegions](intl.zh-CN/API参考/地域/DescribeRegions.md#) 查看最新的阿里云地域列表。|
|NetworkInterfaceId|String|是|弹性网卡的 ID。|

## 返回参数 {#section_f54_lk5_xdb .section}

全是公共返回参数。参阅 [公共参数](intl.zh-CN/API参考/调用方式/公共参数.md#commonResponseParameters)。

## 示例 { .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=DeleteNetworkInterface
&RegionId=cn-hangzhou
&NetworkInterfaceId=[networkInterfaceId]
&<公共请求参数>
```

**返回示例** 

**XML 格式**

```
<DetachNetworkInterface>
    <RequestId>04F0F334-1335-436C-A1D7-6C044FExxxxx</RequestId>
</DetachNetworkInterface>
```

 **JSON 格式** 

```
{
    "RequestId": "04F0F334-1335-436C-A1D7-6C044FExxxxx",
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问 [API 错误中心](https://error-center.alibabacloud.com/status/product/Ecs)。

|错误代码|错误信息|HTTP 状态码|说明|
|:---|:---|:-------|:-|
|Abs.InvalidAccount.NotFound|The Account is not found or ak is expired.|403|您的阿里云账号不存在，或者您的 AccessKey 已经过期。|
|Forbidden.NotSupportRAM|This action does not support accessed by RAM mode.|403|不允许 RAM 用户执行该操作。|
|UnsupportedParameter|The parameters is unsupported.|400|该参数不存在，或者不支持该参数。|
|Forbidden.SubUser|The specified action is not available for you.|403|不允许 RAM 用户执行该操作。|
|InvalidOperation.DetachPrimaryEniNotAllowed|Detaching primary ENI from ECS instance is not allowed.|400|不允许从 ECS 实例上解绑主网卡。|
|MissingParameter|The input parameter that is mandatory for processing this request is not supplied.|400|缺少必需参数。|
|InvalidOperation.InvalidEniType|The operation is not allowed in the current ENI type.|403|当前弹性网卡类型不支持该操作。|

