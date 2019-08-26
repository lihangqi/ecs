# AcceptInquiredSystemEvent {#doc_api_Ecs_AcceptInquiredSystemEvent .reference}

接受并授权执行系统事件操作。对问询中（Inquiring）状态的系统事件，接受系统事件的默认操作，授权系统执行默认操作。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=AcceptInquiredSystemEvent)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|EventId|String|是|e-2zeielxl1qzq8slblxyz|系统事件 ID。

 |
|RegionId|String|是|cn-hangzhou|地域 ID。您可以调用 [DescribeRegions](~~25609~~) 查看最新的阿里云地域列表。

 |
|Action|String|否|AcceptInquiredSystemEvent|系统规定参数。取值：AcceptInquiredSystemEvent

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|4DD56CA6-6D75-4D33-BE34-E4A44EBE1C3D|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://ecs.aliyuncs.com/?Action=AcceptInquiredSystemEvent
&EventId=e-2zeielxl1qzq8slblxyz
&RegionId=cn-hangzhou
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<AcceptInquiredSystemEventResponse>
  <RequestId>4DD56CA6-6D75-4D33-BE34-E4A44EBE1C3D</RequestId>
</AcceptInquiredSystemEventResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"4DD56CA6-6D75-4D33-BE34-E4A44EBE1C3D"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|MissingParameter|%s|缺失必需参数。|
|400|InvalidParameter|%s|参数格式不正确。|
|404|InvalidEventId.NoInquiringEventFound|%s|未找到Inquiring状态的事件。|
|403|OperationConflict|%s|和当前事件操作冲突的其他操作正在执行中，请稍后重试。|
|403|OperationFail.DiskCategoryNotSupported|%s|当前磁盘类别不支持此事件操作。|
|403|OperationFail.DiskStatusNotSupported|%s|当前磁盘状态不支持此事件操作。|
|403|OperationFail.InstanceStatusNotSupported|%s|当前实例状态不支持此事件操作。|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Ecs)

