# DeleteInstance {#DeleteInstance .reference}

释放一台按量付费实例或者到期的预付费（包年包月）实例。

## 描述 {#section_bvk_f4s_xdb .section}

-   释放后，实例所使用的物理资源都被回收，相关数据全部丢失且不可恢复。挂载在实例上 `DeleteWithInstance=True`属性的云盘被释放，云盘的快照仍旧保留。云盘的自动快照的保留和释放跟随云盘的 `DeleteAutoSnapshot` 属性，如果为 `DeleteAutoSnapshot=false` 时，保留自动快照，如果为 `DeleteAutoSnapshot=true`，释放自动快照。
-   释放实例时，实例被 [安全控制](intl.zh-CN/API 参考/附录/安全锁定时的 API 行为.md#) 并且其 `OperationLocks` 中标记了 `"LockReason" : "security"` 的锁定状态，即使云盘的 `DeleteWithInstance` 的属性为 `False`，系统会忽略这个属性而释放挂载在实例上的云盘。

## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：DeleteInstance|
|InstanceId|String|是|实例 ID。|
|TerminateSubscription|Boolean|否|是否释放已到期的预付费（包年包月）实例。默认值：false。

|
|Force|Boolean|否|是否强制释放 **运行中**（`Running`）的实例。-   true：强制释放 **运行中**（`Running`）的实例。强制释放相当于断电，实例内存以及存储中的临时数据都会被擦除，无法恢复。
-   false：正常释放实例，此时实例必须处于 **已停止**（`Stopped`）状态。

默认值：false。

|

## 返回参数 {#ResponseParameter .section}

全是公共返回参数。参阅 [公共返回参数](intl.zh-CN/API 参考/快速入门/公共参数.md#commonResponseParameters)。

## 示例 { .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=DeleteInstance
&InstanceId=i-instance1
&<公共请求参数>
```

**返回示例** 

**XML 格式** 

```
<DeleteInstanceResponse>
    <RequestId>928E2273-5715-46B9-A730-238DC996A533</RequestId>
</DeleteInstanceResponse>
```

**JSON 格式** 

```
{
    "RequestId": "928E2273-5715-46B9-A730-238DC996A533"
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问 [API 错误中心](https://error-center.alibabacloud.com/status/product/Ecs)。

|错误代码|错误信息|HTTP 状态码|说明|
|:---|:---|:-------|:-|
|DependencyViolation.RouteEntry|Specified instance is used by route entry.|400|[路由条目](../../../../../intl.zh-CN/用户指南/路由.md#) 正在使用该实例。|
|DependencyViolation.SLBConfiguring|Specified operation is denied as your instance is using by another product.|400|[负载均衡](../../../../../intl.zh-CN/产品简介/什么是负载均衡.md#) 正在使用该实例。|
|InvalidParameter|The input parameter InstanceId is invalid.|400|指定的实例 ID 不合法。|
|ChargeTypeViolation|The operation is not permitted due to charge type of the instance.|403|不能释放包年包月的实例。|
|IncorrectInstanceStatus|The current status of the resource does not support this operation.|403|实例必须处于 **已停止**（`Stopped`）状态。|
|IncorrectInstanceStatus.Initializing|The specified instance status does not support this operation.|403|实例正在创建中，请稍后重试。|
|InstanceLockedForSecurity|The specified operation is denied as your instance is locked for security reasons.|403|该资源目前被安全锁定，拒绝操作。|
|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|404|指定的实例不存在。|

