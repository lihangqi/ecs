# ModifyDiskChargeType {#ModifyDiskChargeType .reference}

修改一台实例上挂载的一块或最多 16 块磁盘的计费方式。

## 描述 {#Description .section}

使用该接口时，请注意：

-   包年包月磁盘转换为按量付费磁盘时，适用于包年包月实例上挂载的包年包月云盘。

-   按量付费磁盘转换为包年包月磁盘时，适用于预付费实例上挂载的按量付费数据盘，或者按量付费实例上挂载的按量付费数据盘。

-   挂载的实例不能为欠费停机状态。

-   更换计费方式后，默认自动扣费。您需要确保账户余额充足，否则会生成异常订单，此时只能作废订单。如果您的账户余额不足，可以将参数 `AutoPay` 置为 `false`，此时会生成正常的未支付订单，您可以登录[ECS管理控制台](https://ecs.console.aliyun.com/)支付。

-   每块磁盘更换计费方式的次数不能超过三次，即价格差退款不会超过三次。

-   更换计费方式前后的价格差退款会退还到您的原付费方式中，已使用的代金券不退回。

-   每块磁盘成功修改计费方式一次，五分钟内不能再次修改。


## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值： ModifyDiskChargeType|
|DiskIds|String|是|磁盘 ID 列表，一个带有格式的 Json Array：\[“d-xxxxxxxxx”, “d-yyyyyyyyy”, … “d-zzzzzzzzz”\]，最多支持 16 个 ID，用半角逗号（,）隔开。|
|InstanceId|String|是|磁盘挂载的实例 ID。|
|RegionId|String|是|实例所属的地域 ID。您可以调用[DescribeRegions](../intl.zh-CN/API 参考/地域/DescribeRegions.md#)查看最新的阿里云地域列表。|
|DiskChargeType|String|否|磁盘计费方式。取值范围：-   PrePaid（默认）：按量付费数据盘转换为包年包月数据盘。
-   PostPaid：包年包月数据盘转换为按量付费数据盘。

|
|DryRun|Boolean|否|是否只预检此次请求。-   true：发送检查请求，不会查询资源状况。检查项包括AccessKey是否有效、RAM用户的授权情况和是否填写了必需参数。如果检查不通过，则返回对应错误。如果检查通过，会返回错误码`DryRunOperation`。
-   false：发送正常请求，通过检查后返回2XX HTTP状态码并直接查询资源状况。

默认值：false

|
|AutoPay|Boolean|否|是否自动支付。取值范围：-   true（默认）：自动支付。您需要确保账户余额充足，如果账户余额不足会生成异常订单，只能作废订单。
-   false：只生成订单不扣费。如果您的账户余额不足，会生成正常的未支付订单，此订单可登录 ECS 控制台支付。

|
|ClientToken|String|否|保证请求幂等性。从您的客户端生成一个参数值，确保不同请求间该参数值唯一。只支持ASCII字符，且不能超过64个字符。更多详情，请参阅[如何保证幂等性](../intl.zh-CN/API 参考/附录/如何保证幂等性.md#)。

|

## 返回参数 {#ResponseParameter .section}

|名称|类型|描述|
|:-|:-|:-|
|OrderId|Long|生成的订单 ID|

## 示例 { .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=ModifyDiskChargeType
&RegionId=cn-hangzhou
&DiskIds=["d-xxxxx1","d-xxxxx2"]
&InstanceId=i-xxxxx1
&AutoPay=false
&ClientToken=xxxxxxxxxxxxxx
&<公共请求参数>
```

**返回示例** 

**XML格式**

```
<ModifyDiskChargeType>
      <RequestId>04F0F334-1335-436C-A1D7-6C044FE73368</RequestId>
      <Order>1011111111111111</Order>
</ModifyDiskChargeType>
```

**JSON格式** 

```
{
    "RequestId": "04F0F334-1335-436C-A1D7-6C044FE73368",
    "Order": 1011111111111111,
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问[API错误中心](https://error-center.alibabacloud.com/status/product/Ecs)。

|错误代码|错误信息|HTTP状态码|说明|
|:---|:---|:------|:-|
|Account.Arrearage|Your account has an outstanding payment.|400|您的账号已经欠费。|
|IdempotenceParamNotMatch|Request uses a client token in a previous request but is not identical to that request.|400|与相同 ClientToken 的请求参数不符合。|
|InvalidClientToken.ValueNotSupported|The ClientToken provided is invalid.|400|ClientToken 参数值不合法，只支持 ASCII 字符。|
|InvalidInstance.UnpaidOrder|The specified instance has unpaid order.|400|当前实例存在未支付的订单。|
|InvalidInstanceId.Released|The specified instance has been released.|400|指定实例已被释放。|
|OrderCreationFailed|Order creation failed, please check your params and try it again later.|400|创建订单失败。|
|Throttling|You have made too many requests within a short time; your request is denied due to request throttling.|400|操作过于频繁，请稍后再试。|
|ChargeTypeViolation|The operation is not permitted due to charge type of the instance.|403|当前实例的计费方式不支持此操作。|
|InvalidAccountStatus.NotEnoughBalance|Your account does not have enough balance.|403|账户余额不足。|
|InvalidPayMethod|The specified billing method is invalid.|403|指定的计费方式不存在。|
|InvalidUser.PassRoleForbidden|The RAM user does not have privilege to pass a role.|403|您使用的RAM用户账号暂不具有`PassRole`的权限，请联系主账号拥有者[授权](../intl.zh-CN/快速入门/为 RAM 用户授权.md#)PassRole权限。|
|InvalidDiskIds.NotFound|Some of the specified data disks do not exist.|404|磁盘 ID 不存在。|
|InvalidDiskIds.NotPortable|The specified DiskId is not portable.|404|不可卸载磁盘不支持修改磁盘计费方式。|
|InvalidRegionId.NotFound|The RegionId provided does not exist.|404|指定的 RegionId 不存在。|
|PaymentMethodNotFound|No billing method has been registered on the account.|404|您还没有选择付款方式。|
|InternalError|The request processing has failed due to some unknown error, exception or failure.|500|内部错误。|

