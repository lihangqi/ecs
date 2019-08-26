# DescribeInstanceAutoRenewAttribute {#doc_api_1161575 .reference}

查询一台或多台预付费实例自动续费状态。

## 描述 {#description .section}

在设置自动续费或者手动续费前，查询实例续费状态能使您了解实例是否已为自动续费状态。

只支持 [包年包月](~~56220~~) 的实例，[按量付费](~~40653~~) 的实例调用该接口会报错。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=DescribeInstanceAutoRenewAttribute)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|RegionId|String|是|cn-hangzhou|实例所属的地域 ID。您可以调用 [DescribeRegions](~~25609~~) 查看最新的阿里云地域列表。

 |
|Action|String|否|DescribeInstanceAutoRenewAttribute|接口名称。取值：**DescribeInstanceAutoRenewAttribute**

 |
|InstanceId|String|否|i-instance1,i-instance2|实例 ID。支持最多 100 个包年包月实例批量查询，多个实例 ID 以半角逗号分隔。

 |
|OwnerAccount|String|否|ECSforCloud@Alibaba.com|RAM用户的账号登录名称。

 |
|PageNumber|String|否|1|查询接口返回资源信息列表的页码。

 起始值：1。

 默认值：1。

 |
|PageSize|String|否|10|分页展示响应信息时设置的每页行数，单位：行。

 最大值：100。

 默认值：10。

 |
|RenewalStatus|String|否|AutoRenewal|实例的自动续费状态。取值范围：

 -   AutoRenewal：设置为自动续费。
-   Normal：取消自动续费。
-   NotRenewal：不再续费，系统不再发送到期提醒，只在到期前第三天发送不续费提醒。不再续费的 ECS 实例可以通过 [ModifyInstanceAutoRenewAttribute](~~52843~~) 更改成待续费（`Noramal`） 后，再自行续费或设置为自动续费。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|InstanceRenewAttributes| | |实例续费的属性集合

 |
|└AutoRenewEnabled|Boolean|false|是否已设置自动续费。

 |
|└Duration|Integer|1|自动续费时长。

 |
|└InstanceId|String|i-instanceid1|实例 ID。

 |
|└PeriodUnit|String|week|自动续费时长的单位。

 |
|└RenewalStatus|String|Normal|实例的自动续费状态。取值范围：

 -   AutoRenewal：设置为自动续费。
-   Normal：取消自动续费。
-   NotRenewal：不再续费，系统不再发送到期提醒，只在到期前第三天发送不续费提醒。不再续费的 ECS 实例可以通过 [ModifyInstanceAutoRenewAttribute](~~52843~~) 更改成待续费（`Noramal`） 后，再自行续费或设置为自动续费。

 |
|PageNumber|Integer|1|查询接口返回资源信息列表的页码。

 起始值：1。

 默认值：1。

 |
|PageSize|Integer|10|分页展示响应信息时设置的每页行数，单位：行。

 最大值：100。

 默认值：10。

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。无论调用接口成功与否，我们都会返回请求 ID。

 |
|TotalCount|Integer|6|返回的实例总数。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

https://ecs.aliyuncs.com/?Action=DescribeInstanceAutoRenewAttribute
&RegionId=cn-hangzhou
&InstanceId=i-instance1,i-instance2
&PageNumber=1
&PageSize=10
&RenewalStatus=AutoRenewal
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeInstanceAutoRenewAttributeResponse>
  <RequestId>04F0F334-1335-436C-A1D7-6C044FE73368</RequestId>
  <InstanceRenewAttributes>
    <InstanceRenewAttribute>
      <Instance>
        <InstanceId>i-instance1</InstanceId>
        <Duration>0</Duration>
        <AutoRenewEnalbed>false</AutoRenewEnalbed>
        <RenewalStatus>Normal</RenewalStatus>
      </Instance>
      <Instance>
        <InstanceId>i-instance2</InstanceId>
        <Duration>1</Duration>
        <AutoRenewEnalbed>true</AutoRenewEnalbed>
        <RenewalStatus>AutoRenewal</RenewalStatus>
      </Instance>
    </InstanceRenewAttribute>
  </InstanceRenewAttributes>
</DescribeInstanceAutoRenewAttributeResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"InstanceRenewAttributes":{
		"InstanceRenewAttribute":[
			{
				"RenewalStatus":"Normal",
				"InstanceId":"i-instance1",
				"Duration":0,
				"AutoRenewEnabled":false
			},
			{
				"RenewalStatus":"AutoRenewal",
				"InstanceId":"i-instance2",
				"Duration":1,
				"AutoRenewEnabled":true
			}
		]
	},
	"RequestId":"04F0F334-1335-436C-A1D7-6C044FE73368"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|403|MissingParameter.InstanceId|InstanceId should not be null.|参数 InstanceId 不能为空。|
|403|InvalidParameter.InvalidInstanceId|%s|InstanceId参数无效。|
|403|IncorrectInstanceStatus|The current status of the resource does not support this operation.|该资源目前的状态不支持此操作。|
|403|InvalidParameter.RenewalStatus|The specified parameter RenewalStatus is not valid.|续费状态参数无效。|
|403|InvalidParameter.RenewalStatusInstanceId|The parameter RenewalStatus and InstanceId can not be both empty.|续费状态与实例ID不能同时为空。|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Ecs)

