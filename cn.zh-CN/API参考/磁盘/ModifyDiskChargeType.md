# ModifyDiskChargeType {#doc_api_999556 .reference}

修改一台实例上挂载的一块或最多 16 块磁盘的计费方式。

## 描述 {#description .section}

更换计费方式后，默认自动扣费。您需要确保账户余额充足，否则会生成异常订单，此时只能作废订单。如果您的账户余额不足，可以将参数 AutoPay 置为 false，此时会生成正常的未支付订单，您可以登录 [ECS 管理控制台](https://ecs.console.aliyun.com/)支付。

使用该接口时，请注意：

-   包年包月磁盘转换为按量付费磁盘时，适用于包年包月实例上挂载的包年包月云盘。
-   按量付费磁盘转换为包年包月磁盘时，适用于预付费实例上挂载的按量付费数据盘，或者按量付费实例上挂载的按量付费数据盘。
-   挂载的实例不能为欠费停机状态。
-   每块磁盘更换计费方式的次数不能超过三次，即价格差退款不会超过三次。
-   更换计费方式前后的价格差退款会退还到您的原付费方式中，已使用的代金券不退回。
-   每块磁盘成功修改计费方式一次，五分钟内不能再次修改。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=ModifyDiskChargeType)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|DiskIds|String|是|\[“d-xxxxxxxxx”, “d-yyyyyyyyy”, … “d-zzzzzzzzz”\]|磁盘 ID 列表，一个带有格式的 Json Array，最多支持 16 个 ID，用半角逗号（,）隔开。

 |
|InstanceId|String|是|i-instanceid1|磁盘挂载的实例 ID。

 |
|RegionId|String|是|cn-hangzhou|实例所属的地域 ID。您可以调用 [DescribeRegions](~~25609~~) 查看最新的阿里云地域列表。

 |
|Action|String|否|ModifyDiskChargeType|系统规定参数。取值： ModifyDiskChargeType

 |
|AutoPay|Boolean|否|true|是否自动支付。取值范围：

 -   true（默认）：自动支付。您需要确保账户余额充足，如果账户余额不足会生成异常订单，只能作废订单。
-   false：只生成订单不扣费。如果您的账户余额不足，会生成正常的未支付订单，此订单可登录 ECS 控制台支付。

 |
|ClientToken|String|否|123e4567-e89b-12d3-a456-426655440000|保证请求幂等性。从您的客户端生成一个参数值，确保不同请求间该参数值唯一。只支持ASCII字符，且不能超过64个字符。更多详情，请参阅如何保证幂等性。

 |
|DiskChargeType|String|否|PostPaid|磁盘计费方式。取值范围：

 -   PrePaid（默认）：按量付费数据盘转换为包年包月数据盘。
-   PostPaid：包年包月数据盘转换为按量付费数据盘。

 |
|OwnerAccount|String|否|ECSforCloud@Alibaba.com|RAM 用户的账号登录名称。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|OrderId|String|1111111111111111111111110|生成的订单 ID。

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

https://ecs.aliyuncs.com/?Action=ModifyDiskChargeType
&DiskIds=["d-diskid1"]
&InstanceId=i-instanceid1
&RegionId=cn-hangzhou
&AutoPay=true
&ClientToken=123e4567-e89b-12d3-a456-426655440000
&DiskChargeType=PostPaid
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ModifyDiskChargeType>
  <RequestId>04F0F334-1335-436C-A1D7-6C044FE73368</RequestId>
  <Order>1011111111111111</Order>
</ModifyDiskChargeType>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"04F0F334-1335-436C-A1D7-6C044FE73368",
	"Order":1011111111111111
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|404|InvalidRegionId.NotFound|The RegionId provided does not exist.|指定的地域ID不存在。|
|400|InvalidInstanceType.ValueNotSupported|The specified InstanceType is not supported.|指定的实例规格未被授权使用。|
|400|ChargeTypeViolation|The operation is not permitted due to charge type of the instance.|付费方式不支持该操作，请您检查实例的付费类型是否与该操作冲突。|
|400|InvalidInstance.PurchaseNotFound|The specified Instance has no purchase.|指定的实例无法购买。|
|400|InvalidInstance.UnPaidOrder|The specified Instance has unpaid order.|指定的实例有未支付的订单，请您先支付再进行操作。|
|400|Account.Arrearage|Your account has been in arrears.|账户余额不足，请先充值再操作。|
|400|InvalidInstanceType.ValueUnauthorized|The specified InstanceType is not Supported.|不支持指定的实例规格。|
|400|OrderCreationFailed|Create Order failed, please check your parameters and try it later.|创建订单失败，请检查您的参数设置后重试。|
|400|Throttling|Request was denied due to request throttling, please try again after 5 minutes.|请求被流控。|
|404|PaymentMethodNotFound|No billing method has been registered on the account.|您还未选择计费方式。|
|404|InvalidRamRole.NotFound|The specified parameter "RAMRoleName" does not exist.|指定的RAM角色不存在。|
|400|InstanceDowngrade.QuotaExceed|Quota of instance downgrade is exceed.|该实例降配已达到最大允许次数。|
|404|InvalidDiskIds.NotFound|Some of the specified data disks do not exist.|指定的数据盘不存在。|
|404|InvalidDiskIds.NotPortable|The specified DiskId is not portable.|指定的磁盘是不可移植的。|
|403|InvalidAccountStatus.NotEnoughBalance|Your account does not have enough balance.|账号余额不足，请您先充值再进行该操作。|
|403|InvalidInstanceChargeType.NotFound|The chargeType of the instance does not support this operation.|实例的计费方式不支持该操作。|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Ecs)

