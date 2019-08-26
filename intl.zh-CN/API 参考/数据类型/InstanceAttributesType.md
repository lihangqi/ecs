# InstanceAttributesType {#InstanceAttributesType .reference}

云服务器 ECS 实例属性的数据类型。

## 节点名 {#section_nhx_2kp_ydb .section}

由接口决定。

## 子节点 {#ResponseParameter .section}

|名称|类型|描述|
|:-|:-|:-|
|InstanceId|String|实例 ID|
|InstanceName|String|实例名称|
|Description|String|实例描述|
|ImageId|String|实例运行的镜像 ID|
|RegionId|String|实例所属地域 ID|
|ZoneId|String|实例所属可用区|
|Cpu|Integer|vCPU 核数|
|GPUSpec|String|实例规格附带的 GPU 类型|
|GPUAmount|Integer|实例规格附带的 GPU 数量|
|Memory|Float|内存大小，单位 GiB|
|InstanceType|String|实例资源规格|
|InstanceTypeFamily|String|实例规格族|
|HostName|String|实例主机名|
|SerialNumber|String|实例序列号|
|Status|String|实例状态|
|SecurityGroupIds|[SecurityGroupIdSetType](intl.zh-CN/API 参考/数据类型/SecurityGroupIdSetType.md#)|实例所属安全组集合|
|PublicIpAddress|[IpAddressSetType](intl.zh-CN/API 参考/数据类型/IpAddressSetType.md#)|实例公网 IP 地址|
|InternetMaxBandwidthIn|Integer|公网入带宽最大值|
|InternetMaxBandwidthOut|Integer|公网出带宽最大值|
|InternetChargeType|String|网络计费类型。可能值：-   PayByTraffic：按流量计费

|
|CreationTime|String|实例创建时间。按照[ISO8601](../intl.zh-CN/API 参考/附录/时间格式.md#)标准表示，并需要使用UTC时间，格式为yyyy-MM-ddTHH:mm:ssZ。|
|InstanceNetworkType|String|实例网络类型。可能值：-   Classic
-   Vpc

|
|VpcAttributes|[VpcAttributesType](intl.zh-CN/API 参考/数据类型/VpcAttributesType.md#)|专有网络 VPC 属性|
|EipAddress|[EipAddressAssociateType](intl.zh-CN/API 参考/数据类型/EipAddressAssociateType.md#)|弹性公网 IP 绑定信息|
|InnerIpAddress|[IpAddressSetType](intl.zh-CN/API 参考/数据类型/IpAddressSetType.md#)|实例的内网 IP 地址|
|OperationLocks|[OperationLocksType](intl.zh-CN/API 参考/数据类型/OperationLocksType.md#)|实例的锁定原因|
|InstanceChargeType|String|实例的计费方式。可能值：-   PrePaid：预付费（包年包月 ）
-   PostPaid：按量付费

|
|SaleCycle|String|当实例为预付费实例时，实例购买的周期单位。取值范围：week | month | year|
|SpotPriceLimit|Float|设置实例的每小时最高价格。支持最大3位小数，参数`SpotStrategy=SpotWithPriceLimit`时，该参数生效。|
|SpotStrategy|String|抢占式实例的抢占策略。可能值：-   NoSpot：正常按量付费实例
-   SpotWithPriceLimit：设置上限价格的抢占式实例
-   SpotAsPriceGo：系统自动出价，最高按量付费价格

默认值：NoSpot|
|DeviceAvailable|Boolean|实例是否还可以挂载数据盘|
|StoppedMode|String|实例停机后是否继续收费。可能值：-   KeepCharging：停机后继续收费，为您继续保留库存资源。
-   StopCharging：停机后不收费。停机后，我们释放实例对应的资源，例如 vCPU、内存和公网 IP 等资源。重启是否成功依赖于当前地域中是否仍有资源库存。
-   Not-applicable：本实例支持停机不收费功能。

|
|DeploymentSetId|String|部署集 ID|
|NetworkInterfaces|[NetworkInterfaceType](intl.zh-CN/API 参考/数据类型/NetworkInterfaceType.md#)|实例包含的弹性网卡集合|
|IoOptimized|Boolean|是否为 I/O 优化型实例|
|ExpiredTime|String|过期时间。按照[ISO8601](../intl.zh-CN/API 参考/附录/时间格式.md#)标准表示，并需要使用UTC时间，格式为yyyy-MM-ddTHH:mm:ssZ。|
|KeyPairName|String|密钥对名称|

