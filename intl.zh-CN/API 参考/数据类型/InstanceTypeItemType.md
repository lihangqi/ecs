# InstanceTypeItemType {#InstanceTypeItemType .reference}

实例资源规格项的类型。

## 节点名 {#section_xbl_5lp_ydb .section}

InstanceType

## 子节点 {#ResponseParameter .section}

|名称|类型|描述|
|:-|:-|:-|
|InstanceTypeId|String|实例规格 ID|
|CpuCoreCount|Integer|vCPU 内核数目|
|MemorySize|Double|内存大小，单位 GiB|
|InstanceTypeFamily|String|实例规格族|
|GPUAmount|Integer|实例规格附带 GPU 数量|
|GPUSpec|String|实例规格附带 GPU 类型|
|InstanceFamilyLevel|String|实例规格级别。可能值：-   EntryLevel：入门级
-   EnterpriseLevel：企业级
-   CreditEntryLevel：积分入门级，特指 [基本概念](../../../../intl.zh-CN/产品简介/实例/突发性能实例/基本概念.md#)

|
|BaselineCredit|Integer|突发性能实例基准 vCPU 计算性能（多核和）|
|EniQuantity|Integer|实例规格支持网卡数量|
|LocalStorageCapacity|Long|实例挂载的本地存储的单盘容量|
|LocalStorageAmount|Integer|实例挂载的本地存储的数量|
|LocalStorageCategory|String|实例挂载的本地存储的类型|

