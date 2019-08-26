# CreateSnapshot {#doc_api_Ecs_CreateSnapshot .reference}

调用CreateSnapshot为一块云盘创建一份快照。

## 接口说明 {#description .section}

-   一块云盘最多能创建64份快照。
-   云盘挂载的实例必须处于**已停止**（`Stopped`）或者**运行中**（`Running`）状态，否则无法创建快照。
-   云盘必须已经挂载到实例上，否则无法创建快照。
-   云盘挂载的实例从未启动过时，无法创建快照。
-   被 [安全控制](~~25695~~)的ECS实例的`OperationLocks`中标记了`"LockReason" : "security"`时，实例挂载的云盘无法创建快照。
-   新建一台云服务器ECS（[RunInstances](~~63440~~)）、更换系统盘（[ReplaceSystemDisk](~~25521~~)）或者根据快照新增数据盘（[CreateDisk](~~25513~~)），由于尚未完成数据加载，无法创建快照。新建一台云服务器ECS或者更换系统盘大约一小时后可以创建快照，新增一块数据盘可创建快照的时间取决于云盘数据的大小。
-   如果创建快照还未完成，您无法为该云盘再次创建快照。
-   如果创建快照还未完成，这份快照无法用于创建自定义镜像（[CreateImage](~~25535~~)）。
-   支持对处于**已过期**（`Expired`）状态的云盘创建快照。请注意，若创建快照时云盘正好达到过期释放时间，云盘会被释放的同时也会删除**创建中**（`Creating`）的快照。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=CreateSnapshot&type=RPC&version=2014-05-26)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|DiskId|String|是|d-diskid1|云盘ID。

 |
|Action|String|否|CreateSnapshot|系统规定参数。对于您自行拼凑HTTP/HTTPS URL发起的API请求，`Action`为必选参数。取值：CreateSnapshot

 |
|SnapshotName|String|否|FinanceJoshua|快照的显示名称。长度为2~128个英文或中文字符。必须以大小字母或中文开头，不能以http://和https://开头。可以包含数字、半角冒号（:）、下划线（\_）或者连字符（-）。

 为防止和自动快照的名称冲突，不能以auto开头。

 |
|Description|String|否|FinanceDepet|快照的描述。长度为2~256个英文或中文字符，不能以http://和https://开头。

 默认值：空。

 |
|RetentionDays|Integer|否|30|设置快照的保留时间，单位为天。保留时间到期后快照会被自动释放，取值范围：1~65536。

 默认值：空，表示快照不会被自动释放。

 |
|Tag.N.value|String|否|FinanceDept.Joshua|快照的标签值。

 **说明：** 为提高兼容性，建议您尽量使用Tag.N.Value参数。

 |
|Tag.N.key|String|否|FinanceDept|快照的标签键。

 **说明：** 为提高兼容性，建议您尽量使用Tag.N.Key参数。

 |
|Tag.N.Key|String|否|FinanceDept|快照的标签键。N的取值范围：1~20。一旦传入该值，则不允许为空字符串。最多支持64个字符，不能以aliyun和acs:开头，不能包含http://或者https://。

 |
|Tag.N.Value|String|否|FinanceDept.Joshua|快照的标签值。N的取值范围：1~20。一旦传入该值，可以为空字符串。最多支持128个字符，不能以aliyun和acs:开头，不能包含http://或者https://。

 |
|ClientToken|String|否|123e4567-e89b-12d3-a456-426655440000|保证请求幂等性。从您的客户端生成一个参数值，确保不同请求间该参数值唯一。**ClientToken**只支持ASCII字符，且不能超过64个字符。更多详情，请参见[如何保证幂等性](~~25693~~)。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。

 |
|SnapshotId|String|s-snapshotid1|快照ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=CreateSnapshot
&DiskId=d-diskid1
&SnapshotName=FinanceJoshua
&Description=FinanceDepet
&ClientToken=123e4567-e89b-12d3-a456-426655440000
&Tag.1.Key=FinanceDept
&Tag.1.Value=FinanceDept.Joshua
&<公共请求参数>
```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<CreateSnapshotResponse>
          <RequestId>C8B26B44-0189-443E-9816-D951F59623A9</RequestId>
          <SnapshotId>s-923FE2B**</SnapshotId>
</CreateSnapshotResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"C8B26B44-0189-443E-9816-D951F59623A9",
	"SnapshotId":"s-923FE2B**"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|404|InvalidDiskId.NotFound|The specified DiskId does not exist.|指定的磁盘不存在。请您检查磁盘 ID 是否正确。|
|400|InvalidSnapshotName.Malformed|The specified SnapshotName is wrongly formed.|快照名称格式不合法。长度为2-128个字符，以英文字母或中文开头，可包含数字，"."，"\_"或"-"。 不能以 http:// 和 https:// 开头。|
|404|InvalidDescription.Malformed|The specified description is wrongly formed.|指定的资源描述格式不合法。长度为2-256个字符，不能以 http:// 和 https:// 开头。|
|400|IncorrectInstanceStatus|The current status of the resource does not support this operation.|该资源目前的状态不支持此操作。|
|403|IncorrectDiskStatus.CreatingSnapshot|A previous snapshot creation is in process.|当前磁盘有创建中的快照，请您等待创建完成再试。|
|403|InstanceLockedForSecurity|The disk attached instance is locked due to security.|磁盘挂载的实例因安全原因被锁定。|
|403|IncorrectDiskStatus.NeverAttached|The specified disk has never been attached to any instance.|可卸载的云磁盘创建后未被挂载，内容没有变化。|
|403|QuotaExceed.Snapshot|The snapshot quota exceeds.|快照额度超过限制，若要存储新快照，在不影响业务的情况下，请您删除已有的老快照。|
|403|IncorrectDiskStatus.NeverUsed|The specified disk has never been used after creating.|磁盘创建后未被使用，内容没有变化。|
|403|CreateSnapshot.Failed|The process of creating snapshot is failed.|创建快照失败。|
|403|DiskInArrears|The specified operation is denied as your disk has expired.|磁盘欠费过期。|
|500|InternalError|The request processing has failed due to some unknown error.|内部错误，请重试。如果多次尝试失败，请提交工单|
|403|DiskId.ValueNotSupported|The specified parameter diskid is not supported.|当前磁盘类型不支持此操作|
|400|DiskCategory.OperationNotSupported|The operation is not supported to the specified disk due to its disk category|由于磁盘种类限制，指定的磁盘不支持该操作。|
|403|IncorrectDiskStatus|The current disk status does not support this operation.|当前的磁盘不支持此操作，请您确认磁盘处于正常使用状态，是否欠费。|
|403|InvalidAccountStatus.NotEnoughBalance|Your account does not have enough balance.|账号余额不足，请您先充值再进行该操作。|
|403|InvalidAccountStatus.SnapshotServiceUnavailable|Snapshot service has not been opened yet.|快照服务未开通，操作无法执行。|
|404|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|指定的实例不存在，请您检查实例ID是否正确。|
|403|IncorrectVolumeStatus|The current volume status does not support this operation.|共享块存储状态不支持当前操作,|
|404|InvalidVolumeId.NotFound|The specified volume does not exist.|指定的共享块存储不存在，请您检查共享块存储是否正确。|
|403|IdempotentParameterMismatch|The specified clientToken is used.|指定的token已被使用。|
|403|IncorrectDiskStatus.Invalid|The specified device status invalid, restart instance and try again.|指定磁盘的状态无效，请重启实例后重试。|
|403|IncorrectDiskType.NotSupport|The specified device type is not supported.|指定磁盘存储类型不支持此操作。|
|403|IncorrectDiskStatus.Transferring|The specified device is transferring, you can retry after the process is finished.|指定磁盘正在迁移中，请在迁移完毕后重试。|
|403|InvalidParameter.KMSKeyId.KMSUnauthorized|ECS service have no right to access your KMS.|ECS未被授权访问您的KMS资源。|
|500|InternalError|The request processing has failed due to some unknown error, exception or failure.|发生未知错误。|
|400|Duplicate.TagKey|The Tag.N.Key contain duplicate key.|标签键中存在重复的键。|
|400|InvalidTagKey.Malformed|The specified Tag.n.Key is not valid.|指定的标签键不合法。|
|400|InvalidTagValue.Malformed|The specified Tag.n.Value is not valid.|指定的标签值不合法。|
|403|IdempotentProcessing|The previous idempotent request\(s\) is still processing.|同样clienttoken的请求正在处理中。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ecs)查看更多错误码。

