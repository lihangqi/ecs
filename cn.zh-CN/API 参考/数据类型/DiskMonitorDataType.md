# DiskMonitorDataType {#DiskMonitorDataType .reference}

包含磁盘监控数据的类型。

## 节点名 {#section_pf3_fjp_ydb .section}

DiskMonitorData

## 子节点 {#ResponseParameter .section}

|名称|类型|描述|
|:-|:-|:-|
|DiskId|String|磁盘编号|
|BPSRead|Integer|磁盘读带宽，单位：Byte/s|
|BPSWrite|Integer|磁盘写带宽，单位：Byte/s|
|BPSTotal|Integer|磁盘读写总带宽，单位：Byte/s|
|IOPSRead|Integer|磁盘IO读操作，单位：次/s|
|IOPSWrite|Integer|磁盘IO写操作，单位：次/s|
|IOPSTotal|Integer|磁盘IO读写总操作，单位：次/s|
|LatencyRead|Integer|磁盘读延时，单位：Byte/s|
|LatencyWrite|Integer|磁盘写延时，单位：Byte/s|
|TimeStamp|String|查询的时间点，按照 [ISO8601](intl.zh-CN/API参考/附录/时间格式.md#) 标准表示，并使用 UTC 时间。格式为 YYYY-MM-DDThh:mmZ。|

