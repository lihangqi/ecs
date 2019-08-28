# ModifyDiskChargeType {#doc_api_Ecs_ModifyDiskChargeType .reference}

调用ModifyDiskChargeType修改一台实例上挂载的一块或最多16块云盘的计费方式。

## 接口说明 {#description .section}

更换计费方式后，默认自动扣费。您需要确保账户余额充足，否则会生成异常订单，此时只能作废订单。如果您的账户余额不足，可以将参数 AutoPay 置为 false，此时会生成正常的未支付订单，您可以登录 [ECS 管理控制台](https://ecs.console.aliyun.com/)支付。

使用该接口时，请注意：

-   包年包月云盘转换为按量付费云盘时，适用于包年包月实例上挂载的包年包月云盘。
-   按量付费云盘转换为包年包月云盘时，适用于包年包月实例上挂载的按量付费数据盘，或者按量付费实例上挂载的按量付费数据盘。
-   挂载的实例不能为欠费停机状态。
-   每块云盘更换计费方式的次数不能超过三次，即价格差退款不会超过三次。
-   更换计费方式前后的价格差退款会退还到您的原付费方式中，已使用的代金券不退回。
-   每块云盘成功修改计费方式一次，五分钟内不能再次修改。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=ModifyDiskChargeType&type=RPC&version=2014-05-26)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|DiskIds|String|是|\[“d-xxxxxxxxx”, “d-yyyyyyyyy”, … “d-zzzzzzzzz”\]|云盘ID列表，一个带有格式的Json Array，最多支持16个ID，用半角逗号（,）隔开。

 |
|InstanceId|String|是|i-instanceid1|云盘挂载的实例ID。

 |
|RegionId|String|是|cn-hangzhou|实例所属的地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。

 |
|Action|String|否|ModifyDiskChargeType|系统规定参数。取值： ModifyDiskChargeType

 |
|AutoPay|Boolean|否|true|是否自动支付。取值范围：

 -   true（默认）：自动支付。您需要确保账户余额充足，如果账户余额不足会生成异常订单，只能作废订单。
-   false：只生成订单不扣费。如果您的账户余额不足，会生成正常的未支付订单，此订单可登录 ECS 控制台支付。

 |
|ClientToken|String|否|123e4567-e89b-12d3-a456-426655440000|保证请求幂等性。从您的客户端生成一个参数值，确保不同请求间该参数值唯一。**ClientToken**只支持ASCII字符，且不能超过64个字符。更多详情，请参见[如何保证幂等性](~~25693~~)。

 |
|DiskChargeType|String|否|PostPaid|云盘计费方式。取值范围：

 -   PrePaid（默认）：按量付费数据盘转换为包年包月数据盘。
-   PostPaid：包年包月数据盘转换为按量付费数据盘。

 |

## 返回数据 {#resultMapping .section}

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
|400|InvalidInstanceType.ValueUnauthorized|The specified InstanceType is not authorized.|指定的实例规格未授权使用。|
|400|InvalidInstanceType.ValueNotSupported|The specified InstanceType is not supported.|指定的实例规格未被授权使用。|
|400|MissingParameter.RegionId|RegionId should not be null.|参数RegionId不得为空。|
|400|MissingParameter.InstanceIdNotSupported|InstanceId should not be null.|参数 InstanceId 不能为空。|
|400|ChargeTypeViolation|The operation is not permitted due to charge type of the instance.|付费方式不支持该操作，请您检查实例的付费类型是否与该操作冲突。|
|400|InvalidInstanceId.Released|The specified Instance is not exist.|指定的实例不存在，请您检查实例 ID 是否正确。|
|400|InvalidInstance.PurchaseNotFound|The specified Instance has no purchase.|指定的实例无法购买。|
|400|InvalidInstance.UnPaidOrder|The specified Instance has unpaid order.|指定的实例有未支付的订单，请您先支付再进行操作。|
|400|InvalidClientToken.ValueNotSupported|The ClientToken provided is invalid.|指定的 ClientToken 不合法。|
|400|Account.Arrearage|Your account has been in arrears.|账户余额不足，请先充值再操作。|
|400|Idempotence.SignatureMismatch|There is a idempotence signature mismatch between this and last request.|作为和上一个幂等参数相同的请求，其他参数也必须完全相匹配。|
|400|InvalidInstanceType.ValueUnauthorized|The specified InstanceType is not Supported.|不支持指定的实例规格。|
|400|OrderCreationFailed|Create Order failed, please check your parameters and try it later.|创建订单失败，请检查您的参数设置后重试。|
|400|Throttling|Request was denied due to request throttling, please try again after 5 minutes.|请求被流控。|
|403|Forbidden|%s|您未被授权使用指定的资源。|
|404|PaymentMethodNotFound|No billing method has been registered on the account.|您还未选择计费方式。|
|404|InvalidRamRole.NotFound|The specified parameter "RAMRoleName" does not exist.|指定的RAM角色不存在。|
|400|InstanceDowngrade.QuotaExceed|Quota of instance downgrade is exceed.|该实例降配已达到最大允许次数。|
|404|InvalidDiskIds.NotFound|Some of the specified data disks do not exist.|指定的数据盘不存在。|
|404|InvalidDiskIds.NotPortable|The specified DiskId is not portable.|指定的磁盘是不可移植的。|
|500|InternalError|The request processing has failed due to some unknown error.|内部错误，请重试。如果多次尝试失败，请提交工单。|
|403|InvalidAccountStatus.NotEnoughBalance|Your account does not have enough balance.|账号余额不足，请您先充值再进行该操作。|
|403|InvalidInstanceChargeType.NotFound|The chargeType of the instance does not support this operation.|实例的计费方式不支持该操作。|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

