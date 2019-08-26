# DetachDisk {#DetachDisk .reference}

从一台实例上卸载一块按量付费磁盘。磁盘类型包括普通云盘、高效云盘和SSD云盘。

## 描述 {#section_udt_fp5_xdb .section}

当您使用该接口时，请注意：

-   云盘的 `Portable` 属性必须为 `True`。
-   云盘必须已经挂载到实例上，状态为 **使用中**（`In_Use`\)。
-   云盘所挂载的实例的状态必须为 **运行中**（`Running`）或者 **已停止**（`Stopped`）。
-   云盘所挂载的实例被 [安全控制](cn.zh-CN/API参考/附录/安全锁定时的 API 行为.md#) 后，`OperationLocks` 中不能标记为 `"LockReason" : "security"` 的锁定状态。
-   卸载磁盘后，其属性 `DeleteWithInstance` 会被置为 `False`，表示释放该实例时，会保留该云盘，不随实例一起释放。

-   该接口是异步操作，调用接口成功后您需要等待片刻才能完成卸载，预计在 1 分钟左右。


## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：DetachDisk|
|InstanceId|String|是|待卸载的 ECS 实例 ID。|
|DiskId|String|是|待卸载的云盘 ID。|

## 返回参数 {#section_c2t_fp5_xdb .section}

全是公共返回参数。参阅 [公共参数](cn.zh-CN/API参考/调用方式/公共参数.md#commonResponseParameters)

## 示例 { .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=DetachDisk
&InstanceId=i-23jggx34b
&DiskId=d-23jbf2v5m
&<公共请求参数>
```

**返回示例** 

**XML 格式**

```
<DetachDiskResponse>
    <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</DetachDiskResponse>
```

 **JSON 格式** 

```
{
    "RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E"
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问 [API 错误中心](https://error-center.aliyun.com/status/product/Ecs)。

|错误代码|错误信息|HTTP 状态码|说明|
|:---|:---|:-------|:-|
|InvalidParameter|The input parameter is mandatory for processing this request is empty.|400|请求缺少必填参数。|
|DependencyViolation|The specified disk has not been attached on the specified instance.|403|指定的磁盘并没有挂载在指定的实例上。|
|DiskNotPortable|The specified disk is not a portable disk.|403|指定磁盘不是可卸载的云盘。|
|DiskTypeViolation|The specified disk is a system disk and cannot support the operation.|403|您不能卸载实例的系统盘。|
|IncorrectDiskStatus|The current disk status does not support this operation.|403|磁盘必须已经挂载到实例上，状态为 **使用中**（`In_Use`\)。|
|IncorrectInstanceStatus|The current status of the resource does not support this operation.|403|磁盘所挂载的实例的状态必须为 **运行中**（`Running`）或者 **已停止**（`Stopped`）。|
|InstanceLockedForSecurity|The instance is locked due to security.|403|指定的实例被 [安全控制](cn.zh-CN/API参考/附录/安全锁定时的 API 行为.md#)。|
|InvalidDiskId.Released|The specified disk has been released.|403|指定的磁盘已经释放。|
|InvalidDiskId.NotFound|The specified DiskId does not exist.|404|指定的磁盘不存在。|
|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|404|指定的实例不存在。|

