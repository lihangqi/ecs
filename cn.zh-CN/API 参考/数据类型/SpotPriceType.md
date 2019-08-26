# SpotPriceType {#SpotPriceType .reference}

抢占式实例价格的属性集。

## 节点名 {#section_wky_fk5_ydb .section}

价格对象。

## 子节点 {#ResponseParameter .section}

|名称|类型|描述|
|:-|:-|:-|
|ZoneId|String|抢占式实例所属的可用区 ID|
|NetworkType|String|抢占式实例的网络类型|
|InstanceType|String|抢占式实例的实例规格|
|IoOptimized|String|抢占式实例是否为 I/O 优化实例|
|SpotPrice|Float|抢占式实例价格|
|OriginPrice|Float|按量付费实例部分原价|
|Timestamp|String|时间格式为 YYYY-MM-DDTHH:MM:SS 的价格时间|

