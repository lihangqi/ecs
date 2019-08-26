# ReInitDisk {#ReInitDisk .reference}

重新初始化云盘到创建时的初始状态。

## 描述 {#section_rff_nsy_xdb .section}

调用该接口时，您需要注意：

-   云盘的状态必须为 **使用中**（`In_use`），且挂载的 ECS 实例的状态必须为 **已停止** （`Stopped`）。

-   实例首次启动前，不能重新初始化挂载在其上的云盘。

-   对于系统盘，初始化到镜像的最初状态。若创建云盘的源镜像被删除，则无法初始化。

-   对于直接创建的数据盘，初始化到空盘状态。

-   对于通过快照创建的数据盘，初始化到快照状态。若源快照已被删除，则无法初始化并返回错误。


## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：ReInitDisk。|
|DiskId|String|是|指定的云盘 ID。|
|SecurityEnhancementStrategy|String|否|当指定的云盘为系统盘时，您可以设置是否开启安全加固，加载云服务器 ECS 安全组件云盾等。取值范围：-   Active：启用安全加固，免费安装云盾。该值仅支持公共镜像。
-   Deactive：不启用安全加固，卸载云盾等安全组件。该值支持所有镜像。

|

## 返回参数 {#section_zff_nsy_xdb .section}

全是公共返回参数。参阅 [公共参数](intl.zh-CN/API 参考/调用方式/公共参数.md#commonResponseParameters)

## 示例 { .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=ReInitDisk
&DiskId=d-23jbf2v5m
&<公共请求参数>
```

**返回示例** 

**XML 格式**

```
<ReInitDiskResponse>
    <RequestId>F3CD6886-D8D0-4FEE-B93E-1B73239673DE</RequestId>
</ReInitDiskResponse>
```

 **JSON 格式** 

```
{
    "RequestId":"F3CD6886-D8D0-4FEE-B93E-1B73239673DE"
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问 [API 错误中心](https://error-center.alibabacloud.com/status/product/Ecs)。

|错误代码|错误信息|HTTP 状态码|说明|
|:---|:---|:-------|:-|
|DiskCategory.OperationNotSupported|The operation is not supported to the specified disk due to its disk category|400|指定云盘的磁盘类型不支持该操作。|
|DiskCreatingSnapshot|The operation is denied due to a snapshot of the specified disk is not completed yet.|403|指定的云盘正在创建快照，请稍后再试。|
|IncorrectDiskStatus|The current disk status does not support this operation.|403|云盘状态必须为 **使用中**（`In_use`）。|
|IncorrectInstanceStatus|The current status of the resource does not support this operation.|403|云盘挂载的 ECS 实例的状态必须为 **已停止**（`Stopped`）。|
|InstanceExpiredOrInArrears|The specified operation is denied as your prepay instance is expired \(prepay mode\) or in arrears \(afterpay mode\).|403|云盘挂载的 ECS 实例已欠费停机。|
|InstanceLockedForSecurity|The instance is locked due to security.|403|云盘挂载的 ECS 实例已被 [安全控制](intl.zh-CN/API 参考/附录/安全锁定时的 API 行为.md#)。|
|InvalidSnapshot.TooOld|The disk is created from a snapshotId made before 2013-07-15, it cannot be re-initiated the specified disk any more since the detached first time.|403|指定云盘的源快照创建于 2013 年 7 月 15 日及其之前，不能初始化。|
|InvalidSourceSnapshot|The snapshot which is used to create the specified disk has been deleted.|403|指定云盘的源快照已被删除，无法初始化。|
|OperationDenied|The snapshot which is used to create the specified disk has been deleted.|403|指定云盘的源快照已被删除，无法初始化。|
|SharedImageDeleted|The specified image by others shared is deleted.|403|创建指定云盘的共享镜像已被删除，无法初始化。|
|InvalidDiskId.NotFound|The specified disk does not exist.|404|指定的云盘不存在。|

