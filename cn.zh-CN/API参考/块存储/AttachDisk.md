# AttachDisk {#doc_api_Ecs_AttachDisk .reference}

调用AttachDisk为一台ECS实例挂载一块按量付费数据盘。

## 接口说明 {#description .section}

调用该接口时，您需要注意：

-   待挂载的ECS实例的状态必须为**运行中**（Running）或者**已停止**（Stopped）。
-   挂载数据盘时，云盘的状态必须为`待挂载`（Available）。
-   被[安全控制](~~25695~~)的ECS实例的`OperationLocks`不能标记为`"LockReason" : "security"`。
-   即使您在挂载云盘时，将`DeleteWithInstance`置为`false`，一旦ECS实例被安全控制，且`OperationLocks`中标记了`"LockReason" : "security"`，释放ECS实例时会忽略云盘的`DeleteWithInstance`属性而被同时释放。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=AttachDisk&type=RPC&version=2014-05-26)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|DiskId|String|是|d-23jbf2v5m|待挂载的云盘ID。云盘（`DiskId`）和实例（`InstanceId`）必须在同一个可用区。

 |
|InstanceId|String|是|i-instance1|待挂载的ECS实例ID。

 |
|Action|String|否|AttachDisk|系统规定参数。取值：AttachDisk

 |
|DeleteWithInstance|Boolean|否|false|释放实例时，该云盘是否随实例一起释放。

 默认值：False。

 |
|Device|String|否|/dev/xvda|云盘设备名称。

 **说明：** 该参数即将被弃用，为提高兼容性，建议您尽量使用其他参数。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=AttachDisk
&DiskId=d-23jbf2***
&InstanceId=i-instance1
&DeleteWithInstance=false
&<公共请求参数>
```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<AttachDiskResponse>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</AttachDiskResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|404|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|指定的实例不存在，请您检查实例ID是否正确。|
|404|InvalidDiskId.NotFound|The specified disk does not exist.|指定的磁盘不存在。请您检查磁盘 ID 是否正确。|
|400|InvalidDevice.Malformed|The specified device is not valid.|指定的磁盘设备名不存在。|
|403|InstanceDiskLimitExceeded|The amount of the disk on instance in question reach its limits.|指定实例已经达到可挂载磁盘的最大值。|
|403|InvalidDevice.InUse|The specified device has been occupied.|指定的设备已经挂载了磁盘。|
|403|IncorrectDiskStatus|The operation is not supported in this status.|当前的磁盘不支持此操作，请您确认磁盘处于正常使用状态，是否欠费。|
|403|DiskNotPortable|The specified disk is not a portable disk.|指定的磁盘不是可卸载的磁盘，Portable为false的磁盘无法卸载。|
|403|InstanceLockedForSecurity|The instance is locked due to security.|您的资源被安全锁定，拒绝操作。|
|403|ResourcesNotInSameZone|The specified instance and disk are not in the same zone.|指定的实例和磁盘不在同一可用区。|
|403|InstanceExpiredOrInArrears|The specified operation is denied as your prepay instance is expired \(prepay mode\) or in arrears \(afterpay mode\).|包年包月实例已过期，请您续费后再进行操作。|
|403|DiskInArrears|The specified operation is denied as your disk owing fee.|指定的磁盘已欠费。|
|400|IncorrectInstanceStatus|The current status of the resource does not support this operation.|该资源目前的状态不支持此操作。|
|403|DiskError|IncorrectDiskStatus.|指定的磁盘状态不合法。|
|403|DiskError|IncorrectDiskStatus|指定的磁盘状态不合法。|
|500|InternalError|The request processing has failed due to some unknown error.|内部错误，请重试。如果多次尝试失败，请提交工单。|
|400|InvalidParameter|The input parameter is mandatory for processing this request is empty.|参数不能为空。|
|403|DiskId.ValueNotSupported|The specified parameter diskid is not supported.|当前磁盘类型不支持此操作|
|403|DiskId.StatusNotSupported|The specified disk status is not supported.|不支持指定的磁盘状态。|
|404|InvalidDisk.InUse|The specified disk has been occupied.|指定的磁盘已占用。|
|404|DiskAttachedNumberExceeded|The attaching times of the specified disk exceeded.|超过了该磁盘的附加时间。|
|403|UserNotInTheWhiteList|The user is not in disk white list.|您暂时不能使用该磁盘服务。|
|400|InvalidRegionId.MalFormed|The specified RegionId is not valid|指定的 RegionId 不合法。|
|400|InvalidOperation.InstanceTypeNotSupport|The instance type of the specified instance does not support hot attach disk.|磁盘挂载的实例不支持磁盘热插拔操作。|
|400|DiskCategory.OperationNotSupported|The operation is not supported to the specified disk due to its disk category|由于磁盘种类限制，指定的磁盘不支持该操作。|
|400|InvalidOperation.InstanceTypeNotSupport|The specified disk which has kms key should only attach to ioOptimized instance.|仅I/O优化实例支持KMS Key。|
|403|InvalidParameter.KMSKeyId.KMSUnauthorized|ECS service have no right to access your KMS.|ECS未被授权访问您的KMS资源。|
|500|InternalError|The request processing has failed due to some unknown error, exception or failure.|发生未知错误。|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

