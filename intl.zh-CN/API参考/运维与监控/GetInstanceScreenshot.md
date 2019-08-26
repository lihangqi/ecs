# GetInstanceScreenshot {#doc_api_999429 .reference}

获取实例的截屏信息。

## 描述 {#description .section}

我们返回Base64编码后的JPG图像格式的实例截屏，您需要自行解码。您可以在排查故障时调用该接口，并请注意：

-   实例必须处于运行中（Running）状态。
-   [已停售的实例规格](~~55263~~) 无法获取截屏信息。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=GetInstanceScreenshot)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|InstanceId|String|是|i-myInstance|实例ID。

 |
|RegionId|String|是|cn-shenzhen|实例所在地域ID。您可以调用 [DescribeRegions](~~25609~~) 查看最新的阿里云地域列表。

 |
|Action|String|否|GetInstanceScreenshot|系统规定参数。取值：GetInstanceScreenshot

 |
|OwnerAccount|String|否|ECSforCloud@Alibaba.com|RAM 用户的账号登录名称。

 |
|WakeUp|Boolean|否|false|是否唤醒处于休眠状态的实例。

 默认值：false

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|InstanceId|String|i-myInstance|实例ID。

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。无论调用接口成功与否，我们都会返回请求 ID。

 |
|Screenshot|String|iVBORw0KGgoA...AAABJRU5ErkJggg==|JPG图像格式的实例截屏，返回Base64编码后的图像。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http://ecs-cn-hangzhou.example.com/?Action=GetInstanceScreenshot
&InstanceId=i-myInstance
&RegionId=cn-shenzhen
&WakeUp=false
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<GetInstanceScreenshotResponse>
  <RequestId>22A1933F-AD02-4560-A6A7-53CF2231D942</RequestId>
  <InstanceId>i-j5e42sbbthlokka11ech</InstanceId>
  <Screenshot>iVBORw0KGgoA...AAABJRU5ErkJggg==</Screenshot>
</GetInstanceScreenshotResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"Screenshot":"iVBORw0KGgoA...AAABJRU5ErkJggg==",
	"InstanceId":"i-j5e42sbbthlokka11ech",
	"RequestId":"22A1933F-AD02-4560-A6A7-53CF2231D942"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|MissingParameter|%s|缺失必需参数。|
|404|InvalidParameter|%s|参数格式不正确。|
|405|IncorrectInstanceStatus|%s|实例当前的状态不支持该操作。|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Ecs)

