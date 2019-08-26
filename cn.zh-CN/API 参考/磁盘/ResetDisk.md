# ResetDisk {#ResetDisk .reference}

使用磁盘的历史快照回滚至某一阶段的磁盘状态。

## 描述 {#section_qfp_gty_xdb .section}

调用该接口时，您需要注意：

-   磁盘的状态必须为 **使用中**（`In_Use`）的状态。

-   磁盘挂载的实例的状态必须为 **已停止**（`Stopped`\)。

-   指定的参数 `SnapshotId` 必须是由 `DiskId` 创建的历史快照。

-   被 [安全控制](cn.zh-CN/API参考/附录/安全锁定时的 API 行为.md#) 的 ECS 实例的 `OperationLocks` 中不能标记为 `"LockReason" : "security"`。


## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：ResetDisk|
|DiskId|String|是|指定的磁盘设备 ID。|
|SnapshotId|String|是|需要恢复到某一磁盘阶段的历史快照 ID。|

## 返回参数 {#section_yfp_gty_xdb .section}

全是公共返回参数。参阅 [公共参数](cn.zh-CN/API参考/调用方式/公共参数.md#commonResponseParameters)

## 示例 { .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=ResetDisk
&DiskId=d-23jbf2v5m
&SnapshotId=s-snapshot1
&<公共请求参数>
```

**返回示例** 

**XML 格式**

```
<ResetDiskResponse>
    <RequestId>F3CD6886-D8D0-4FEE-B93E-1B73239673DE</RequestId>
</ResetDiskResponse>
```

 **JSON 格式** 

```
{
    "RequestId":"F3CD6886-D8D0-4FEE-B93E-1B73239673DE"
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问 [API 错误中心](https://error-center.aliyun.com/status/product/Ecs)。

|错误代码|错误信息|HTTP 状态码|说明|
|:---|:---|:-------|:-|
|DiskCategory.OperationNotSupported|The operation is not supported to the specified disk due to its disk category.|400|指定磁盘的磁盘类型不支持该操作。|
|IncorrectDiskStatus|The current disk status does not support this operation.|403|磁盘的状态必须为 **使用中**（`In_Use`）的状态。|
|IncorrectInstanceStatus|The current status of the resource does not support this operation.|403|磁盘挂载的实例的状态必须为 **已停止**（`Stopped`）。|
|InstanceExpiredOrInArrears|The specified operation is denied as your prepay instance is expired \(prepay mode\) or in arrears \(afterpay mode\).|403|您的实例已过期或者已欠费。|
|InstanceLockedForSecurity|The instance is locked due to security.|403|指定的实例被 [安全控制](cn.zh-CN/API参考/附录/安全锁定时的 API 行为.md#)。|
|InvalidAccountStatus.NotEnoughBalance|Your account does not have enough balance.|403|账户余额不足。|
|InvalidAccountStatus.SnapshotServiceUnavailable|Snapshot service has not been opened yet.|403|您暂未开通快照服务，前往 [ECS 控制台](https://ecs.console.aliyun.com/) 开通。|
|InvalidParameter.Mismatch|The specified snapshot is not created from the specified disk.|403|指定的快照不是指定磁盘的历史快照。|
|InvalidSnapshot.TooOld|The snapshotId is created before 2013-07-15, it cannot be restored since the first time the disk detached.|403|指定的快照创建于 2013 年 7 月 15 日（含）之前，不能用于回滚磁盘。|
|InvalidSnapshotId.NotReady|The specified snapshot has not completed yet.|403|指定的快照还在创建中。|
|OperationDenied|The specified snapshot dees not support ResetDisk.|403|指定的快照不能用于回滚。|
|InvalidDiskId.NotFound|The specified disk does not exist.|404|指定的磁盘不存在。|
|InvalidSnapshotId.NotFound|The specified SnapshotId does not exist.|404|指定的快照不存在。|

