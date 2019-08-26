# ModifyPrepayInstanceSpec {#ModifyPrepayInstanceSpec .reference}

升级或者降低预付费（包年包月）实例规格，新实例规格将会覆盖实例的整个生命周期。

## 描述 {#section_pvl_dj5_xdb .section}

调用该接口时，您需要注意：

-   实例必须处于**已停止**（`Stopped`）状态。

-   实例欠费时，无法修改实例规格。

-   升级或者降低[预付费（包年包月）](../cn.zh-CN/产品定价/包年包月.md#)实例规格前，您可以通过[DescribeResourcesModification](cn.zh-CN/API 参考/地域/DescribeResourcesModification.md#)查询当前实例支持变配的实例规格。

    更多详情，请参阅*云栖社区*[查询ECS变配的可用资源实践](https://yq.aliyun.com/articles/500164)。

-   对于降低实例规格：

-   每台实例降低实例规格次数不能超过三次，即价格差退款不会超过三次。
-   降低前后的实例规格价格差退款会退还到您的原付费方式中，已使用的代金券不退回。
-   单台实例每成功操作一次，五分钟内不能继续操作。


## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：ModifyPrepayInstanceSpec|
|InstanceId|String|是|实例ID。|
|RegionId|String|是|实例所属的地域ID。您可以调用[DescribeRegions](../cn.zh-CN/API 参考/地域/DescribeRegions.md#)查看最新的阿里云地域列表。|
|InstanceType|String|是|需要变配的目标实例规格。更多详情，请参阅[实例规格族](../cn.zh-CN/产品简介/实例规格族.md#)，也可以调用[DescribeInstanceTypes](cn.zh-CN/API 参考/实例/DescribeInstanceTypes.md#)接口获得最新的规格表。|
|OperatorType|String|否|操作类型。取值范围：-   upgrade：升级实例规格
-   downgrade：降配实例规格

默认值：upgrade

当参数`OperatorType`被置为`upgrade`时，请确保您的账户余额充足。

|
|AutoPay|Boolean|否|是否自动支付。取值范围：-   true：自动支付。您需要确保账户余额充足，如果账户余额不足会生成异常订单，只能作废订单。
-   false：只生成订单不扣费。更换计费方式后，默认自动扣费。您需要确保账户余额充足，否则会生成异常订单，此时只能作废订单。如果您的账户余额不足，可以将参数`AutoPay`置为`false`，此时会生成正常的未支付订单，您可以登录[ECS管理控制台](https://ecs.console.aliyun.com/)支付。

默认值：true当参数`OperatorType`被置为`downgrade`时，将忽略参数`AutoPay`。

|
|SystemDisk.Category|String|否|更换系统盘类型。该参数只有在从[已停售的实例规格](https://help.aliyun.com/document_detail/55263.html)升级到 [正常售卖的实例规格族](../cn.zh-CN/产品简介/实例规格族.md#)，并将非I/O优化实例规格升级为I/O优化实例规格时有效。取值范围：-   cloud\_efficiency：高效云盘
-   cloud\_ssd：SSD云盘

|
|MigrateAcrossZone|Boolean|否|是否支持跨集群升级实例规格。默认值：False

当参数`MigrateAcrossZone`取值为`True`时，一旦您根据返回信息升级了云服务器，请留意以下注意事项：

-   经典网络类型实例：
    -   对于[已停售的实例规格](https://help.aliyun.com/document_detail/55263.html)，非I/O优化实例变配到I/O优化实例时，实例私网IP地址、磁盘设备名和软件授权码会发生变化。对于Linux实例，普通云盘（`cloud`）会被识别为`xvda`或者`xvdb`等，高效云盘（`cloud_efficiency`）和SSD云盘（`cloud_ssd`）会被识别为`vda`或者`vdb`等。
    -   对于[正常售卖的实例规格族](../cn.zh-CN/产品简介/实例规格族.md#)，实例的私网IP地址会发生变化。
-   专有网络VPC类型实例：

对于[已停售的实例规格](https://help.aliyun.com/document_detail/55263.html)，非I/O优化实例变配到I/O优化实例时，云服务器磁盘设备名和软件授权码会发生变化。Linux 实例的普通云盘（`cloud`）会被识别为`xvda`或者`xvdb`等，高效云盘（`cloud_efficiency`） 和SSD云盘（`cloud_ssd`）会被识别为`vda`或者`vdb`等。


|
|ClientToken|String|否| 保证请求幂等性。从您的客户端生成一个参数值，确保不同请求间该参数值唯一。只支持ASCII字符，且不能超过64个字符。更多详情，请参阅[如何保证幂等性](../cn.zh-CN/API 参考/附录/如何保证幂等性.md#)。

 |

## 返回参数 {#ResponseParameter .section}

|名称|类型|描述|
|:-|:-|:-|
|OrderId|Long|生成的订单ID|

## 示例 { .section}

**请求示例**

```
https://ecs.aliyuncs.com/?Action=ModifyPrepayInstanceSpec
&RegionId=cn-hangzhou
&InstanceId=i-xxxxx1
&InstanceType=ecs.s1.large
&AutoPay=true
&OperatorType=upgrade
&ClientToken=xxxxxxxxxxxxxx
&<公共请求参数>
```

**返回示例**

**XML格式**

```
<ModifyInstanceConfiguration>
    <RequestId>04F0F334-1335-436C-A1D7-6C044FE73368</RequestId>
    <OrderId>1011111111111111</OrderId>
</ModifyInstanceConfiguration>
```

**JSON格式**

```
{
    "RequestId": "04F0F334-1335-436C-A1D7-6C044FE73368",
    "OrderId": 1011111111111111,
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问[API错误中心](https://error-center.aliyun.com/status/product/Ecs)。

|错误代码|错误信息|HTTP状态码|说明|
|:---|:---|:------|:-|
|Account.Arrearage|Your account has an outstanding payment.|400|账户已经欠费。|
|IdempotenceParamNotMatch|Request uses a client token in a previous request but is not identical to that request.|400|与相同`ClientToken`的请求参数不符合。|
|InvalidBillingMethod.ValueNotSupported|The operation is not permitted due to an invalid billing method of the instance.|400|实例付费类型不合法。|
|InvalidClientToken.ValueNotSupported|The ClientToken provided is invalid.|400|`ClientToken`参数值不合法，不能包含ASCII以外的字符。|
|InvalidInstance.UnpaidOrder|The specified Instance has unpaid order.|400|当前实例有未支付的订单。|
|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|400|指定的实例ID不存在。|
|InvalidInstanceId.Released|The specified Instance has been released.|400|指定实例已被释放。|
|InvalidInstanceType.ValueNotSupported|The specified InstanceType is not supported.|400|指定的`InstanceType`不合法（超出可选范围）。|
|InvalidInstanceType.ValueUnauthorized|The specified InstanceType is not authorized.|400|指定的`InstanceType`未授权使用。|
|MissingParameter.InstanceIdNotSupported|The InstanceId should not be null.|400|`InstanceId`不能为空。|
|MissingParameter.RegionId|The RegionId should not be null.|400|`RegionId`不能为空。|
|OrderCreationFailed|Order creation failed, please check your params and try it again later.|400|创建订单失败。|
|Throttling|You have made too many requests within a short time; your request is denied due to request throttling.|400|操作过于频繁。|
|ImageNotSupportInstanceType|The specified image does not support the specified InstanceType.|403|指定镜像不支持该实例类型。|
|InvalidAccountStatus.NotEnoughBalance|Your account does not have enough balance.|403|账户余额不足。|
|InvalidBillingMethod|The specified billing method is invalid.|403|指定的付费类型不存在。|
|InvalidUser.PassRoleForbidden|The RAM user does not have privilege to pass a role.|403|您使用的RAM用户账号暂不具有`PassRole`的权限，请联系主账号拥有者[授权](../cn.zh-CN/快速入门/为 RAM 用户授权.md#)PassRole权限。|
|BillingMethodNotFound|The account has not chosen any billing method.|404|该账户没有选择付款方式。|
|InvalidRegionId.NotFound|The specified RegionId does not exist.|404|指定的`RegionId`不存在。|
|InternalError|The request processing has failed due to some unknown error, exception or failure.|500|内部错误。|

