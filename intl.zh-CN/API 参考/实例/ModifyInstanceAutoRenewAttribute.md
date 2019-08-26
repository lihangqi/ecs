# ModifyInstanceAutoRenewAttribute {#ModifyInstanceAutoRenewAttribute .reference}

设置一台或多台预付费实例的自动续费状态。

## 描述 {#section_hjb_cg5_xdb .section}

-   为了减少您的资源到期维护成本，包年包月 ECS 实例可以设置自动续费，自动续费扣款日为实例到期前第 9 天，扣费在北京时间 （UTC +8） 08:00:00 开始执行。

-   如果前一日执行自动扣费失败，将会继续下一日定时继续执行，直到扣费成功或者 9 天之后实例到期锁定。您只需要保证自己的账号的余额或者信用额度充足即可。


## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：ModifyInstanceAutoRenewAttribute|
|RegionId|String|是|实例所属的地域 ID。您可以调用 [DescribeRegions](intl.zh-CN/API参考/地域/DescribeRegions.md#) 查看最新的阿里云地域列表。|
|InstanceId|String|是|实例 ID。支持批量设置最多 100 个包年包月实例，多个实例 ID 以英文逗号分隔。|
|Duration|Integer|否|设置实例自动续费时长。单位：月，取值：1|2|3|6|12|
|AutoRenew|Boolean|否|设置是否自动续费。取值范围：-   True：设置为自动续费类型。
-   False：取消自动续费类型。

默认值： False|
|RenewalStatus|String|否|设置是否不再续费，参数 `RenewalStatus` 的优先级高于参数 `AutoRenew`。如果不传入参数 `RenewalStatus`，则默认以参数 `AutoRenew`为准。取值范围：-   AutoRenewal：设置为自动续费。
-   Normal：取消自动续费。
-   NotRenewal：不再续费。传入该值后，系统不再发送到期提醒，只在到期前第三天发送不续费提醒。不再续费的 ECS 实例可以更改成待续费（`Noramal`） 后，再自行续费或设置为自动续费。

|

## 返回参数 {#section_rjb_cg5_xdb .section}

全是公共返回参数。参阅 [公共参数](intl.zh-CN/API参考/调用方式/公共参数.md#commonResponseParameters)。

## 示例 { .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=ModifyInstanceAutoRenewAttribute
&RegionId=cn-hangzhou
&InstanceId=i-instance1,i-instance2
&Duration=2
&AutoRenew=True
&<公共请求参数>
```

**返回示例** 

**XML 格式**

```
<ModifyInstanceAutoRenewAttributeResponse>
    <RequestId>04F0F334-1335-436C-A1D7-6C044FE73368</RequestId>
</ModifyInstanceAutoRenewAttributeResponse>
```

 **JSON 格式** 

```
{
    "RequestId": "04F0F334-1335-436C-A1D7-6C044FE73368"
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问 [API 错误中心](https://error-center.alibabacloud.com/status/product/Ecs)。

|错误代码|错误信息|HTTP 状态码|说明|
|:---|:---|:-------|:-|
|ChargeTypeViolation|Pay-As-You-Go instances do not support this operation.|403|此操作不支持按量付费实例类型。|
|IncorrectInstanceStatus|The current status of the resource does not support this operation.|403|由于实例已过期，不支持此操作。|
|InvalidParameter.Duration|The auto renewal duration should be one of the following values: 1|2|3|6|12.|403|指定的续费时长不符合要求，应为 \[1,2,3,6,12\] 中的一个。|
|InvalidParameter.InvalidInstanceId|The specified instanceId is not valid.|403|指定的 `InstanceId` 无效。|
|InvalidParameter.ToManyInstanceIds|No more than 100 InstanceIds can be specified.|403|指定的 `InstanceId` 数量不能大于 100。|
|MissingParameter.InstanceId|InstanceId should not be null.|403|参数 `InstanceId` 不能为空。|

