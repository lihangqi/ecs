# RenewInstance {#doc_api_Ecs_RenewInstance .reference}

调用RenewInstance续费一台预付费ECS实例。

## 接口说明 {#description .section}

请确保在使用该接口前，您已充分了解[云服务器ECS](https://www.aliyun.com/price/product#/ecs/detail)的计费方式和产品定价。

调用该接口时，您需要注意：

-   仅支持续费预付费ECS实例。
-   除折扣账号之外，支付续费产生的账单时，默认优先使用您的账号下的代金券。
-   您的账号必须支持账号余额支付或信用支付。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=RenewInstance&type=RPC&version=2014-05-26)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|InstanceId|String|是|i-instance1|需要续费的实例ID。

 |
|Period|Integer|是|1|预付费续费时长。一旦指定了DedicatedHostId，则取值范围不能超过专有宿主机的订阅时长。取值范围：

 -   PeriodUnit=Week时，Period取值：1~4
-   PeriodUnit=Month时，Period取值：1~12, 24, 36, 48, 60

 |
|Action|String|否|RenewInstance|接口名称，取值：**RenewInstance**

 |
|OwnerAccount|String|否|happyCustomer|RAM用户的账号登录名称。

 |
|PeriodUnit|String|否|Month|续费时长的时间单位，即参数Period的单位。取值范围：

 -   Week
-   Month（默认）

 |
|ClientToken|String|否|0c593ea1-3bea-11e9-b96b-88e9fe637760|保证请求幂等性。从您的客户端生成一个参数值，确保不同请求间该参数值唯一。**ClientToken**只支持ASCII字符，且不能超过64个字符。更多详情，请参见[如何保证幂等性](~~25693~~)。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=RenewInstance
&InstanceId=i-instance1
&Period=1
&PeriodUnit=Month
&ClientToken=0c593ea1-3bea-11e9-b96b-88e9fe637760
&<公共请求参数>
```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ModifyInstanceSpecResponse>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</ModifyInstanceSpecResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InvalidInternetChargeType.ValueNotSupported|The specified InternetChargeType is not valid.|指定的实例升降配规格不存在。|
|400|InvalidInstanceType.NotSupported|The specified InstanceType is not Supported.|不支持指定的 InstanceType。|
|400|InvalidParameter|The specified parameter "InternetMaxBandwidthOut" is not valid.|指定的 InternetMaxBandwidthOut 参数不合法。|
|400|InvalidInstanceChargeType.NotFound|The InstanceChargeType does not exist in our records.|指定的实例计费方式不存在。|
|400|InvalidRebootTime.ValueNotSupported|The specified RebootTime is out of the permitted range.|指定的重启时间超出取值范围。|
|400|IdempotenceParamNotMatch|Request uses a client token in a previous request but is not identical to that request.|与相同 ClientToken 的请求参数不符合。|
|400|InvalidClientToken.ValueNotSupported|The ClientToken provided is invalid.|指定的 ClientToken 不合法。|
|403|ChargeTypeViolation|The operation is not permitted due to charge type of the instance.|付费方式不支持该操作，请您检查实例的付费类型是否与该操作冲突。|
|400|InvalidInstanceType.ValueNotSupported|The specified InstanceType does not exist or beyond the permitted range.|指定的实例规格不支持。|
|404|InvalidDiskId.NotFound|The specified disk does not exist.|指定的磁盘不存在。请您检查磁盘 ID 是否正确。|
|403|Diskcategory.Mismatch|The disk specified to convert to portable is not allowed due to the disk category does not support.|由于磁盘种类限制，指定的磁盘不能转换为可卸载磁盘。|
|404|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|指定的实例不存在，请您检查实例ID是否正确。|
|403|IncorrectInstanceStatus|The current status of the resource does not support this operation.|该资源目前的状态不支持此操作。|
|400|InvalidInstanceType.codeUnauthorized|The specified InstanceType is not authorized.|指定的 InstanceType 不合法。|
|400|InvalidInternetChargeType.InstanceNotSupported|The specified instance which is in vpc is not support the parameter InternetChargeType.|指定的 VPC 网络实例不支持指定的网络计费方式。|
|400|InvalidPeriod|The specified period is not valid.|指定的时段不合法。|
|403|InstanceSpecModification.NotEffective|The specified instance has been reserved for making a spec modification and not taken effective in the current contract period.|指定的实例因规格调整被保留，在当前合同期内无法生效。|
|400|Upgrade.NotSupported|Upgrade operation is not supported.|升级操作不合法。|
|403|LastTokenProcessing|The last token request is processing.|正在处理上一条令牌请求，请您稍后再试。|
|403|Instance.UnPaidOrder|The specified instance has unpaid order.|该实例有未完成的账单。|
|400|OperationDenied|Specified instance is in VPC.|指定实例存在于 VPC。|
|400|InvalidInstanceType.ValueUnauthorized|The specified InstanceType is not authorized.|指定的实例规格未授权使用。|
|400|InvalidParameter|The specified parameter " InternetMaxBandwidthOut " is not valid.|InternetMaxBandwidthOut参数设置无效。|
|403|InstanceLockedForSecurity|The specified operation is denied as your instance is locked for security reasons.|实例被安全锁定，指定的操作无法完成。|
|403|InvalidDisk.NotAllowed|The specified disk is not allowed to be converted to portable.|指定的磁盘不允许转换为可卸载磁盘。|
|400|DependencyViolation.InstanceType|Current instancetype cannot be changed to the specified one.|当前实例规格不能更改为指定规格。|
|403|InstanceTypeNotSupported|The specified zone does not offer the specified instancetype.|指定的可用区不支持指定的实例规格。|
|400|InvalidPeriodUnit.ValueNotSupported|The specified parameter PeriodUnit is not valid.|市场单位不支持。|
|400|InvalidDedicatedHostId.NotFound|The specified DedicatedHostId does not exist.|指定的专有宿主机ID不存在。|
|400|InvalidDedicatedHostStatus.NotSupport|Operation denied due to dedicated host status.|资源状态不支持操作。|
|400|IncorrectDedicatedHostStatus|The current status of the resource does not support this operation.|资源状态不支持操作。|
|400|InvalidPeriod.ExceededDedicatedHost|Instance expired date can't exceed dedicated host expired date.|实例的自动订阅时长不能晚于专有宿主机订阅时长。|
|400|InvalidStatus.Upgrading|The instance is upgrading; please try again later.|实例正在升级，请稍后重试。|
|400|InvalidPeriod.ExceededMaximumExpirationDate|The specified renewal period cannot exceed the maximum expiration date. We recommend you try shortening the renewal period at next attempt.|续费时长。|
|500|InternalError|The request processing has failed due to some unknown error.|内部错误，请重试。如果多次尝试失败，请提交工单|
|400|LastOrderProcessing|The previous order is still processing, please try again later.|订单正在处理中，稍后重试。|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

