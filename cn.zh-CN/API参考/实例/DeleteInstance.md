# DeleteInstance {#doc_api_Ecs_DeleteInstance .reference}

调用DeleteInstance释放一台按量付费实例或者到期的预付费（包年包月）实例。

## 接口说明 {#description .section}

-   释放后，实例所使用的物理资源都被回收，相关数据全部丢失且不可恢复。挂载在实例上 `DeleteWithInstance=True`属性的云盘被释放，云盘的快照仍旧保留。云盘的自动快照的保留和释放跟随云盘的 `DeleteAutoSnapshot` 属性，如果为 `DeleteAutoSnapshot=false` 时，保留自动快照，如果为 `DeleteAutoSnapshot=true`，释放自动快照。
-   释放实例时，实例被 [安全控制](~~25695~~) 并且其 `OperationLocks` 中标记了 `"LockReason" : "security"` 的锁定状态，即使云盘的 `DeleteWithInstance` 的属性为 `False`，系统会忽略这个属性而释放挂载在实例上的云盘。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=DeleteInstance)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|InstanceId|String|是|i-instance1|实例 ID。

 |
|Action|String|否|DeleteInstance|系统规定参数。取值：DeleteInstance

 |
|Force|Boolean|否|false|是否强制释放 **运行中**（`Running`）的实例。

 -   true：强制释放 **运行中**（`Running`）的实例。强制释放相当于断电，实例内存以及存储中的临时数据都会被擦除，无法恢复。
-   false（默认值）：正常释放实例，此时实例必须处于 **已停止**（`Stopped`）状态。

 |
|TerminateSubscription|Boolean|否|false|是否释放已到期的预付费（包年包月）实例。 默认值：false。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。无论调用接口成功与否，我们都会返回请求 ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

https://ecs.aliyuncs.com/?Action=DeleteInstance
&InstanceId=i-instance1
&Force=false
&TerminateSubscription=false
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DeleteInstanceResponse>
  <RequestId>928E2273-5715-46B9-A730-238DC996A533</RequestId>
</DeleteInstanceResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"928E2273-5715-46B9-A730-238DC996A533"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|403|IncorrectInstanceStatus|The current status of the resource does not support this operation.|该资源目前的状态不支持此操作。|
|403|InstanceLockedForSecurity|The specified operation is denied as your instance is locked for security reasons.|实例被安全锁定，指定的操作无法完成。|
|403|ChargeTypeViolation|The operation is not permitted due to charge type of the instance.|付费方式不支持该操作，请您检查实例的付费类型是否与该操作冲突。|
|500|InternalError|The request processing has failed due to some unknown error.|内部错误，请重试。如果多次尝试失败，请提交工单|
|400|DependencyViolation.SLBConfiguring|Specified operation is denied as your instance is using by another product.|实例被SLB引用，且SLB正在配置。|
|400|DependencyViolation.RouteEntry|Specified instance is used by route entry.|当前专有网络VPC还存在未删除的自定义路由规则，删除失败。|
|400|InvalidParameter|The input parameter InstanceId is invalid.|指定的 InstanceId 不合法，请您检查 InstanceId 是否正确，且存在。|
|404|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|指定的实例不存在，请您检查实例ID是否正确。|
|403|IncorrectInstanceStatus.Initializing|The specified instance status does not support this operation.|实例正在初始化中，暂时无法释放请稍后重试。|
|403|IncorrectInstanceStatus|The specified instance is still attached by volumes.|指定的实例上存在数据卷。|
|403|InvalidOperation.DeletionProtection|%s|实例被删除保护了。|
|403|InvalidOperation.NotInWhiteList|%s|灰度中参数。|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

