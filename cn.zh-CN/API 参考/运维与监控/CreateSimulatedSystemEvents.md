# CreateSimulatedSystemEvents {#CreateSimulatedSystemEvents .reference}

为一台或多台ECS实例预约模拟系统事件。模拟系统事件相当于事件演习，不会真正执行事件，也不会对ECS实例产生影响。

## 描述 {#section_hbw_vnm_x2b .section}

-   预约模拟事件后，您可以通过ECS管理控制台、[ECS API](cn.zh-CN/API 参考/运维与监控/DescribeInstanceHistoryEvents.md#)和云监控服务查看已经预约的模拟系统事件。

-   下表为模拟系统事件的生命周期：

    |名称|描述|状态详情|
    |:-|:-|:---|
    |`Scheduled`|计划中|预约后，模拟系统事件自动切换为`Scheduled`状态。|
    |`Executed`|已完成|在没有人为干预的情况下，模拟系统事件在指定时间点（NotBefore）自动变成`Executed`状态。|
    |`Canceled`|已取消|您调用[CancelSimulatedSystemEvents](cn.zh-CN/API 参考/运维与监控/CancelSimulatedSystemEvents.md#)取消模拟系统事件后，变成`Canceled`状态。|
    |`Avoided`|已避免|对于因系统维护实例重启（SystemMaintenance.Reboot）的模拟系统事件，可以通过在指定时间点前[重启实例](cn.zh-CN/API 参考/实例/RebootInstance.md#)而变成`Avoided`状态。|


## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：CreateSimulatedSystemEvents|
|RegionId|String|是|地域ID。您可以调用[DescribeRegions](../cn.zh-CN/API 参考/地域/DescribeRegions.md#)查看最新的阿里云地域列表。|
|InstanceId.N|String|是|一个或者多个ECS实例ID。N的取值范围：\[1, 100\]，多个取值使用重复列表的形式。|
|EventType|String|是|系统事件的类型。取值范围：-   SystemMaintenance.Reboot：因系统维护实例重启
-   SystemFailure.Reboot：因系统错误实例重启
-   InstanceFailure.Reboot：因实例错误实例重启

|
|NotBefore|String|是|事件计划执行时间的开始时间。按照[ISO8601](../cn.zh-CN/API 参考/附录/时间格式.md#)标准表示，并需要使用UTC时间，格式为yyyy-MM-ddTHH:mm:ssZ。|

## 返回参数 {#ResponseParameter .section}

|名称|类型|描述|
|:-|:-|:-|
|EventIdSet|List of `EventId`|模拟事件ID（EventId）列表。|

## 示例 { .section}

**请求示例**

```
https://ecs.aliyuncs.com/?Action=CreateSimulatedSystemEvents
&RegionId=cn-hangzhou
&InstanceId.1=i-instance1
&InstanceId.2=i-instance1
&EventType=SystemMaintenance.Reboot
&NotBefore=2018-12-01T06:32:31Z
&<公共请求参数>
```

**返回示例**

**XML格式**

```
<CreateSimulatedSystemEventsResponse>
	<EventIdSet>
		<EventId>e-xhskHun1256xxxx</EventId>
		<EventId>e-xhskHun1257xxxx</EventId>
	</EventIdSet>
        <RequestId>E69EF3CC-94CD-42E7-8926-F133B86387C0</RequestId>
</CreateSimulatedSystemEventsResponse>
```

**JSON格式**

```
{
    "RequestId":"E69EF3CC-94CD-42E7-8926-F133B86387C0",
	"EventIdSet":{
		"EventId": "e-xhskHun1256xxxx",
		"EventId": "e-xhskHun1257xxxx"
	}
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问 [API错误中心](https://error-center.aliyun.com/status/product/Ecs)。

|错误代码|错误信息|HTTP状态码|说明|
|:---|:---|:------|:-|
|InvalidNotBefore.Passed|The NotBefore of system event has passed.|400|指定的NotBefore不能晚于当前时间。|
|InvalidInstanceId.NotFound|Cannot find InstanceId.|400|指定的实例ID不存在。|
|SimulatedEventLimitExceeded|The amount of active simulated system event exceeds limit.|400|已超过当前地域下最大活跃模拟事件数量。|
|InstanceIdLimitExceeded|The amount of InstanceId specified exceeds limit.|400|一次最多指定100个实例ID。|
|MissingParameter|The input parameter that is mandatory for processing this request is not supplied.|404|缺失必需参数。|

