# AvailableResourcesType {#AvailableResourcesType .reference}

支持创建的资源类型。

## 节点名 {#section_qyr_mfp_ydb .section}

由接口决定。

## 子节点 {#ResponseParameter .section}

|名称|类型|描述|
|:-|:-|:-|
|IoOptimized|String|是否 I/O 优化|
|supportedNetworkCategory|String|支持的网络类型|
|supportedInstanceGeneration|Array|支持的实例系列|
|supportedInstanceTypeFamily|Array|支持的实例规格族|
|supportedSystemDiskCategory|Array|支持创建的系统盘类型组成的数组|
|supportedDataDiskCategory|Array|支持创建的数据盘类型组成的数组|
|supportedInstanceType|Array|支持创建的实例规格组成的数组|

