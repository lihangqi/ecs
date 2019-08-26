# PermissionType {#PermissionType .reference}

安全组规则类型。

## 节点名 {#section_gq4_b4p_ydb .section}

Permission

## 子节点 {#ResponseParameter .section}

|名称|类型|描述|
|:-|:-|:-|
|IpProtocol|String|IP协议|
|PortRange|String|端口范围|
|SourceCidrIp|String|源IP地址段，用于入方向授权|
|SourceGroupId|String|源安全组，用于入方向授权|
|SourceGroupOwnerAccount|String|源安全组所属阿里云账户Id|
|DestCidrIp|String|目标IP地址段，用于出方向授权|
|DestGroupId|String|目标安全组，用于出方向授权|
|DestGroupOwnerAccount|String|目标安全组所属阿里云账户Id|
|Policy|String|授权策略|
|NicType|String|网络类型|
|Priority|String|规则优先级|
|Direction|String|授权方向|
|Description|String|描述信息|
|CreateTime|String|创建时间，UTC时间|

