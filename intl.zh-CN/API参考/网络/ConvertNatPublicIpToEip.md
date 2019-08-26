# ConvertNatPublicIpToEip {#doc_api_Ecs_ConvertNatPublicIpToEip .reference}

将一台网络类型为专有网络VPC的ECS实例的公网 IP（NatPublicIp）转化为弹性公网IP（EIP）。

## 接口说明 {#description .section}

调用该接口时，您需要注意：

-   仅支持VPC网络类型的ECS实例。
-   仅支持状态为已停止（Stopped）或者运行中（Running）的ECS实例。
-   不支持公网带宽为0 Mbps的实例，此时该ECS实例没有分配公网IP（NatPublicIp）。
-   不支持已经绑定了EIP的ECS实例。
-   不支持有未生效的变更配置任务ECS实例。
-   不支持即将在24小时内到期的ECS实例。
-   公网IP（NatPublicIp）转换为EIP后，EIP将单独计费。
-   不支持 [公网带宽](~~25411~~) 为按固定带宽计费的 [预付费（包年包月）](~~56220~~) ECS实例。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=ConvertNatPublicIpToEip)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|InstanceId|String|是|i-test|需要转化公网IP的实例ID。

 |
|RegionId|String|是|cn-hangzhou|实例所属的地域ID。您可以调用 [DescribeRegions](~~25609~~) 查看最新的阿里云地域列表。

 |
|Action|String|否|ConvertNatPublicIpToEip|系统规定参数。取值：ConvertNatPublicIpToEip

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=ConvertNatPublicIpToEip
&RegionId=cn-hangzhou
&InstanceId=i-test
&<公共请求参数>
```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ConvertNatPublicIpToEipResponse>
  <RequestId>B154D309-F3E1-4AB7-BA94-FEFCA8B89001</RequestId>
</ConvertNatPublicIpToEipResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"B154D309-F3E1-4AB7-BA94-FEFCA8B89001"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|403|InvalidInstanceId.PlanedChange|%s|实例的已经预约了表更操作，不支持该操作。|
|403|InvalidInstanceStatus.Released|%s|指定的实例状态无效。|
|403|IncorrectInstanceStatus|%s|实例当前的状态不支持该操作。|
|404|InvalidInstanceId.NotFound|%s|指定的实例不存在。|
|403|InvalidInternetChargeType.ValueNotSupported|%s|参数不支持。|
|403|MaxEIPQuotaExceeded|The number of EIP exceeds the limit per region.|已超出当前地域下的EIP数量。|
|403|InvalidInstance.OverduePayment|%s|您的账号已欠费，请充值后重试。|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Ecs)

