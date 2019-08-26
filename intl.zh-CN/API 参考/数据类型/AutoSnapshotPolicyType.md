# AutoSnapshotPolicyType {#AutoSnapshotPolicyType .reference}

自动快照策略类型，自动快照策略的详细设置信息。

## 节点名 {#section_ybk_b2p_ydb .section}

由接口决定

## 子节点 {#ResponseParameter .section}

|名称|类型|描述|
|:-|:-|:-|
|AutoSnapshotPolicyId|String|自动快照策略ID。|
|RegionId|String|自动快照策略所属的地域 ID。|
|AutoSnapshotPolicyName|String|自动快照策略的名称。|
|TimePoints|String|指定自动快照的创建时间点。最小单位为小时，从 00:00~23:00 共 24 个时间点可选，参数为 0~23 的数字，如：1 代表在 01:00 时间点。可以选定多个时间点。 传递参数为一个带有格式的 Json Array：\[“0”, “1”, … “23”\]，最多 24 个时间点，用半角逗号字符隔开。|
|RepeatWeekdays|String|指定自动快照的重复日期。选定周一到周日中需要创建快照的日期，参数为1~7 的数字，如：1 表示周一。允许选择多个日期。 传递参数为一个带有格式的 Json Array：\[ “1”，“2”…“7”\]。|
|RetentionDays|Integer|指定自动快照的保留时间，单位为天。 -1：永久保存 1~65536：指定保存天数。|
|DiskNums|Integer|启用该策略的磁盘数量。|
|OperationLocks|[OperationLocksType](intl.zh-CN/API 参考/数据类型/OperationLocksType.md#)|快照锁定原因类型。|
|Status|String|自动快照策略状态，取值：Creating | Available。|
|CreationTime|String|创建时间。按照[ISO8601](../intl.zh-CN/API 参考/附录/时间格式.md#)标准表示，并需要使用UTC时间，格式为yyyy-MM-ddTHH:mm:ssZ。|

