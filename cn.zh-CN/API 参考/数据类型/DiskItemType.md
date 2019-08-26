# DiskItemType {#DiskItemType .reference}

列举磁盘信息项的类型。

## 节点名 {#section_h34_v3p_ydb .section}

Disk

## 子节点 {#ResponseParameter .section}

|名称|类型|描述|
|:-|:-|:-|
|DiskId|String|磁盘 ID。|
|RegionId|String|磁盘所属的地域 ID。|
|ZoneId|String|磁盘所属的可用区 ID。|
|DiskName|String|磁盘名。|
|Description|String|磁盘描述。|
|Type|String|磁盘类型。取值范围：-   system: 系统盘
-   data: 数据盘

|
|Category|String|磁盘种类。取值范围：-   cloud: 普通云盘
-   cloud\_efficiency：高效云盘
-   cloud\_ssd：SSD云盘
-   ephemeral\_ssd: 本地 SSD 盘
-   ephemeral: 本地磁盘

|
|Encrypted|Boolean|是否为加密磁盘。取值范围：-   true: 是加密磁盘。
-   false：不是加密磁盘。

|
|Size|Integer|磁盘大小，单位 GB。|
|ImageId|String|创建磁盘的镜像 ID，只有通过镜像创建的磁盘才有值，否则为空。这个值在磁盘的生命周期内始终不变。|
|SourceSnapshotId|String|创建磁盘使用的快照，如果创建磁盘时，没有指定快照，则为空。这个值在磁盘的生命周期内始终不变。|
|ProductCode|String|云市场的商品标识。|
|IOPSRead|String|每秒读操作的次数，单位：次/s。|
|IOPSWrite|String|每秒写操作的次数，单位：次/s。|
|IOPS|String|每秒读写（I/O）操作的次数，单位：次/s。|
|Portable|String|磁盘是否可卸载。取值范围：-   true：独立普通云盘，可以独立存在且可以自由在可用区内挂载和卸载。
-   false：非独立普通云盘，不可以独立存在，不可以在可用区内挂载和卸载，生命周期与实例等同。

`Portable` 属性为 `true` 的磁盘才能挂载（[AttachDisk](intl.zh-CN/API参考/磁盘/AttachDisk.md#)）或卸载（[DetachDisk](intl.zh-CN/API参考/磁盘/DetachDisk.md#)）。`Portable` 属性为 `false` 的磁盘包括本地磁盘、本地 SSD 盘、普通云盘、SSD 盘的系统盘和包年包月的普通云盘。不支持修改该属性。|
|Status|String|磁盘状态。取值范围：-   In\_use
-   Available
-   Attaching
-   Detaching
-   Creating
-   ReIniting

|
|OperationLocks|OperationLocksType|磁盘锁定原因类型。|
|InstanceId|String|磁盘挂载的实例 ID。只有在 `Status` 为 `In_use` 时才有值，其他状态为空。|
|Device|String|磁盘挂载的实例的设备名，例如 /dev/xvdb。只有在 `Status` 为 `In_use` 时才有值，其他状态为空。|
|DeleteWithInstance|String|是否随实例释放。取值范围：-   true：释放实例时，这块磁盘随实例一起释放。
-   false：释放实例时，这块磁盘保留不释放。

|
|DeleteAutoSnapshot|String|是否同时删除自动快照。取值范围：-   true：删除磁盘上的快照。
-   false：保留磁盘上的快照。

通过 [CreateSnapshot](intl.zh-CN/API参考/快照/CreateSnapshot.md#) 或者在控制台创建的快照，不受这个参数的影响，会始终保留。|
|EnableAutoSnapshot|String|磁盘是否执行自动快照策略。取值范围：-   true：这块磁盘执行自动快照策略。
-   false：这块磁盘不执行自动快照策略。

默认值：false|
|CreationTime|String|创建时间。按照 [ISO8601](intl.zh-CN/API参考/附录/时间格式.md#) 标准表示，并需要使用 UTC时间。格式为 YYYY-MM-DDThh:mmZ。|
|AttachedTime|String|挂载时间。按照 [ISO8601](intl.zh-CN/API参考/附录/时间格式.md#) 标准表示，并需要使用 UTC时间。格式为 YYYY-MM-DDThh:mmZ只有在 `Status` 为 `In_use` 时才有意义。|
|DetachedTime|String|卸载时间。按照 [ISO8601](intl.zh-CN/API参考/附录/时间格式.md#) 标准表示，并需要使用 UTC 时间。格式为：YYYY-MM-DDThh:mmZ只有在`Status` 为 `Available` 时才有意义。|
|DiskChargeType|String|磁盘的付费方式。取值范围：-   PrePaid：预付费，即包年包月。
-   PostPaid：后付费，即按量付费。

|

