# RenewInstance {#RenewInstance .reference}

续费一台预付费 ECS 实例。

## 描述 {#section_ut4_lk5_xdb .section}

调用该接口时，您需要注意：

-   仅支持续费预付费 ECS 实例。

-   除折扣账号之外，支付续费产生的账单时，默认优先使用您的账号下的代金券。

-   您的账号必须支持账号余额支付或信用支付。


## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：RenewInstance|
|InstanceId|String|是|需要续费的实例 ID。|
|Period|Integer|是|预付费续费时长。一旦指定了 DedicatedHostId，则取值范围不能超过专有宿主机的订阅时长。取值范围：-   `PeriodUnit=Week`时，Period 取值：\{“1”, “2”, “3”, “4”\}
-   `PeriodUnit=Month`时，Period 取值：\{ “1”, “2”, “3”, “4”, “5”, “6”, “7”, “8”, “9”, “12”, “24”, “36”,”48”,”60”\}

|
|PeriodUnit|String|否|续费时长的时间单位，即参数 `Period` 的单位。取值范围：-   Week
-   Month（默认）

|
|ClientToken|String|否| 保证请求幂等性。从您的客户端生成一个参数值，确保不同请求间该参数值唯一。只支持ASCII字符，且不能超过64个字符。更多详情，请参阅[如何保证幂等性](../intl.zh-CN/API 参考/附录/如何保证幂等性.md#)。

 |

## 返回参数 {#section_f54_lk5_xdb .section}

全是公共返回参数。参阅[公共返回参数](../intl.zh-CN/API 参考/快速入门/公共参数.md#commonResponseParameters)。

## 示例 { .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=RenewInstance
&InstanceId=i-instance1
&Period=1
&<公共请求参数>
```

**返回示例** 

**XML 格式**

```
<ModifyInstanceSpecResponse>
    <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</ModifyInstanceSpecResponse>
```

 **JSON 格式** 

```
{
    "RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E"
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问[API错误中心](https://error-center.alibabacloud.com/status/product/Ecs)。

|错误代码|错误信息|HTTP 状态码|说明|
|:---|:---|:-------|:-|
|IdempotenceParamNotMatch|Request uses a client token in a previous request but is not identical to that request.|400|您重用了 `ClientToken` 参数，但其他请求参数有变化。|
|InvalidClientToken.ValueNotSupported|The ClientToken provided is invalid.|400|`ClientToken`参数取值不能包含 ASCII 以外的字符。|
|InvalidPeriod|The specified period is not valid.|400|指定的 `Period` 参数取值格式无效，取值必须为数字并且在允许范围内。|
|ChargeTypeViolation|The operation is not permitted due to charge type of the instance.|403|仅支持续费预付费实例。|
|IncorrectInstanceStatus|The current status of the resource does not support this operation.|403|实例的当前状态不支持续费。|
|Instance.UnPaidOrder|The specified instance has unpaid order.|403|您的账号下有未付费的订单。|
|InstanceLockedForSecurity|The specified operation is denied as your instance is locked for security reasons.|403|实例已被安全锁定，无法续费。|
|LastTokenProcessing|The last token request is processing.|403|正在处理上一次请求，请稍后再试。|
|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|404|指定的 `InstanceId` 不存在。|

