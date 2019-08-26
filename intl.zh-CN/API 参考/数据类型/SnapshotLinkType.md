# SnapshotLinkType {#SnapshotLinkType .reference}

快照链详情的数据类型。

## 节点名 {#section_qtj_3rp_ydb .section}

由接口决定。

## 子节点 {#ResponseParameter .section}

|名称|类型|描述|
|:-|:-|:-|
|SnapshotLinkId|String|快照链 ID|
|RegionId|String|快照链所属的地域 ID|
|SourceDiskId|String|源磁盘 ID，如果快照的源磁盘已经被删除，该字段仍旧保留|
|SourceDiskSize|Integer|源磁盘容量，单位为 GB|
|TotalSize|Integer|快照链中所有快照的大小，单位为 Byte|
|TotalCount|Integer|快照链中所有快照的数量|
|CreationTime|String|快照链创建时间，按照 [ISO8601](cn.zh-CN/API 参考/附录/时间格式.md#) 标准表示，并需要使用 UTC 时间，格式为 YYYY-MM-DDThh:mmZ|

