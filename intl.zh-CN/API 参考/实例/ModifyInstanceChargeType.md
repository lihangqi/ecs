# ModifyInstanceChargeType {#ModifyInstanceChargeType .reference}

更换一台或者多台实例的计费方式。支持在按量付费实例和预付费（包年包月）实例间相互转换，同时可以将实例挂载的所有按量付费云盘转换为预付费（包年包月）云盘。

## 描述 {#Description .section}

调用该接口时，您需要注意：

-   目标实例的状态必须为**运行中**（`Running`）或者**已停止**（`Stopped`），并且无欠费的情况下才能修改计费方式。

-   更换计费方式后，默认自动扣费。您需要确保账户余额充足，否则会生成异常订单，此时只能作废订单。如果您的账户余额不足，可以将参数`AutoPay`置为`false`，此时会生成正常的未支付订单，您可以登录[ECS管理控制台](https://ecs.console.aliyun.com/)支付。

**预付费转按量付费**

-   达到一定信用等级的阿里云用户可以使用预付费转按量付费功能。

-   包年包月实例转按量实例的时候，新计费方式将覆盖实例的整个生命周期，您会收到修改前后的实例计费的价格差退款，退还到您的原付款渠道中，已使用的代金券将不退回。

-   **退款规则**：您在一个月内能自由操作的退款额度有限且不累计，消耗完退款额度后，只能等待次月转换计费方式。一次转换计费消耗的退款额度公式为**vCPU数\*\(退款天数\*24±浮动小时数\)**。下图以计算网络增强型实例规格ecs.sn1ne.xlarge（4vCPU）为例，讲述消耗退款额度的规则：

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9878/154157763412954_zh-CN.png)


**按量付费转预付费**

-   支持将实例挂载的所有按量付费数据盘同时转换为包年包月数据盘。

-   如果按量付费实例已经设置了释放时间，则不能调用该接口。


## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：ModifyInstanceChargeType|
|RegionId|String|是|实例所属的地域ID。您可以调用[DescribeRegions](../intl.zh-CN/API 参考/地域/DescribeRegions.md#)查看最新的阿里云地域列表。|
|InstanceIds|String|是|实例ID。取值可以由多台实例ID组成一个JSON数组，格式为\["s-xxxxxxxxx", "s-yyyyyyyyy", … "s-zzzzzzzzz"\]，最多支持20个ID，ID之间用半角逗号（`,`）隔开。|
|Period|Integer|否|购买实例的时长。|
|PeriodUnit|String|否|时长周期单位。取值范围：Year | Month | Week | Day目前只支持`Year`、`Week`和`Month`。

|
|IncludeDataDisks|Boolean|否|是否将实例挂载的所有按量付费数据盘一起转换为包年包月数据盘。默认值：true|
|InstanceChargeType|String|否|实例需要修改的目标计费方式。取值范围：-   PrePaid（默认）：预付费（包年包月），即按量付费实例转换为包年包月实例。
-   PostPaid：按量付费，即包年包月实例转换为按量付费实例。

|
|AutoPay|Boolean|否|是否自动支付。取值范围：-   true（默认）：自动支付。您需要确保账户余额充足，如果账户余额不足会生成异常订单，只能作废订单。
-   false：只生成订单不扣费。如果您的账户余额不足，会生成正常的未支付订单，此订单可登录[ECS管理控制台](https://ecs.console.aliyun.com/)支付。

|
|DryRun|Boolean|否|是否只预检此次请求。-   true：发送检查请求，不会查询资源状况。检查项包括AccessKey是否有效、RAM用户的授权情况和是否填写了必需参数。如果检查不通过，则返回对应错误。如果检查通过，会返回错误码`DryRunOperation`。
-   false：发送正常请求，通过检查后返回2XX HTTP状态码并直接查询资源状况。

默认值：false

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

**返回示例**

**XML格式**

```
<ModifyInstanceConfigurationResponse>
    <RequestId>04F0F334-1335-436C-A1D7-6C044FExxxxx</RequestId>
    <OrderId>10111111111xxxxx</OrderId>
</ModifyInstanceConfigurationResponse>
```

**JSON格式**

```
{
    "RequestId": "04F0F334-1335-436C-A1D7-6C044FExxxxx",
    "OrderId": 1011111111111111,
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问[API错误中心](https://error-center.alibabacloud.com/status/product/Ecs)。

|错误代码|错误信息|HTTP状态码|说明|
|:---|:---|:------|:-|
|ExpiredInstance|Expired instances exist in your request list.|400|实例列表中存在欠费实例。|
|InstancesIdQuotaExceed|The maximum number of Instances is exceeded.|400|单次最多能指定20台实例。|
|InvalidInstance.UnpaidOrder|The specified instance has unpaid order.|400|实例有未支付的订单。|
|InvalidClientToken.ValueNotSupported|The ClientToken provided is invalid.|400|参数`ClientToken`参数值不合法，不能包含ASCII以外的字符。|
|InvalidParameter.InstanceIds|The specified InstanceIds are invalid.|400|指定的`InstanceIds`不合法。|
|InvalidStatus.ValueNotSupported|The instance cannot be modified in the specified status.|400|实例必须处于**运行中**（`Running`）或者**已停止**（`Stopped`）状态。|
|ReleaseTimeHaveBeenSet|The specified instance has been set released time.|400|您的请求中存在已设置了释放时间的实例。|
|Throttling|You have made too many requests within a short time; your request is denied due to request throttling.|400|您的操作过于频繁，请稍后再试。|
|InvalidPeriod.ExceededDedidactedHost|Instance expired date can't exceed dedicated host expired date.|400|实例生命周期不能长于专有宿主机生命周期。|
|InvalidAccountStatus.NotEnoughBalance|Your account does not have enough balance.|403|您的账户余额不足。|
|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|404|指定的实例不存在。|
|InternalError|The request processing has failed due to some unknown error, exception or failure.|500|内部错误。|

