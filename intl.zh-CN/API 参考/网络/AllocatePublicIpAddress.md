# AllocatePublicIpAddress {#AllocatePublicIpAddress .reference}

为一台实例分配一个公网 IP 地址。

## 描述 {#section_udj_c3n_ydb .section}

调用该接口时，您需要注意：

-   分配公网 IP 地址之前，实例必须处于 **运行中**（`Running`）或者 **已停止**（`Stopped`）状态。

-   当VPC类型实例已经绑定了 EIP，则无法再分配公网 IP。

-   一台实例只能分配一个公网 IP 地址。如果实例已经拥有一个公网 IP 地址，将报错 `AllocatedAlready`。

-   重启实例（[RebootInstance](intl.zh-CN/API 参考/实例/RebootInstance.md#)）或者启动实例（[StartInstance](intl.zh-CN/API 参考/实例/StartInstance.md#)）后，新的公网 IP 地址生效。

-   被 [安全控制](intl.zh-CN/API 参考/附录/安全锁定时的 API 行为.md#) 的实例的 `OperationLocks` 中标记了 `"LockReason" : "security"` 时，不能分配公网 IP 地址。


除分配公网 IP 之外，您还可以给实例绑定弹性公网 IP（EIP）。更多详情，请参阅 [AssociateEipAddress](../../../../intl.zh-CN/API 参考/弹性公网IP/AssociateEipAddress.md#)。

## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：AllocatePublicIpAddress|
|InstanceId|String|是|需要分配 IP 地址的实例 ID。|

## 返回参数 {#ResponseParameter .section}

|名称|类型|描述|
|:-|:-|:-|
|IpAddress|String|实例的公网 IP 地址|

## 示例 { .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=AllocatePublicIpAddress
&InstanceId=i-instance1
&<公共请求参数>
```

**返回示例** 

**XML 格式**

```
<AllocatePublicIpAddressResponse>
    <RequestId>F2EF6A3B-E345-46B9-931E-0EA094818567</RequestId>
    <IpAddress>10.1.149.159</IpAddress>
</AllocatePublicIpAddressResponse>
```

 **JSON 格式** 

```
{
    "RequestId": "F2EF6A3B-E345-46B9-931E-0EA094818567",
    "IpAddress": "10.1.149.159"
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问 [API 错误中心](https://error-center.alibabacloud.com/status/product/Ecs)。

|错误代码|错误信息|HTTP 状态码|说明|
|:---|:---|:-------|:-|
|InsufficientPublicIp|Ip address not found|400|公网 IP 地址资源目前库存不足，请稍后再试。|
|OperationDenied|Specified operation is denied as your instance is in VPC.|400|指定的 VPC 类型实例已绑定了 EIP。|
|AllocatedAlready|There is an IpAddress allocated already for the specified instance.|403|这台实例已经拥有一个公网 IP 地址。|
|IncorrectInstanceStatus|The current status of the resource does not support this operation.|403|分配公网 IP 地址之前，实例必须处于 **运行中**（`Running`）或者 **已停止**（`Stopped`）状态。|
|InstanceExpiredOrInArrears|The specified operation is denied as your prepay instance is expired \(prepay mode\) or in arrears \(afterpay mode\).|403|指定的 [包年包月](../../../../intl.zh-CN/产品定价/包年包月.md#) 实例已到期或者 [按量付费](../../../../intl.zh-CN/产品定价/按量付费.md#) 实例已欠费。|
|InstanceLockedForSecurity|The specified operation is denied as your instance is locked for security reasons.|403|实例目前被 [安全控制](intl.zh-CN/API 参考/附录/安全锁定时的 API 行为.md#)，拒绝任何操作。|
|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|404|指定的 `InstanceId` 不存在。|

