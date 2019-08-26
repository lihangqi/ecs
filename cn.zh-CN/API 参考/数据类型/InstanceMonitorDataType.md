# InstanceMonitorDataType {#InstanceMonitorDataType .reference}

实例的监控数据集合。

## 节点名 {#section_tlx_qkp_ydb .section}

InstanceMonitorData

## 子节点 {#ResponseParameter .section}

|名称|类型|描述|
|:-|:-|:-|
|InstanceId|String|实例 ID。|
|CPU|Integer|实例 vCPU 的使用比例，单位：百分比（%）|
|IntranetRX|Integer|实例在 `TimeStamp` 时刻接收的内网数据流量，单位：kbits|
|IntranetTX|Integer|实例在 `TimeStamp` 时刻发送的内网数据流量，单位：kbits|
|IntranetBandwidth|Integer|实例的内网带宽，单位时间内的网络流量，单位：kbits/s|
|InternetRX|Integer|实例在 `TimeStamp` 时刻接收的公网数据流量，单位：kbits|
|InternetTX|Integer|实例在 `TimeStamp` 时刻发送的公网数据流量，单位：kbits|
|InternetBandwidth|Integer|实例的公网带宽，单位时间内的网络流量，单位：kbits/s|
|IOPSRead|Integer|实例系统盘 I/O 读操作，单位：次/s|
|IOPSWrite|Integer|实例系统盘 I/O 写操作，单位：次/s|
|BPSRead|Integer|实例系统盘读带宽，单位：Byte/s|
|BPSWrite|Integer|实例系统盘写带宽，单位：Byte/s|
|TimeStamp|String|查询监控信息的时间戳。按照 [ISO8601](cn.zh-CN/API 参考/附录/时间格式.md#) 标准表示，并使用 UTC 时间，格式为 YYYY-MM-DDThh:mmZ|

