# AutoSnapshotExecutionStatusType {#AutoSnapshotExecutionStatusType .reference}

自动快照执行状态类型，返回上一次的执行结果。

## 节点名 {#section_t2z_j2p_ydb .section}

接口决定

## 子节点 {#ResponseParameter .section}

|名称|类型|描述|
|:-|:-|:-|
|SystemDiskExecutionStatus|String|返回最近一次执行的状态，取值：Standby | Executed | Failed-   Standby：刚设置完成还未开始执行或者系统盘的策略被关闭
-   Executed：执行成功
-   Failed：执行失败

|
|DataDiskExecutionStatus|String|返回最近一次执行的状态，取值：Standby | Executed | Failed-   Standby：刚设置完成还未开始执行或者数据盘的策略被关闭
-   Executed：执行成功
-   Failed：执行失败

|

