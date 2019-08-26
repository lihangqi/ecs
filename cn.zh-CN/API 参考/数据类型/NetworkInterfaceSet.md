# NetworkInterfaceSet {#NetworkInterfaceSet .reference}

弹性网卡（ENI）集合的数据类型。

## 节点名 {#section_r2k_5tp_ydb .section}

由接口确定。

## 子节点 {#ResponseParameter .section}

|名称|类型|描述|
|:-|:-|:-|
|NetworkInterfaceId|String|弹性网卡 ID|
|Status|String|弹性网卡的状态|
|Type|String|弹性网卡类型|
|VpcId|String|VPC ID|
|VSwitchId|String|指定 VPC 的交换机 ID|
|ZoneId|String|可用区的 ID|
|AssociatedPublicIp|[AssociatedPublicIp](intl.zh-CN/API参考/数据类型/AssociatedPublicIp.md#)|弹性网卡关联的公网 IP|
|PrivateIpAddress|String|弹性网卡主私有 IP 地址|
|PrivateIpSet|[PrivateIpSet](intl.zh-CN/API参考/数据类型/PrivateIpSet.md#)|PrivateIp 组成的集合|
|MacAddress|String|弹性网卡的 MAC 地址|
|SecurityGroupIds|[SecurityGroupIdSetType](intl.zh-CN/API参考/数据类型/SecurityGroupIdSetType.md#)|所属的安全组集合|
|NetworkInterfaceName|String|弹性网卡的名称|
|Description|String|弹性网卡描述信息|
|InstanceId|String|弹性网卡附加的实例 ID|
|CreationTime|String|创建时间。按照 [ISO8601](intl.zh-CN/API参考/附录/时间格式.md#) 标准表示，并需要使用 UTC 时间。 格式为：YYYY-MM-DDThh:mmZ|

