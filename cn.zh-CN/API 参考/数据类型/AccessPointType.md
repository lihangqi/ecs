# AccessPointType {#AccessPointType .reference}

接入点信息的类型。

## 节点名 {#section_vk3_ldp_ydb .section}

接口决定

## 子节点 {#ResponseParameter .section}

|名称|类型|描述|
|:-|:-|:-|
|AccessPointId|String|接入点（AP）ID|
|Type|String|专线接入点（AP）类型，可选值：-   VPC：VPC接入点，可接受访问VPC类型网络的专线接入

|
|Status|String|专线接入点状态，可选值：-   Recommended：状态良好，推荐接入
-   Hot：接入客户较多，状态正常
-   Full ：接入客户已满，无法接入

|
|Name|String|专线接入点（AP）的名称|
|Description|String|专线接入点（AP）的描述|
|AttachedRegionId|String|接入点物理上所在的Region ID，不填表示接入点物理上不属于任何地域|
|Location|String|专线接入点（AP）所处物理位置|
|HostOperator|String|专线接入点（AP）机房所属的运营商|

