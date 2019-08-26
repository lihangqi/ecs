# OperationProgressType {#OperationProgressType .reference}

操作任务的资源操作明细。

## 节点名 {#section_unz_jnp_ydb .section}

OperationProgress

## 子节点 {#ResponseParameter .section}

|名称|类型|描述|
|:-|:-|:-|
|RelatedItemSet|[RelatedItemSetType](intl.zh-CN/API参考/数据类型/RelatedItemType.md#)|资源信息类型|
|OperationStatus|String|操作状态 可选值：-   Processing 执行中
-   Success，执行成功
-   Failed，执行失败

|
|ErrorCode|String|错误码。只有 OperationStatus 为 Failed 时才会有值，其余情况下为空。|
|ErrorMsg|String|错误信息。只有 OperationStatus 为 Failed 时才会有值，其余情况下为空。|

