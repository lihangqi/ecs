# ModifyInstanceNetworkSpec {#ModifyInstanceNetworkSpec .reference}

修改实例的带宽配置。当实例现有网络规格不满足要求时，可以通过修改实例的带宽配置提高网络性能。

## 描述 {#section_rb5_jnn_ydb .section}

调用该接口时，您需要注意：

-   修改**包年包月**（PrePaid）实例的带宽配置时：

    -   可以升级或者降配计费方式为**按使用流量**（PayByTraffic）的带宽。

    -   **公网出带宽**（InternetMaxBandwidthOut）从0 Mbps升级到一个非零值时会自动分配一个公网 IP。

-   修改**按量付费**（PostPaid）实例的带宽配置时：
    -   可以升级或者降配带宽。

    -   **公网出带宽**（InternetMaxBandwidthOut）从0 Mbps升级到一个非零值时不会自动分配公网IP，您需要调用[AllocatePublicIpAddress](intl.zh-CN/API 参考/网络/AllocatePublicIpAddress.md#)为实例分配公网IP。

-   对于经典网络（Classic）类型实例，当**公网出带宽**（InternetMaxBandwidthOut）从0 Mbps升级到一个非零值时，实例必须处于**已停止**（`Stopped`）状态。

-   升级带宽后，默认自动扣费。您需要确保账户余额充足，否则会生成异常订单，此时只能作废订单。如果您的账户余额不足，可以将参数AutoPay置为false，此时会生成正常的未支付订单，您可以登录[ECS管理控制台](https://ecs.console.aliyun.com/) 支付。

-   每台预付费（包年包月）实例降低公网带宽的次数不能超过三次，即价格差退款不会超过三次。

-   修改带宽配置前后的价格差退款会退还到您的原付费方式中，已使用的代金券不退回。

-   单个实例每成功操作一次，五分钟内不能继续操作。


## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：ModifyInstanceNetworkSpec|
|InstanceId|String|是|需要修改网络配置的实例ID。|
|InternetMaxBandwidthOut|Integer|否|公网出带宽最大值，单位为Mbps（Megabit per second）。取值范围：\[0, 100\]|
|InternetMaxBandwidthIn|Integer|否|设置公网入带宽最大值，单位为Mbps（Megabit per second）。取值范围：\[1, 200\]|
|NetworkChargeType|String|否|转换网络计费方式。取值范围：-   PayByTraffic：按使用流量计费

|
|AutoPay|Boolean|否|是否自动支付。取值范围：-   true：变更带宽配置后，自动扣费。当您将参数 Autopay 置为 True 时，您需要确保账户余额充足，如果账户余额不足会生成异常订单，此订单暂时不支持通过 ECS 控制台支付，只能作废。
-   false：变更带宽配置后，只生成订单不扣费。如果您的账户余额不足，可以将参数 Autopay 置为 false，即取消自动支付，此时调用该接口会生成正常的未支付订单，此订单可登录[ECS管理控制台](https://ecs.console.aliyun.com/)支付。

默认值：true|
|ClientToken|String|否| 保证请求幂等性。从您的客户端生成一个参数值，确保不同请求间该参数值唯一。只支持ASCII字符，且不能超过64个字符。更多详情，请参阅[如何保证幂等性](../intl.zh-CN/API 参考/附录/如何保证幂等性.md#)。

 |

## 返回参数 {#ResponseParameter .section}

|名称|类型|描述|
|:-|:-|:-|
|RequestId|String|请求ID|
|OrderId|Long|生成的订单ID|

## 示例 { .section}

**请求示例**

```
https://ecs.aliyuncs.com/?Action=ModifyInstanceNetworkSpec
&RegionId=cn-hangzhou
&InstanceId=i-xxxxx1
&InternetMaxBandwidthOut=10
&ClientToken=xxxxxxxxxxxxxx
&<公共请求参数>
```

**返回示例**

**XML格式**

```
<ModifyInstanceNetworkSpecResponse>
      <RequestId>04F0F334-1335-436C-A1D7-6C044FE73368</RequestId>
</ModifyInstanceNetworkSpecResponse>
```

**JSON格式**

```
{
      "RequestId": "04F0F334-1335-436C-A1D7-6C044FE73368"
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问[API错误中心](https://error-center.alibabacloud.com/status/product/Ecs)。

|错误代码|错误信息|HTTP状态码|说明|
|:---|:---|:------|:-|
|Account.Arrearage|Your account has an outstanding payment.|400|账号已经欠费。|
|DecreasedBandWidthNotAllowed|A higher bandwidth than the current one is required.|400|新带宽不能低于已有带宽。|
|InvalidInstance.UnpaidOrder|The specified instance has unpaid order.|400|当前实例有未支付的订单。|
|InvalidInstanceStatus.NotStopped|The specified Instance status is not Stopped.|400|实例未处于停止状态。|
|InvalidInternetChargeType.ValueNotSupported|The specified InternetChargeType is invalid.|400|指定的InternetChargeType不存在。|
|InvalidInternetMaxBandwidthIn.ValueNotSupported|The specified InternetMaxBandwidthIn is beyond the permitted range.|400|指定的InternetMaxBandwidthIn超出取值范围。|
|InvalidInternetMaxBandwidthOut.ValueNotSupported|The specified InternetMaxBandwidthOut is beyond the permitted range.|400|指定的InternetMaxBandwidthOut超出取值范围。|
|MissingParameter|The input parameter “InstanceId” that is mandatory for processing this request is not supplied.|400|缺少InstanceId值|
|OperationDenied|Specified instance is in VPC.|400|VPC网络实例不支持该操作。|
|ChargeTypeViolation|The operation is not permitted due to billing method of the instance.|403|当前实例的付费类型不支持此操作。|
|IncorrectInstanceStatus|The current status of the instance does not support this operation.|403|该实例目前的状态不支持此操作。|
|InstanceExpiredOrInArrears|The specified operation is denied as your prepay instance is expired \(prepay mode\) or in arrears \(afterpay mode\).|403|实例到期或者欠费（是指该实例是包年包月或者按量欠费的情况）。|
|InstanceLockedForSecurity|The specified operation is denied as your instance is locked for security reasons.|403|该实例目前被[安全控制](intl.zh-CN/API 参考/附录/安全锁定时的 API 行为.md#)，拒绝操作。|
|InvalidAccountStatus.NotEnoughBalance|Your account does not have enough balance.|403|账户余额不足。|
|OperationDenied|The operation is denied due to the instance is PrePaid.|403|包年包月实例不支持此操作。|
|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|404|指定的实例ID不存在。|
|InternalError|The request processing has failed due to some unknown error, exception or failure.|500|内部错误，请稍后再试。|

