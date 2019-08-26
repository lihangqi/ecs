# ModifyInstanceChargeType {#doc_api_Ecs_ModifyInstanceChargeType .reference}

更换一台或者多台实例的计费方式。支持在按量付费实例和预付费（包年包月）实例间相互转换，同时可以将实例挂载的所有按量付费云盘转换为预付费（包年包月）云盘。

## 接口说明 {#description .section}

请确保在使用该接口前，您已充分了解 [云服务器 ECS](https://www.alibabacloud.com/product/ecs#pricing) 的计费方式和产品定价。

调用该接口时，您需要注意：

-   目标实例的状态必须为 **运行中**（`Running`）或者 **已停止**（`Stopped`），并且无欠费的情况下才能修改计费方式。
-   更换计费方式后，默认自动扣费。您需要确保账户余额充足，否则会生成异常订单，此时只能作废订单。如果您的账户余额不足，可以将参数`AutoPay`置为`false`，此时会生成正常的未支付订单，您可以登录 [ECS 管理控制台](https://ecs.console.aliyun.com/)支付。
-   **预付费转按量付费**：
    -   达到一定信用等级的阿里云用户可以使用预付费转按量付费功能。
    -   包年包月实例转按量实例的时候，新计费方式将覆盖实例的整个生命周期。您会收到修改前后的实例计费的价格差退款，退还到您的原付款渠道中，已使用的代金券将不退回。
    -   **退款规则**：您在一个月内能自由操作的退款额度有限且不累计，消耗完退款额度后，只能等待次月转换计费方式。一次转换计费消耗的退款额度公式为 **vCPU数\*\(退款天数\*24±浮动小时数\)**。
-   **按量付费转预付费**：
    -   支持将实例挂载的所有按量付费数据盘同时转换为包年包月数据盘。
    -   如果按量付费实例已经设置了释放时间，则不能调用该接口。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=ModifyInstanceChargeType)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|InstanceIds|String|是|\["i-xxxxx1","i-xxxxx2"\]|实例 ID。取值可以由多台实例 ID 组成一个 JSON 数组，最多支持 20 个 ID，ID 之间用半角逗号（`,`）隔开。

 |
|RegionId|String|是|cn-hangzhou|实例所属的地域ID。您可以调用 [DescribeRegions](~~25609~~) 查看最新的阿里云地域列表。

 |
|Action|String|否|ModifyInstanceChargeType|接口名称。取值：**ModifyInstanceChargeType**

 |
|AutoPay|Boolean|否|false|是否自动支付。当参数OperatorType被置为downgrade时，将忽略参数AutoPay。取值范围：

 -   true（默认）：自动支付。您需要确保账户余额充足，如果账户余额不足会生成异常订单，只能作废订单。
-   false：只生成订单不扣费。更换计费方式后，默认自动扣费。您需要确保账户余额充足，否则会生成异常订单，此时只能作废订单。如果您的账户余额不足，可以将参数 **AutoPay** 置为 **false**，此时会生成正常的未支付订单，您可以登录 ECS 管理控制台支付。

 |
|DryRun|Boolean|否|false|是否只预检此次请求。

 -   true：发送检查请求，不会查询资源状况。检查项包括 AccessKey 是否有效、RAM 用户的授权情况和是否填写了必需参数。如果检查不通过，则返回对应错误。如果检查通过，会返回错误码 `DryRunOperation`。
-   false（默认）：发送正常请求，通过检查后返回 2XX HTTP 状态码并直接查询资源状况。

 |
|IncludeDataDisks|Boolean|否|true|是否将实例挂载的所有按量付费数据盘一起转换为包年包月数据盘。默认值：true

 |
|InstanceChargeType|String|否|PrePaid|实例需要修改的目标计费方式。取值范围：

 -   PrePaid（默认）：预付费（包年包月），即按量付费实例转换为包年包月实例。
-   PostPaid：按量付费，即包年包月实例转换为按量付费实例。

 |
|OwnerAccount|String|否|EcsforCloud@Alibaba.com|RAM用户的账号登录名称。

 |
|Period|Integer|否|2|预付费续费时长。一旦指定了 DedicatedHostId，则取值范围不能超过专有宿主机的订阅时长。取值范围：

 -   `PeriodUnit=Month` 时，`Period` 取值：\{ “1”, “2”, “3”, “4”, “5”, “6”, “7”, “8”, “9”, “12”, “24”, “36”,”48”,”60”\}

 |
|PeriodUnit|String|否|month|续费时长的时间单位，即参数 `Period` 的单位。取值范围：

 -   Month（默认）

 |
|ClientToken|String|否|155780923770 084 104 105 115 073 115 084 104 101 070 105 114 115 116 082 101 113 117 101 115 116|保证请求幂等性。从您的客户端生成一个参数值，确保不同请求间该参数值唯一。**ClientToken** 只支持 ASCII 字符，且不能超过 64 个字符。更多详情，请参阅 [如何保证幂等性](~~25693~~)。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|OrderId|String|10111111111xxxxx|生成的订单 ID。

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

https://ecs.aliyuncs.com/?Action=ModifyInstanceChargeType
&RegionId=cn-hangzhou
&InstanceIds=["i-xxxxx1","i-xxxxx2"]
&Period=1
&PeriodUnit=Month
&AutoPay=false
&IncludeAllDisks=true
&ClientToken=xxxxxxxxxxxxxx
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ModifyInstanceChargeTypeResponse>
  <RequestId>04F0F334-1335-436C-A1D7-6C044FExxxxx</RequestId>
  <OrderId>10111111111xxxxx</OrderId>
</ModifyInstanceChargeTypeResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"OrderId":"10111111111xxxxx",
	"RequestId":"04F0F334-1335-436C-A1D7-6C044FExxxxx"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InvalidParameter.InstanceIds|The specified InstanceIds are invalid.|指定的实例无效。|
|400|InvalidParameter|%s|参数格式不正确。|
|400|InvalidStatus.ValueNotSupported|%s|该资源当前的状态不支持该操作。|
|400|InvalidInstanceChargeType.ValueNotSupported|%s|该计费方式取值不存在。|
|400|ExpiredInstance|The specified instance has expired.|指定的实例已过期。|
|403|InvalidInstance.TempBandwidthUpgrade|Cannot switch to Pay-As-You-Go during the period of temporary bandwidth upgrade.|临时带宽升级期间不能转换为按量付费。|
|400|InstancesIdQuotaExceed|The maximum number of Instances is exceeded.|超过了实例数的上限。|
|400|InvalidClientToken.ValueNotSupported|The ClientToken provided is invalid.|指定的 ClientToken 不合法。|
|400|InvalidInternetChargeType.ValueNotSupported|%s|参数不支持。|
|403|InvalidInstanceType.ValueNotSupported|The specified InstanceType does not exist or beyond the permitted range.|指定的实例规格不支持。|
|403|InstanceType.Offline|%s|实例规格不能使用。|
|500|InternalError|The request processing has failed due to some unknown error, exception or failure.|发生未知错误。|
|400|ReleaseTimeHaveBeenSet|The specified instance has been set released time.|指定的实例已设置释放时间。|
|403|InvalidAccountStatus.NotEnoughBalance|Your account does not have enough balance.|账号余额不足，请您先充值再进行该操作。|
|403|Account.Arrearage|Your account has an outstanding payment.|账号存在未支付款项。|
|400|Throttling|Request was denied due to request throttling, please try again after 5 minutes.|请求被流控。|
|403|InvalidParameter.NotMatch|%s|参数冲突。|
|403|InvalidAction|%s|操作不合法。|
|400|Throttling|%s|请求被流控。|
|400|QuotaExceed.AfterpayInstance|The maximum number of Pay-As-You-Go instances is exceeded: %s|已经达到允许创建按量实例数量的最大值。|
|400|InvalidParameter.Bandwidth|%s|参数不支持。|
|400|InvalidPeriod.UnitMismatch|The specified Period must be correlated with the PeriodUnit.|指定的时长必须得。|
|400|InvalidImageType.NotSupported|%s|指定的镜像类型无效。|
|400|InvalidPeriod.ExceededDedicatedHost|Instance expired date can't exceed dedicated host expired date.|实例的自动订阅时长不能晚于专有宿主机订阅时长。|
|400|InvalidMarketImageChargeType.NotSupport|The specified chargeType of marketImage is unsupported.|云市场镜像的计费方式无效。|
|403|QuotaExceed.PostPaidDisk|Living postPaid disks quota exceeded.|按量付费磁盘数量已超出允许数量。|
|403|ImageNotSupportInstanceType|The specified instanceType is not supported by instance with marketplace image.|指定的市场镜像不支持该实例规格。|
|403|InvalidInstanceType.PhasedOut|This instanceType is no longer offered.|该实例规格已下线。|
|400|InvalidSystemDiskCategory.ValueNotSupported|%s|参数不支持。|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Ecs)

