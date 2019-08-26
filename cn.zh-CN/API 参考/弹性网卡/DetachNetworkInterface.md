# DetachNetworkInterface {#DetachNetworkInterface .reference}

从一台实例上分离一个弹性网卡（ENI）。

## 描述 {#section_u1n_s34_ydb .section}

调用该接口时，您需要注意：

-   不允许分离实例主网卡。

-   弹性网卡必须处于 **解绑中**（`Detaching`）或者 **已绑定**（`InUse`）状态。

-   实例必须处于 **运行中**（`Running`）或者 **已停止**（`Stopped`）状态。


## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：DetachNetworkInterface|
|RegionId|String|是|实例所在地域的 ID。您可以调用 [DescribeRegions](intl.zh-CN/API 参考/地域/DescribeRegions.md#) 查看最新的阿里云地域列表。|
|NetworkInterfaceId|String|是|弹性网卡 ID。|
|InstanceId|String|是|实例 ID。|

## 返回参数 {#ResponseParameter .section}

全是公共返回参数。参阅[公共返回参数](../intl.zh-CN/API 参考/快速入门/公共参数.md#commonResponseParameters)。

## 示例 { .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=DetachNetworkInterface
&RegionId=cn-hangzhou
&NetworkInterfaceId=[networkInterfaceId]
&InstanceId=AY121018033933eaxxxxx
&<公共请求参数>
```

**返回示例** 

**XML 格式**

```
<DetachNetworkInterfaceResponse>
    <RequestId>04F0F334-1335-436C-A1D7-6C044FExxxxx</RequestId>
</DetachNetworkInterfaceResponse>
```

**JSON 格式** 

```
{
    "RequestId": "04F0F334-1335-436C-A1D7-6C044FExxxxx",
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问[API错误中心](https://error-center.alibabacloud.com/status/product/Ecs)。

|错误代码|错误信息|HTTP状态码|说明|
|:---|:---|:------|:-|
|UnsupportedParameter|The parameters is unsupported.|400|该参数不存在，或者不支持该参数。|
|InvalidOperation.InvalidEcsState|The operation is not allowed in the current ECS state.|400|当前 ECS 实例状态不支持该操作。|
|InvalidOperation.DetachPrimaryEniNotAllowed|Detaching primary ENI from ECS instance is not allowed.|400|不允许从 ECS 实例上解绑主网卡。|
|MissingParameter|The input parameter that is mandatory for processing this request is not supplied.|400|缺少必需参数。|
|Forbidden.SubUser|The specified action is not available for you.|403|不允许 RAM 用户执行该操作。|
|Abs.InvalidAccount.NotFound|The Account is not found or ak is expired.|403|您的阿里云账号不存在，或者您的 AccessKey 已经过期。|
|Forbidden.NotSupportRAM|This action does not support accessed by RAM mode.|403|不允许 RAM 用户执行该操作。|
|EniPerInstanceLimitExceeded|The number of ENI exceeds the limit for the type of instance you are trying to launch.|403|弹性网卡的数量超过了指定实例类型允许的最大值。|
|InvalidOperation.InvalidEniType|The operation is not allowed in the current ENI type.|403|当前弹性网卡类型不支持该操作。|
|InvalidEcsId.NotFound|The specified EcsId is not found.|404|指定的实例 ID 不存在。|

