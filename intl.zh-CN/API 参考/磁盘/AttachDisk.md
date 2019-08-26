# AttachDisk {#AttachDisk .reference}

为一台ECS实例挂载一块数据盘。

## 描述 {#section_vgf_j45_xdb .section}

调用该接口时，您需要注意：

-   待挂载的ECS实例的状态必须为**运行中**（`Running`）或者**已停止**（`Stopped`）。
-   挂载数据盘时，云盘的状态必须为**待挂载**（`Available`）。
-   被 [安全控制](../intl.zh-CN/API 参考/附录/安全锁定时的 API 行为.md#) 的ECS实例的`OperationLocks`不能标记为`"LockReason" : "security"`。
-   即使您在挂载云盘时，将`DeleteWithInstance`置为`false`，一旦ECS实例被安全控制，且 `OperationLocks`中标记了`"LockReason" : "security"`，释放ECS实例时会忽略云盘的`DeleteWithInstance`属性而被同时释放。

## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：AttachDisk|
|InstanceId|String|是|待挂载的ECS实例ID。|
|DiskId|String|是|待挂载的云盘ID。云盘（`DiskId`）和实例（`InstanceId`）必须在同一个可用区。|
|DeleteWithInstance|Boolean|否|释放实例时，该云盘是否随实例一起释放。默认值：False|

## 返回参数 {#ResponseParameter .section}

全是公共返回参数。参阅 [公共返回参数](../intl.zh-CN/API 参考/调用方式/公共参数.md#commonResponseParameters)。

## 示例 { .section}

**请求示例**

```
https://ecs.aliyuncs.com/?Action=AttachDisk
&InstanceId=i-23jggx34b
&DiskId=d-23jbf2v5m
&<公共请求参数>
```

**返回示例**

**XML格式**

```
<AttachDiskResponse>
    <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</AttachDiskResponse>
```

**JSON格式**

```
{
    "RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E"
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问 [API错误中心](https://error-center.alibabacloud.com/status/product/Ecs)。

|错误代码|错误信息|HTTP状态码|说明|
|:---|:---|:------|:-|
|IncorrectInstanceStatus|The current status of the resource does not supportthis operation.|400|待挂载的ECS实例的状态必须为**运行中**（`Running`）或者**已停止**（`Stopped`）。|
|InvalidParameter|The input parameter is mandatory for processing thisrequest is empty.|400|缺少必填参数。|
|DiskError|IncorrectDiskStatus.|403|云盘的状态必须为**待挂载**（`Available`）。|
|DiskId.ValueNotSupported|The specified parameter diskid is not supported.|403|指定的磁盘不支持挂载。|
|DiskInArrears|The specified operation is denied as your disk owingfee.|403|指定的云盘已欠费。|
|DiskNotPortable|The specified disk is not a portable disk.|403|指定云盘不是可卸载的云盘。|
|IncorrectDiskStatus|The operation is not supported in this status.|403|挂载数据盘时，云盘的状态必须为**待挂载**（`Available`）。|
|InstanceExpiredOrInArrears|The specified operation is denied as your prepay instance is expired \(prepay mode\) or in arrears \(afterpay mode\).|403|指定的实例已欠费。|
|InstanceLockedForSecurity|The instance is locked due to security.|403|指定的实例被安全锁定。|
|InvalidDevice.InUse|The specified device has been occupied.|403|指定的云盘已经被挂载到其他实例上。|
|ResourcesNotInSameZone|The specified instance and disk are not in the samezone.|403|指定云盘和实例必须在同一个可用区。|
|InvalidDiskId.NotFound|The specified disk does not exist.|404|指定的云盘不存在。|
|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|404|指定的实例不存在。|

