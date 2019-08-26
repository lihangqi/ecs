# CreateSimulatedSystemEvents {#doc_api_Ecs_CreateSimulatedSystemEvents .reference}

调用CreateSimulatedSystemEvents为一台或多台ECS实例预约模拟系统事件。模拟系统事件相当于事件演习，不会真正执行事件，也不会对ECS实例产生影响。

## 接口说明 {#description .section}

预约模拟事件后，您可以通过ECS管理控制台、[ECS API](~~63962~~) 和云监控服务查看已经预约的模拟系统事件。

下表为模拟系统事件的生命周期：

-   Scheduled（计划中）：预约后，模拟系统事件自动切换为Scheduled状态。
-   Executed（已完成）：在没有人为干预的情况下，模拟系统事件在指定时间点（NotBefore）自动变成Executed状态。
-   Canceled（已取消）：您调用 [CancelSimulatedSystemEvents](~~88808~~) 取消模拟系统事件后，变成Canceled状态。
-   Avoided（已避免）：对于因系统维护实例重启（SystemMaintenance.Reboot）的模拟系统事件，可以通过在指定时间点前 [重启实例](~~25502~~) 而变成Avoided状态。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=CreateSimulatedSystemEvents)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|EventType|String|是|SystemMaintenance.Reboot|系统事件的类型。取值范围：

 -   SystemMaintenance.Reboot：因系统维护实例重启
-   SystemFailure.Reboot：因系统错误实例重启
-   InstanceFailure.Reboot：因实例错误实例重启

 |
|InstanceId.N|RepeatList|是|i-instance1|一个或者多个ECS实例ID。N的取值范围：1~100，多个取值使用重复列表的形式。

 |
|NotBefore|String|是|2018-12-01T06:32:31Z|事件计划执行时间的开始时间。按照 [ISO8601](~~25696~~) 标准表示，并需要使用UTC时间，格式为yyyy-MM-ddTHH:mm:ssZ。

 |
|RegionId|String|是|cn-hangzhou|地域ID。您可以调用 [DescribeRegions](~~25609~~) 查看最新的阿里云地域列表。

 |
|Action|String|否|CreateSimulatedSystemEvents|系统规定参数。取值：CreateSimulatedSystemEvents

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|EventIdSet| |e-xhskHun1256\*\*\*\*|模拟事件ID（EventId）列表。

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=CreateSimulatedSystemEvents
&EventType=SystemMaintenance.Reboot
&InstanceId.1=i-instance1
&NotBefore=2018-12-01T06:32:31Z
&RegionId=cn-hangzhou
&<公共请求参数>
```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<CreateSimulatedSystemEventsResponse>
  <EventIdSet>
    <EventId>e-bp191hqye********34x</EventId>
    <EventId>e-bp191hqye********34y</EventId>
  </EventIdSet>
  <RequestId>E69EF3CC-94CD-42E7-8926-F133B86387C0</RequestId>
</CreateSimulatedSystemEventsResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"EventIdSet":{
		"EventId":[
			"e-bp191hqye********34x",
			"e-bp191hqye********34y"
		]
	},
	"RequestId":"679E9056-9B75-4306-8A72-A1DF93EBEF74"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|404|MissingParameter|%s|缺失必需参数。|
|403|InvalidParameter|%s|参数格式不正确。|
|403|InvalidNotBefore.Passed|%s|指定的NotBefore不得早于当前时间。|
|404|InvalidInstanceId.NotFound|%s|指定的实例不存在。|
|403|SimulatedEventLimitExceeded|%s|已达到可设置模拟事件的个数上限。|
|403|InstanceIdLimitExceeded|%s|指定的InstanceId个数不得超过100个。|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

