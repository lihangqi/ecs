# DeleteInstances {#doc_api_Ecs_DeleteInstances .reference}

调用DeleteInstances释放一台或多台按量付费ECS实例或者到期的包年包月ECS实例。

## 接口说明 {#description .section}

-   释放实例时，实例被[安全控制](~~25695~~)并且其`OperationLocks`中标记了`"LockReason" : "security"`的锁定状态，即使云盘的`DeleteWithInstance`的属性为`False`，系统会忽略这个属性而释放挂载在实例上的云盘。
-   释放后，实例所使用的物理资源都被回收，相关数据全部丢失且不可恢复。挂载在实例上 `DeleteWithInstance=True`属性的云盘被释放，云盘的快照仍旧保留。云盘的自动快照的保留和释放跟随云盘的`DeleteAutoSnapshot`属性，如果为`DeleteAutoSnapshot=false`时，保留自动快照，如果为`DeleteAutoSnapshot=true`，释放自动快照。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=DeleteInstances&type=RPC&version=2014-05-26)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|InstanceId.N|RepeatList|是|i-instanceid1|实例ID。N的取值范围：1~100。

 |
|Action|String|否|DeleteInstances|系统规定参数。对于您自行拼凑HTTP/HTTPS URL发起的API请求，`Action`为必选参数。取值：DeleteInstances

 |
|TerminateSubscription|Boolean|否|false|是否释放已到期的包年包月实例。

 默认值：false。

 |
|Force|Boolean|否|false|是否强制释放**运行中**（`Running`）的ECS实例。

 -   true：强制释放**运行中**（`Running`）的实例。强制释放相当于断电，实例内存以及存储中的临时数据都会被擦除，无法恢复。
-   false（默认值）：正常释放实例，此时实例必须处于**已停止**（`Stopped`）状态。

 |
|DryRun|Boolean|否|false|是否只预检此次请求。

 -   true：发送检查请求，不会查询资源状况。检查项包括AccessKey是否有效、RAM用户的授权情况和是否填写了必需参数。如果检查不通过，则返回对应错误。如果检查通过，会返回错误码DryRunOperation。
-   false（默认值）：发送正常请求，通过检查后返回2XX HTTP状态码并直接查询资源状况。

 |
|ClientToken|String|否|123e4567-e89b-12d3-a456-426655440000|保证请求幂等性。从您的客户端生成一个参数值，确保不同请求间该参数值唯一。**ClientToken**只支持ASCII字符，且不能超过64个字符。更多详情，请参见[如何保证幂等性](~~25693~~)。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|7B7813C6-57BF-41XX-B12B-F172F65A6046|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=DeleteInstances
&InstanceId.1=i-instance1
&Force=false
&<公共请求参数>
```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DeleteInstancesResponse>
      <RequestId>7B7813C6-57BF-41XX-B12B-F172F65A6046</RequestId>
</DeleteInstancesResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"7B7813C6-57BF-41XX-B12B-F172F65A6046"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|403|InvalidOperation.NotInWhiteList|%s|灰度中参数。|
|403|InvalidOperation.DeletionProtection|%s|实例被删除保护了。|
|403|IncorrectInstanceStatus|%s|实例当前的状态不支持该操作。|
|403|IncorrectInstanceStatus|The current status of the resource does not support this operation.|该资源目前的状态不支持此操作。|
|500|InternalError|The request processing has failed due to some unknown error.|内部错误，请重试。如果多次尝试失败，请提交工单。|
|500|InternalError|%s|内部错误。|
|403|InstanceLockedForSecurity|The specified operation is denied as your instance is locked for security reasons.|实例被安全锁定，指定的操作无法完成。|
|400|DependencyViolation.SLBConfiguring|Specified operation is denied as your instance is using by another product.|实例被SLB引用，且SLB正在配置。|
|400|DependencyViolation.RouteEntry|Specified instance is used by route entry.|当前专有网络VPC还存在未删除的自定义路由规则，删除失败。|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

