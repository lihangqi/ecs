# SnapshotType {#SnapshotType .reference}

快照详情的数据类型。

## 节点名 {#section_yrq_4rp_ydb .section}

由接口确定。

## 子节点 {#ResponseParameter .section}

|名称|类型|描述|
|:-|:-|:-|
|SnapshotId|String|快照 ID。|
|SnapshotName|String|快照显示名称。如果创建时指定了快照显示名称，则返回。|
|Description|String|描述信息。|
|Encrypted|Boolean|该快照是否加密。|
|Progress|String|快照创建进度，单位为百分比。|
|SourceDiskId|String|源磁盘ID，如果快照的源磁盘已经被删除，该字段仍旧保留。|
|SourceDiskSize|Integer|源磁盘容量，单位：GB。|
|SourceDiskType|String|源磁盘属性。取值范围：-   System
-   Data

|
|ProductCode|String|从镜像市场继承的产品编号。|
|RetentionDays|Integer|自动快照保留天数。|
|RemainTime|Integer|正在创建的快照剩余完成时间，单位为秒。|
|CreationTime|String|创建时间。按照 [ISO8601](intl.zh-CN/API 参考/附录/时间格式.md#) 标准表示，并需要使用 UTC 时间。格式为：YYYY-MM-DDThh:mmZ|
|Status|String|快照状态。取值范围：-   progressing
-   accomplished
-   failed

|
|Usage|String|有引用关系的资源类型。取值范围：-   image
-   disk
-   image\_disk
-   none

|

