# EipAddressAssociateType {#EipAddressAssociateType .reference}

包含弹性公网 IP 绑定信息的类型。

## 节点名 {#section_tvf_sjp_ydb .section}

接口决定。

## 子节点 {#ResponseParameter .section}

|名称|类型|描述|
|:-|:-|:-|
|AllocationId|String|弹性公网 IP 绑定的实例 ID。|
|IpAddress|String|弹性公网 IP。|
|Bandwidth|Integer|弹性公网 IP 的公网带宽限速，单位为 Mbps。默认值：5。

|
|InternetChargeType|String|弹性公网 IP 的计费方式。|
|IsSupportUnassociate|Boolean|是否可以解绑弹性公网 IP。|

