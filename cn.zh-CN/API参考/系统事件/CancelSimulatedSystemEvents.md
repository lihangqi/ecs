# CancelSimulatedSystemEvents {#doc_api_Ecs_CancelSimulatedSystemEvents .reference}

取消一件或多件处于Scheduled（计划中）或Executing（执行中）状态的模拟系统事件。取消系统事件后，模拟事件变为Canceled（已取消）状态。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=CancelSimulatedSystemEvents)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|EventId.N|RepeatList|是|e-xhskHun1256xxxx|一个或者多个系统事件ID。N的取值范围：1~100，多个取值使用重复列表的形式。

 |
|RegionId|String|是|cn-hangzhou|地域ID。您可以调用 [DescribeRegions](~~25609~~) 查看最新的阿里云地域列表。

 |
|Action|String|否|CancelSimulatedSystemEvents|系统规定参数。取值：CancelSimulatedSystemEvents

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=CancelSimulatedSystemEvents
&EventId.1=e-xhskHun1256xxxx
&RegionId=cn-hangzhou
&<公共请求参数>
```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<CancelSimulatedSystemEventsResponse>
  <RequestId>E69EF3CC-94CD-42E7-8926-F133B86387C0</RequestId>
</CancelSimulatedSystemEventsResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"E69EF3CC-94CD-42E7-8926-F133B86387C0"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|404|MissingParameter|%s|缺失必需参数。|
|403|InvalidParameter|%s|参数格式不正确。|
|403|CannotCancelSystemEvent.NotSimulated|%s|不能取消非模拟的系统事件。|
|403|InvalidEventId.NotFound|%s|指定的EventId不存在。|
|400|EventIdLimitExceeded|%s|一次最多能指定100个模拟事件ID。|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Ecs)

