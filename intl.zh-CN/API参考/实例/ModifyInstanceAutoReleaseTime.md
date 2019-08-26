# ModifyInstanceAutoReleaseTime {#doc_api_1161583 .reference}

为一台按量付费 实例设定或者取消自动释放时间。设置自动释放时请谨慎操作，配置的时间到期后将自动释放 ECS 实例。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=ModifyInstanceAutoReleaseTime)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|InstanceId|String|是|i-instanceid1|需要自动释放的 ECS 实例 ID。

 |
|Action|String|否|ModifyInstanceAutoReleaseTime|接口名称。取值：**ModifyInstanceAutoReleaseTime**

 |
|AutoReleaseTime|String|否|2018-01-01T01:02:03Z|自动释放时间。按照 [ISO8601](~~25696~~) 标准表示，并需要使用 UTC 时间。格式为：yyyy-MM-ddTHH:mm:ssZ。

 -   如果秒（`ss`）取值不是 `00`，则自动取为当前分钟（`mm`）开始时。
-   最短释放时间为当前时间半小时之后。
-   最长释放时间不能超过当前时间三年。

 如果不传入参数 `AutoReleaseTime`，表示自动释放功能已取消，ECS 实例不再自动释放。

 |
|OwnerAccount|String|否|ECSforCloud@Alibaba.com|RAM用户的账号登录名称。

 |
|RegionId|String|否|cn-hangzhou|实例所属的地域 ID。您可以调用 [DescribeRegions](~~25609~~) 查看最新的阿里云地域列表。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。无论调用接口成功与否，我们都会返回请求 ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

https://ecs.aliyuncs.com/?Action=ModifyInstanceAutoReleaseTime
&InstanceId=i-instance1
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ModifyInstanceAutoReleaseTimeResponse>
  <RequestId>04F0F334-1335-436C-A1D7-6C044FE73368</RequestId>
</ModifyInstanceAutoReleaseTimeResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"C0003E8B-B930-4F59-ADC0-0E209A9012A8"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|MissingParameter|InstanceId should not be null.|参数 RegionId 不得为空。|
|500|InternalError|The request processing has failed due to some unknown error, exception or failure.|发生未知错误。|
|403|ChargeTypeViolation|The operation is not permitted due to charge type of the instance.|付费方式不支持该操作，请您检查实例的付费类型是否与该操作冲突。|
|404|NoSuchResource|The specified resource is not found.|指定的资源不存在|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Ecs)

