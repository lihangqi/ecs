# ResetDisk {#doc_api_1030729 .reference}

使用磁盘的历史快照回滚至某一阶段的磁盘状态。

## 接口说明 {#description .section}

调用该接口时，您需要注意：

-   磁盘的状态必须为 使用中（In\_Use）的状态。
-   磁盘挂载的实例的状态必须为 已停止（Stopped\)。
-   指定的参数 SnapshotId 必须是由 DiskId 创建的历史快照。
-   被 [安全控制](~~25695~~) 的 ECS 实例的 OperationLocks 中不能标记为 "LockReason" : "security"。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=ResetDisk)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|DiskId|String|是|d-diskid1|指定的磁盘设备 ID。

 |
|SnapshotId|String|是|s-snapshotid1|需要恢复到某一磁盘阶段的历史快照 ID。

 |
|Action|String|否|ResetDisk|系统规定参数。取值：ResetDisk

 |
|OwnerAccount|String|否|ECSforCloud@Alibaba.com|RAM 用户的账号登录名称。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

https://ecs.aliyuncs.com/?Action=ResetDisk
&DiskId=d-diskid1
&SnapshotId=s-snapshotid1
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ResetDiskResponse>
  <RequestId>F3CD6886-D8D0-4FEE-B93E-1B73239673DE</RequestId>
</ResetDiskResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"F3CD6886-D8D0-4FEE-B93E-1B73239673DE"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|404|Disk.NotFound|The specified disk does not exist.|指定的磁盘不存在，请您检查磁盘是否正确。|
|403|IncorrectInstanceStatus|The current status of the resource does not support this operation.|该资源目前的状态不支持此操作。|
|403|InstanceLockedForSecurity|The instance is locked due to security.|您的资源被安全锁定，拒绝操作。|
|403|InvalidParameter.Mismatch|The specified snapshot is not created from the specified disk.|指定的快照不是该磁盘的快照。|
|403|InvalidSnapshot.TooOld|The snapshotId is created before 2013-07-15, it cannot be restored since the first time the disk detached.|指定的快照创建时间不能晚于2013年7月15日。|
|403|InstanceExpiredOrInArrears|The specified operation is denied as your prepay instance is expired \(prepay mode\) or in arrears \(afterpay mode\).|包年包月实例已过期，请您续费后再进行操作。|
|403|OperationDenied|The specified snapshot dees not support ResetDisk.|指定的快照不支持重置磁盘。|
|403|InvalidSnapshotId.NotReady|The specified snapshot has not completed yet.|指定的快照未完成。|
|403|InvalidAccountStatus.NotEnoughBalance|Your account does not have enough balance.|账号余额不足，请您先充值再进行该操作。|
|403|Operation.Conflict|The operation may conflicts with others.|该操作与其他操作冲突。|
|403|UserNotInTheWhiteList|The user is not in disk white list.|您暂时不能使用该磁盘服务。|
|500|InternalError|The request processing has failed due to some unknown error, exception or failure.|发生未知错误。|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Ecs)

