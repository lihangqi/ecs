# CreateSnapshot {#CreateSnapshot .reference}

为一块ECS磁盘创建一份快照。

## 描述 {#section_syj_wjz_xdb .section}

调用该接口时，您需要注意：

-   一块磁盘最多能创建64份快照。

-   磁盘挂载的实例必须处于**已停止**（`Stopped`）或者**运行中**（`Running`）状态，否则无法创建快照。

-   磁盘必须已经挂载到实例上，否则无法创建快照。

-   磁盘挂载的实例从未启动过时，无法创建快照。

-   被[安全控制](../intl.zh-CN/API 参考/附录/安全锁定时的 API 行为.md#)的ECS实例的`OperationLocks`不能标记为`"LockReason" : "security"`。

-   新建一台云服务器ECS（[RunInstances](intl.zh-CN/API 参考/实例/RunInstances.md#)）、更换系统盘（[ReplaceSystemDisk](intl.zh-CN/API 参考/磁盘/ReplaceSystemDisk.md#)）或者根据快照新增数据盘（[CreateDisk](intl.zh-CN/API 参考/磁盘/CreateDisk.md#)），由于尚未完成数据加载，无法创建快照。新建一台云服务器ECS或者更换系统盘大约1小时后可以创建快照，新增一块数据盘可创建快照的时间取决于磁盘数据的大小。

-   如果创建快照还未完成，您无法为该磁盘再次创建快照。

-   如果创建快照还未完成，这份快照无法用于创建自定义镜像（[CreateImage](intl.zh-CN/API 参考/镜像/CreateImage.md#)）。


## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：CreateSnapshot|
|DiskId|String|是|磁盘ID。|
|SnapshotName|String|否|快照的显示名称。长度为\[2, 128\]个英文或中文字符。必须以大小字母或中文开头，不能以http://和https://开头。可以包含数字、半角冒号（:）、下划线（\_）或者连字符（-）。为防止和[自动快照](intl.zh-CN/API 参考/快照/CreateAutoSnapshotPolicy.md#)的名称冲突，不能以`auto`开头。

|
|Description|String|否|快照的描述。长度为\[2, 256\]个英文或中文字符，不能以http://和https://开头。默认值：空

|
|Tag.n.Key|String|否|快照的标签键。n的取值范围：\[1, 20\]。一旦传入该值，则不允许为空字符串。最多支持64个字符，不能以aliyun、acs:、http://或者https://开头。|
|Tag.n.Value|String|否|快照的标签值。n的取值范围：\[1, 20\]。一旦传入该值，可以为空字符串。最多支持128个字符，不能以aliyun、acs:、http://或者https://开头。|
|ClientToken|String|否| 保证请求幂等性。从您的客户端生成一个参数值，确保不同请求间该参数值唯一。只支持ASCII字符，且不能超过64个字符。更多详情，请参阅[如何保证幂等性](../intl.zh-CN/API 参考/附录/如何保证幂等性.md#)。

 |

## 返回参数 {#ResponseParameter .section}

|名称|类型|描述|
|:-|:-|:-|
|SnapshotId|String|快照ID|

## 示例 { .section}

**请求示例**

```
https://ecs.aliyuncs.com/?Action=CreateSnapshot
&DiskId=1033-60053321
&<公共请求参数>
```

**返回示例**

**XML格式**

```
<CreateSnapshotResponse>
        <RequestId>C8B26B44-0189-443E-9816-D951F59623A9</RequestId>
        <SnapshotId>s-923FE2BF0</SnapshotId>
</CreateSnapshotResponse>
```

**JSON格式**

```
{
    "RequestId": "C8B26B44-0189-443E-9816-D951F59623A9",
    "SnapshotId": "s-923FE2BF0"
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问[API错误中心](https://error-center.alibabacloud.com/status/product/Ecs)。

|错误代码|错误信息|HTTP状态码|说明|
|:---|:---|:------|:-|
|DiskCategory.OperationNotSupported|The operation is not supported to the specified disk due to its disk category|400|指定磁盘的磁盘类型不支持该操作。|
|IncorrectInstanceStatus|The current status of the resource does not support this operation.|400|磁盘挂载的实例必须处于**已停止**（`Stopped`）或者**运行中**（`Running`）状态。|
|InvalidSnapshotName.Malformed|The specified SnapshotName is wrongly formed.|400|指定的参数`SnapshotName`不合法。|
|CreateSnapshot.Failed|The process of creating snapshot is failed.|403|创建快照失败。|
|DiskId.ValueNotSupported|The specified parameter diskid is not supported.|403|指定的参数`DiskId`不能创建快照。|
|DiskInArrears|The specified operation is denied as your disk has expired.|403|指定的磁盘已经欠费。请重新续费后重试。|
|IncorrectDiskStatus|The current disk status does not support this operation.|403|磁盘必须处于**使用中**（`In_use`）的状态。|
|IncorrectDiskStatus.CreatingSnapshot|A previous snapshot creation is in process.|403|指定的磁盘正在创建快照。请稍后再试。|
|IncorrectDiskStatus.NeverAttached|The specified disk has never been attached to any instance.|403|磁盘必须已经挂载到实例上。|
|IncorrectDiskStatus.NeverUsed|The specified disk has never been used after creating.|403|该磁盘未被使用，不能创建快照。|
|InstanceLockedForSecurity|The disk attached instance is locked due to security.|403|指定的实例被安全锁定。|
|InvalidAccountStatus.NotEnoughBalance|Your account does not have enough balance.|403|您的账户余额不足。请[充值](https://help.aliyun.com/document_detail/37107.html)后重试。|
|InvalidAccountStatus.SnapshotServiceUnavailable|Snapshot service has not been opened yet.|403|您还未开通快照服务。请[提交工单](https://workorder-intl.console.aliyun.com/#/ticket/createIndex) 申请开通。|
|QuotaExceed.Snapshot|The maximum number of snapshots is exceeded.|403|您已超出能创建的最大快照数量。一块磁盘最多能创建64份快照。|
|InvalidDescription.Malformed|The specified description is wrongly formed.|404|指定的参数`Description`不合法。|
|InvalidDiskId.NotFound|The specified DiskId does not exist.|404|指定的磁盘不存在。|

