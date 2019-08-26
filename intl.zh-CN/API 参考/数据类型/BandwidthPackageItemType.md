# BandwidthPackageItemType {#BandwidthPackageItemType .reference}

共享带宽包描述信息。

## 节点名 {#section_qvm_tfp_ydb .section}

接口决定

## 子节点 {#ResponseParameter .section}

|名称|类型|描述|
|:-|:-|:-|
|BandwidthPackageId|String|BandwidthPackage的ID，例如 bwp-xxoo123。|
|RegionId|String|地域 ID。|
|Name|String|实例的显示名称，\[2, 128\] 英文或中文字符，必须以大小字母或中文开头，可包含数字，“.”，“:”，“\_”或“-”。不能以 http:// 和 https:// 开头。|
|Description|String|自定义描述\[\[2, 256\] 个字符，实例描述会显示在控制台。不填则为空，默认为空。不能以 http:// 和 https:// 开头。|
|ZoneId|String|可用区。|
|GatewayId|String|依附的NAT网关的ID。|
|Bandwidth|String|带宽值；取值范围5-5000，单位为Mbps。|
|InstanceChargeType|String|实例的付费方式。目前仅支持按量付费.取值：PostPaid：后付费，即按量付费。|
|InternetChargeType|String|网络计费类型，PayByBandwidth |PayByTraffic两个值中的一个。目前仅支持按带宽计费。PayByTraffic：按流量计费

PayByBandwidth：按带宽计费

|
|ISP|string|目前只支持 BGP。|
|PublicIpAddresses|PublicIpAddressSetType|IP列表；每个IP有一个全局唯一的AllocatedId属性和一个IP地址属性。|
|BusinessStatus|string|Normal（正常）、FinancialLocked（欠费锁定状态）、

SecurityLocked（安全风控锁定状态）|
|CreationTime|String|创建时间。按照ISO8601标准表示，并需要使用UTC时间。格式为：YYYY-MM-DDThh:mmZ。|

