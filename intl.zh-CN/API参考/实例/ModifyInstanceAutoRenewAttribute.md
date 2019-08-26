# ModifyInstanceAutoRenewAttribute {#doc_api_Ecs_ModifyInstanceAutoRenewAttribute .reference}

设置一台或多台预付费实例的自动续费状态。为了减少您的资源到期维护成本，包年包月 ECS 实例可以设置自动续费。

## 接口说明 {#description .section}

请确保在使用该接口前，您已充分了解 [云服务器 ECS](https://www.alibabacloud.com/product/ecs#pricing) 的计费方式和产品定价。

-   自动续费扣款日为实例到期前第 9 天，扣费在北京时间 （UTC +8） 08:00:00 开始执行。
-   如果前一日执行自动扣费失败，将会继续下一日定时继续执行，直到扣费成功或者 9 天之后实例到期锁定。您只需要保证自己的账号的余额或者信用额度充足即可。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=ModifyInstanceAutoRenewAttribute)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|InstanceId|String|是|i-instance1,i-instance2|实例 ID。支持批量设置最多 100 个包年包月实例，多个实例 ID 以英文逗号分隔。

 |
|RegionId|String|是|cn-hangzhou|实例所属的地域 ID。您可以调用 [DescribeRegions](~~25609~~) 查看最新的阿里云地域列表。

 |
|Action|String|否|ModifyInstanceAutoRenewAttribute|接口名称。取值：**ModifyInstanceAutoRenewAttribute**

 |
|AutoRenew|Boolean|否|true|实例到期前是否自动续费。默认值：false

 |
|Duration|Integer|否|2|设置实例自动续费时长。

 -   `PeriodUnit`为`year`（年）时，`Duration`的取值范围为：\{"1", "2", "3"\}
-   `PeriodUnit`为`month`（月）时，`Duration`的取值范围为：\{"1", "2", "3", "6", "12"\}

 |
|PeriodUnit|String|否|week|续费时长的时间单位，即参数 `Period` 的单位。取值范围：

 -   month（默认）
-   year

 |
|RenewalStatus|String|否|AutoRenewal|置是否不再续费，参数 `RenewalStatus` 的优先级高于参数 `AutoRenew`。如果不传入参数 `RenewalStatus`，则默认以参数 `AutoRenew`为准。取值范围：

 -   AutoRenewal：设置为自动续费。
-   Normal：取消自动续费。
-   NotRenewal：不再续费。传入该值后，系统不再发送到期提醒，只在到期前第三天发送不续费提醒。不再续费的 ECS 实例可以更改成待续费（`Noramal`） 后，再自行续费或设置为自动续费。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=ModifyInstanceAutoRenewAttribute
&RegionId=cn-hangzhou
&InstanceId=i-instance1,i-instance2
&Duration=2
&AutoRenew=True
&<公共请求参数>
```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ModifyInstanceAutoRenewAttributeResponse>
  <RequestId>04F0F334-1335-436C-A1D7-6C044FE73368</RequestId>
</ModifyInstanceAutoRenewAttributeResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"04F0F334-1335-436C-A1D7-6C044FE73368"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|403|MissingParameter.InstanceId|InstanceId should not be null.|参数 InstanceId 不能为空。|
|403|InvalidParameter.ToManyInstanceIds|InstanceId should be less than 100.|实例数应小于100。|
|403|InvalidParameter.InvalidInstanceId|%s|InstanceId参数无效。|
|403|IncorrectInstanceStatus|The current status of the resource does not support this operation.|该资源目前的状态不支持此操作。|
|403|ChargeTypeViolation|Pay-As-You-Go instances do not support this operation.|按量付费实例不支持该操作，检查实例的付费类型是否与该操作冲突。|
|403|InvalidParameter.Duration|%s|Duration参数无效。|
|403|InvalidParameter.RenewalStatus|%s|RenewalStatus参数无效。|
|403|InvalidPeriodUnit.ValueNotSupported|The specified parameter PeriodUnit is not valid.|市场单位不支持。|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Ecs)

