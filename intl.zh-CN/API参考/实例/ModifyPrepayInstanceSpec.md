# ModifyPrepayInstanceSpec {#doc_api_Ecs_ModifyPrepayInstanceSpec .reference}

升级或者降低预付费（包年包月）实例规格，新实例规格将会覆盖实例的整个生命周期。

## 接口说明 {#description .section}

请确保在使用该接口前，您已充分了解 [云服务器 ECS](https://www.alibabacloud.com/product/ecs#pricing) 的计费方式和产品定价。

调用该接口时，您需要注意：

-   实例必须处于**已停止**（`Stopped`）状态。
-   实例欠费时，无法修改实例规格。
-   升级或者降低[预付费（包年包月）](~~56220~~)实例规格前，您可以通过[DescribeResourcesModification](~~66187~~)查询当前实例支持变配的实例规格。
-   对于降低实例规格：
-   每台实例降低实例规格次数不能超过三次，即价格差退款不会超过三次。
-   降低前后的实例规格价格差退款会退还到您的原付费方式中，已使用的代金券不退回。
-   单台实例每成功操作一次，五分钟内不能继续操作。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=ModifyPrepayInstanceSpec)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|InstanceId|String|是|i-xxxxx1|实例ID。

 |
|InstanceType|String|是|ecs.s1.large|需要变配的目标实例规格。更多详情，请参阅 [实例规格族](~~25378~~)，也可以调用 [DescribeInstanceTypes](~~25620~~) 接口获得最新的规格表。

 |
|RegionId|String|是|cn-hangzhou|实例所属的地域ID。您可以调用 [DescribeRegions](~~25609~~) 查看最新的阿里云地域列表。

 |
|Action|String|否|ModifyPrepayInstanceSpec|接口名称。取值：**ModifyPrepayInstanceSpec**

 |
|AutoPay|Boolean|否|true|是否自动支付。当参数 OperatorType 被置为 downgrade 时，将忽略参数AutoPay。取值范围：

 -   true（默认）：自动支付。您需要确保账户余额充足，如果账户余额不足会生成异常订单，只能作废订单。
-   false：只生成订单不扣费。更换计费方式后，默认自动扣费。您需要确保账户余额充足，否则会生成异常订单，此时只能作废订单。如果您的账户余额不足，可以将参数 **AutoPay** 置为 **false**，此时会生成正常的未支付订单，您可以登录 ECS管理控制台 支付。

 |
|MigrateAcrossZone|Boolean|否|false|是否支持跨集群升级实例规格。默认值：False

 当参数 MigrateAcrossZone 取值为 True 时，一旦您根据返回信息升级了云服务器，请留意以下注意事项：

 经典网络类型实例：

 -   对于 [已停售的实例规格](~~55263~~)，非I/O优化实例变配到I/O优化实例时，实例私网IP地址、磁盘设备名和软件授权码会发生变化。对于Linux实例，普通云盘（cloud）会被识别为 xvda 或者 xvdb 等，高效云盘（cloud\_efficiency）和SSD云盘（cloud\_ssd）会被识别为 vda 或者 vdb 等。
-   对于 [正常售卖的实例规格族](~~25378~~)，实例的私网 IP 地址会发生变化。

 专有网络VPC类型实例：对于已停售的实例规格\]，非 I/O 优化实例变配到 I/O 优化实例时，云服务器磁盘设备名和软件授权码会发生变化。Linux 实例的普通云盘（cloud）会被识别为 xvda 或者 xvdb 等，高效云盘（cloud\_efficiency） 和SSD云盘（cloud\_ssd）会被识别为 vda 或者 vdb 等。

 |
|OperatorType|String|否|upgrade|操作类型。取值范围：

 -   upgrade（默认）：升级实例规格。当参数`OperatorType`被置为`upgrade`时，请确保您的账户支付方式余额充足。
-   downgrade：降配实例规格。

 |
|SystemDisk.Category|String|否|cloud\_efficiency|更换系统盘类型。该参数只有在从 [已停售的实例规格](~~55263~~) 升级到 [正常售卖的实例规格族](~~25378~~)，并将非 I/O 优化实例规格升级为 I/O 优化实例规格时有效。取值范围：

 -   cloud\_efficiency：高效云盘
-   cloud\_ssd：SSD云盘

 |
|ClientToken|String|否|123e4567-e89b-12d3-a456-426655440000|保证请求幂等性。从您的客户端生成一个参数值，确保不同请求间该参数值唯一。**ClientToken** 只支持 ASCII 字符，且不能超过 64 个字符。更多详情，请参阅 [如何保证幂等性](~~25693~~)。

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

https://ecs.aliyuncs.com/?Action=ModifyPrepayInstanceSpec
&RegionId=cn-hangzhou
&InstanceId=i-xxxxx1
&InstanceType=ecs.s1.large
&AutoPay=true
&OperatorType=upgrade
&ClientToken=xxxxxxxxxxxxxx
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ModifyPrepayInstanceSpecResponse>
  <RequestId>04F0F334-1335-436C-A1D7-6C044FE73368</RequestId>
  <OrderId>1011111111111111</OrderId>
</ModifyPrepayInstanceSpecResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"OrderId":1011111111111111,
	"RequestId":"04F0F334-1335-436C-A1D7-6C044FE73368"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|404|InvalidRegionId.NotFound|The specified RegionId does not exist.|指定的 RegionId 不存在，请您检查此产品在该地域是否可用。|
|400|InvalidInstanceType.ValueUnauthorized|The specified InstanceType is not authorized.|指定的实例规格未授权使用。|
|400|InvalidInstanceType.ValueNotSupported|The specified InstanceType does not exist or beyond the permitted range.|指定的实例规格不支持。|
|500|InternalError|The request processing has failed due to some unknown error, exception or failure.|发生未知错误。|
|404|BillingMethodNotFound|The account has not chosen any billing method.|该帐户没有选择任何计费方法。|
|403|OperationDenied.NoStock|The specified instance is out of usage.|库存不足。|
|400|InvalidBillingMethod.ValueNotSupported|The operation is not permitted due to an invalid billing method of the instance.|由于实例的计费方式无效，该操作不允许。|
|400|InvalidInstanceId.Released|The specified instance has been released.|该实例已经被释放。|
|400|InvalidInstance.PurchaseNotFound|The specified instance has no purchase history.|该实例的订购记录不存在。|
|400|InvalidInstanceType.NotSupported|The specified InstanceType is not Supported.|不支持指定的 InstanceType。|
|400|OrderCreationFailed|Order creation failed, please check your params and try it again later.|订单创建失败，请核查参数并重试。|
|400|Throttling|You have made too many requests within a short time; your request is denied due to request throttling.|请求被流控。|
|400|Account.Arrearage|Your account has an outstanding payment.|账号存在未支付款项。|
|403|InvalidUser.PassRoleForbidden|The RAM user does not have privilege to pass a role.|RAM子账号不具备授予ECS RAM角色的权利。|
|400|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|指定的实例不存在，请您检查实例ID是否正确。|
|400|InvalidRebootTime.MalFormed|The specified rebootTime is not valid.|指定的 RebootTime 不合法。|
|400|InvalidRebootTime.ValueNotSupported|The specified RebootTime is not valid.|指定的重启时间不合法。|
|403|ImageNotSupportInstanceType|The specified image does not support the specified InstanceType.|指定的镜像不支持改实例规格。|
|403|InstanceType.Offline|%s|实例规格不能使用。|
|400|IdempotenceParamNotMatch|Request uses a client token in a previous request but is not identical to that request.|与相同 ClientToken 的请求参数不符合。|
|403|IncorrectInstanceStatus|The current status of the resource does not support this operation.|该资源目前的状态不支持此操作。|
|400|IdempotenceParamNotMatch|%s|幂等签名不一致。|
|400|InvalidInstanceChargeType.ValueNotSupported|%s|该计费方式取值不存在。|
|400|InvalidStatus.NotStopped|Instance status must be stopped.|实例状态必须被停止。|
|400|InvalidAction|%s|操作不合法。|
|400|InstanceDowngrade.QuotaExceed|Quota of instance downgrade is exceed.|该实例降配已达到最大允许次数。|
|400|InvalidInstanceType.ValueNotSupported|%s|实例类型属性不正确。|
|403|InvalidParameter.InstanceId|%s|InstanceId参数无效。|
|400|InvalidParameter|%s|参数格式不正确。|
|403|ImageNotSupportInstanceType|The specified instanceType is not supported by instance with marketplace image.|指定的市场镜像不支持该实例规格。|
|403|InvalidInstanceStatus|The current status of the instance does not support this operation.|实例当前状态不支持该操作。|
|403|InvalidInstance.PreInstanceExpired|Instance business status is not Expired|实例的状态不正确。|
|403|InvalidInstance.EipNotSupport|The special instance with eip not support operate, please unassociate eip first.|本实例已绑定EIP不支持该操作，请优先解绑EIP。|
|403|InvalidOperation.Ipv4CountExceeded|%s|IPv4 个数达到上限。|
|403|InvalidOperation.Ipv6CountExceeded|%s|IPv6 个数达到上限。|
|403|InvalidOperation.Ipv6NotSupport|%s|实例规格不支持 IPv6。|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Ecs)

