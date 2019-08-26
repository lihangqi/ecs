# OperationLocksType {#OperationLocksType .reference}

资源的锁定原因类型。

## 节点名 {#section_yj4_1np_ydb .section}

OperationLock

## 子节点 {#ResponseParameter .section}

|名称|类型|描述|
|:-|:-|:-|
|LockReason|String|锁定类型-   financial：因欠费被锁定
-   security：因安全原因被锁定
-   recycling：抢占式实例的待释放锁定状态

|

