# RedeployInstance {#doc_api_1063670 .reference}

当 ECS 实例收到系统事件通知时，RedeployInstance 可以重新部署这台实例。

## 接口说明 {#description .section}

RedeployInstance 为异步调用接口，会重启迁移实例。重新部署成功后，实例进入 运行中（Running）状态。重新部署失败时，实例返回原有的物理服务器，并恢复到重新部署前的状态。调用该接口时，您需要注意：

-   RedeployInstance 能响应以下系统事件类型，更多有关系统事件的详情，请参阅 [系统事件](~~66574~~)：
    -   待执行（Scheduled）状态下的实例重启（SystemMaintenance.Reboot）事件和实例重新部署（SystemMaintenance.Redeploy）事件。
    -   执行中（ Executing）状态下的实例异常重启（ SystemFailure.Reboot）事件（仅支持本地盘实例规格）。

        **警告：** 重新部署本地盘实例会重新初始化本地盘，磁盘数据被清空。请慎重操作。

-   目标实例必须处于运行中或者已停止状态，调用接口后的实例状态变化：
    -   处于运行中（Running）的实例会进入 停止中（Stopping）状态。
    -   处于 已停止（Stopped）的实例会进入 启动中（Starting）状态。
-   被安全控制的实例的 OperationLocks 中标记了 "LockReason": "security" 时，不支持重新部署。
-   不支持重新部署专有宿主机上的实例。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=RedeployInstance)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|InstanceId|String|是|i-bp1azkttqpldxgtedXXX|处于运行中或者已停止状态的实例 ID。

 |
|Action|String|否|RedeployInstance|接口名称。取值: RedeployInstance

 |
|ForceStop|Boolean|否|false|是否强制停止 运行中（Running）的实例。默认值：false

 **说明：** 强制停止等同于典型的服务器断电关机，实例操作系统中暂未写入磁盘的数据会丢失。建议您尽量对已停止实例做重新部署操作。

 |
|OwnerAccount|String|否|ECSforCloud@Alibaba.com|RAM用户的账号登录名称。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。

 |
|TaskId|String|t-bp10e8orkpqm0lc74o8x|重新部署的任务ID。您可以使用[DescribeTasks](~~25622~~)接口查询迁移结果，以下为使用DescribeTasks时需要设置的参数示例：

 -   请参设置示例：`TaskIds=["t-bp10e8orkpqm0lc74o8x", "t-bp10e8orkpqm0lc74o8y"]`，`TaskAction=RedeployInstance`
-   返参查询示例：
    -   TaskStatus=Processing表示正在重新部署中
    -   TaskStatus=Finished表示已完成重新部署，实例进入运行中（Running）状态
    -   TaskStatus=Failed表示重新部署失败，实例返回原有的物理服务器，并恢复到重新部署前的状态。请[提交工单](https://selfservice.console.aliyun.com/ticket/createIndex)联系阿里云技术支持

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

https://ecs.aliyuncs.com/?Action=RedeployInstance
&InstanceId=i-bp1azkttqpldxgtedXXX
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<RedeployInstanceResponse>
    <RequestId>1C488B66-B819-4D14-8711-C4EAAA13AC01</RequestId>
    <TaskId>t-bp10e8orkpqm0lc74o8x</TaskId>
</RedeployInstanceResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"1C488B66-B819-4D14-8711-C4EAAA13AC01",
	"TaskId":"t-bp10e8orkpqm0lc74o8x"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|403|IncorrectInstanceStatus|The current status of the resource does not support this operation.|该资源目前的状态不支持此操作。|
|403|DiskError|IncorrectDiskStatus.|指定的磁盘状态不合法。|
|403|InstanceExpiredOrInArrears|The specified operation is denied as your prepay instance is expired \(prepay mode\) or in arrears \(afterpay mode\).|包年包月实例已过期，请您续费后再进行操作。|
|403|IncorrectInstanceStatus|%s|实例当前的状态不支持该操作。|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Ecs)

