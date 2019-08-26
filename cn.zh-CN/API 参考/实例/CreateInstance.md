# CreateInstance {#CreateInstance .reference}

创建一台ECS实例。

## 描述 {#section_nnh_jcy_wdb .section}

创建一台实例前，您可以调用 [DescribeAvailableResource](intl.zh-CN/API 参考/地域/DescribeAvailableResource.md#) 查看指定地域或者可用区内的实例资源供给情况。

创建实例会涉及到资源计费，建议您提前了解云服务器ECS的计费方式。更多详情，请参阅[计费概述](../intl.zh-CN/产品定价/计费概述.md#)。若实例付费类型为预付费的包年包月实例（`PrePaid`），则在付款时默认会使用您可用的优惠券。

根据请求参数创建实例时，您需要注意以下几类请求参数的使用说明。

**实例规格**

-   创建实例时，可以通过参数 `IoOptimized` 指定是否创建I/O优化实例。
-   如果选择创建本地SSD盘（`ephemeral_ssd`）的实例，一旦创建就不能修改实例规格。

**镜像**

在创建实例时，必须要选择镜像，确定新创建实例的系统盘配置。基于镜像创建实例后，实例的系统盘即为此镜像的完全克隆。

-   实例内存为512 MiB时不能使用Windows镜像。

-   实例内存为4 GiB以上时不能使用32位操作系统的镜像。


**网络配置**

-   专有网络VPC类型实例只能在创建时指定，必须且只能属于一个交换机。

-   指定 `VSwitchId` 时，`SecurityGroupId` 和 `VSwitchId` 要属于同一个VPC。

-   `VSwitchId` 和 `PrivateIpAddress` 同时指定时，`PrivateIpAddress` 要包含在交换机的CidrBlock之内。

-   `PrivateIpAddress` 依赖于 `VSwitchId`，不能单独指定 `PrivateIpAddress`。

-   使用本接口创建的实例将不会分配公网IP，您可以调用 [AllocatePublicIpAddress](intl.zh-CN/API 参考/网络/AllocatePublicIpAddress.md#) 分配公网IP。

-   在创建实例时，`InternetChargeType` 和 `InternetMaxBandwidthOut` 的设置决定可能发生的带宽费用。`InternetMaxBandwidthIn` 的值在任何情况下都与计费无关，实例的入数据流量是免费的。

-   参数 `InternetChargeType` 与 `InternetMaxBandwidthOut` 之间的关系如下表所示。

    |参数|InternetChargeType|InternetMaxBandwidthOut|
    |:-|:-----------------|:----------------------|
    |参数取值|`PayByTraffic`|按使用流量付费。带宽的上限设置，计费以实际使用的网络流量为依据。|


**安全组**

-   安全组需要预先创建，可通过 [CreateSecurityGroup](intl.zh-CN/API 参考/安全组/CreateSecurityGroup.md#) 创建。

-   可以在新创建实例时指定安全组，也可通过 [ModifyInstanceAttribute](intl.zh-CN/API 参考/实例/ModifyInstanceAttribute.md#) 的接口变更实例所属安全组。

-   在同一个安全组内的实例内网可以相互访问。不同安全组之间默认隔离，不可相互访问，但是可以授权访问。更多详情，请参阅 [AuthorizeSecurityGroup](intl.zh-CN/API 参考/安全组/AuthorizeSecurityGroup.md#) 和 [AuthorizeSecurityGroupEgress](intl.zh-CN/API 参考/安全组/AuthorizeSecurityGroupEgress.md#)。

-   同一个安全组内的实例数量不能超过1000台。


**存储**

-   不同类型云盘的最大容量不同：

    -   单块普通云盘（`cloud`）容量最大不能超过2000 GiB。

    -   单块高效云盘（`cloud_efficiency`）容量最大不超过32 TiB（32768 GiB）。

    -   单块SSD云盘（`cloud_ssd`）容量最大不能超过32 TiB（32768 GiB）。

    -   单块本地SSD盘（`ephemeral_ssd`）容量最大不能超过800 GiB。

-   创建实例时，我们根据您指定的镜像为实例分配一个相应大小的系统盘。系统盘容量必须大于或者等于max\{20, ImageSize\}。系统盘的种类有普通云盘（`cloud`）、高效云盘（`cloud_efficiency`）、SSD云盘（`cloud_ssd`）、和本地SSD盘（`ephemeral_ssd`）。

-   当系统盘是普通云盘（`cloud`）、高效云盘（`cloud_efficiency`）或SSD云盘（`cloud_ssd`）时，数据盘不能是本地SSD盘 `ephemeral_ssd`。

-   当实例选择为I/O优化实例时，系统盘只能选择高效云盘（`cloud_efficiency`）及SSD云盘（`cloud_ssd`）。

-   一个实例最多添加16块数据盘。数据盘挂载点由系统默认顺序分配，/dev/xvdb开始到/dev/xvdz。数据盘选择本地SSD盘 `ephemeral_ssd` 时，系统盘必须为本地SSD盘，同时一个实例的本地SSD盘总容量不超过1 TiB（1024 GiB，不包括系统盘）。

-   本地SSD盘 `ephemeral_ssd` 必须在创建实例时指定，实例创建完成后不能再添加。更多详情，请参阅 [实例规格族](../intl.zh-CN/产品简介/实例规格族.md#)。


**自定义数据**

若实例满足使用 [实例自定义数据](../intl.zh-CN/用户指南/实例/实例自定义数据和元数据/实例自定义数据.md#) 的限制，您可传入UserData信息。UserData以Base64的方式编码。UserData将以不加密的方式传入，不要以明文方式传入机密的信息，例如密码和私钥等。如果必须传入，建议加密后，然后以Base64的方式编码后再传入，在实例内部以同样的方式反解密。

**其他**

在阿里云CLI及SDK中使用API时，部分带点号（.）的入参需要去掉点号（.）再使用，包括：`SystemDisk.Category`、`SystemDisk.Size`、`SystemDisk.Description`、`DataDisk.n.Size`、`DataDisk.n.Category`、`DataDisk.n.SnapshotId`、`DataDisk.n.DiskName`、`DataDisk.n.Description`、`DataDisk.n.DeleteWithInstance`。

例如，在 阿里云[CLI](https://www.alibabacloud.com/help/doc-detail/29993.htm)  及 [SDK](https://github.com/aliyun) 中使用 `SystemDiskCategory` 表示入参 `SystemDisk.Category`。

## 请求参数 {#section_cx1_3cy_wdb .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：CreateInstance|
|RegionId|String|是|实例所属的地域ID。您可以调用[DescribeRegions](../intl.zh-CN/API 参考/地域/DescribeRegions.md#)查看最新的阿里云地域列表。|
|ImageId|String|是|镜像文件ID，启动实例时选择的镜像资源。如需使用云市场镜像，您可以在云市场镜像商详情页查看ImageId。|
|InstanceType|String|是|实例的资源规格。更多详情，请参阅 [实例规格族](../intl.zh-CN/产品简介/实例规格族.md#)，也可以调用 [DescribeInstanceTypes](intl.zh-CN/API 参考/实例/DescribeInstanceTypes.md#) 接口获得最新的规格表。|
|CreditSpecification|String|否| 修改突发性能 t5 实例的运行模式。取值范围：

 -   Standard：标准模式，实例性能请参阅 [t5性能约束实例](../intl.zh-CN/产品简介/实例/突发性能实例/t5性能约束实例.md#)。
-   Unlimited：无性能约束模式，实例性能请参阅 [t5无性能约束实例](../intl.zh-CN/产品简介/实例/突发性能实例/t5无性能约束实例.md#)。

 默认值：无。

 |
|SecurityGroupId|String|是|指定新创建实例所属于的安全组代码，同一个安全组内的实例之间可以互相访问。|
|ZoneId|String|否|实例所属的可用区编号。更多详情，请参阅 [DescribeZones](intl.zh-CN/API 参考/地域/DescribeZones.md#) 获取可用区列表。空表示由系统选择，默认值：空。

|
|InstanceName|String|否|实例的名称。长度为 \[2, 128\] 个英文或中文字符。必须以大小字母或中文开头，不能以 http:// 和 https:// 开头。可以包含数字、半角冒号（:）、下划线（\_）或者连字符（-）。如果没有指定该参数，默认值为实例的InstanceId。

|
|Description|String|否|实例的描述。长度为 \[2, 256\] 个英文或中文字符，不能以 http:// 和 https:// 开头。默认值：空。

|
|DedicatedHostId|String|否| 是否在专有宿主机上创建 ECS 实例。您可以通过[DescribeDedicatedHosts](intl.zh-CN/API 参考/专有宿主机/DescribeDedicatedHosts.md#) 查询专有宿主机 ID 列表。

 由于专有宿主机不支持创建抢占式实例，指定 DedicatedHostId 参数后，会自动忽略请求中的 SpotStrategy 和 SpotPriceLimit 设置。

 |
|InternetChargeType|String|否|网络计费类型。取值范围：-   PayByTraffic：按使用流量计费

默认值：PayByTraffic|
|InternetMaxBandwidthIn|String|否|公网入带宽最大值，单位为Mbit/s。取值范围：\[1,200\] 默认值：200

|
|InternetMaxBandwidthOut|String|否|公网出带宽最大值，单位为Mbit/s。取值范围：\[0, 100\]默认值：0

|
|HostName|String|否|云服务器的主机名。-   点号（.）和短横线（-）不能作为首尾字符，更不能连续使用。
-   Windows 实例：字符长度为 \[2, 15\]，不支持点号（.），不能全是数字。允许大小写英文字母、数字和短横线（-）。
-   其他类型实例（Linux 等）：字符长度为 \[2, 64\]，支持多个点号（.），点之间为一段，每段允许大小写英文字母、数字和短横线（-）。

|
|Password|String|否|实例的密码。长度为 8 至 30 个字符，必须同时包含大小写英文字母、数字和特殊符号。特殊符号可以是\(\)\` ~!@\#$%^&\*-+=|\{\}\[\]:;‘<\>,.?/。其中，Windows 实例不能以斜线号（/）为密码首字符。**说明：** 如果传入`Password`参数，建议您使用HTTPS协议发送请求，避免密码泄露。

|
|PasswordInherit|Boolean|否|是否使用镜像预设的密码。使用该参数时，`Password`参数必须为空，同时您需要确保使用的镜像已经设置了密码。|
|IoOptimized|String|否|是否为I/O优化实例。取值范围：-   none：非I/O优化
-   optimized：I/O优化

[已停售的实例规格](https://www.alibabacloud.com/help/faq-detail/55263.htm) 实例默认值：none其他实例规格默认值：optimized

|
|SystemDisk.Category|String|否|系统盘的磁盘种类。取值范围：-   cloud：普通云盘
-   cloud\_efficiency：高效云盘
-   cloud\_ssd：SSD 云盘
-   ephemeral\_ssd：本地 SSD 盘

[已停售的实例规格](https://www.alibabacloud.com/help/faq-detail/55263.htm)且非 I/O 优化实例默认值：cloud否则，默认值：cloud\_efficiency

|
|SystemDisk.Size|Integer|否|系统盘大小，单位为GiB。取值范围：\[20, 500\]该参数的取值必须大于或者等于max\{20, ImageSize\}。

默认值：max\{40, ImageSize\}

|
|SystemDisk.DiskName|String|否|系统盘名称。长度为 \[2, 128\] 个英文或中文字符。必须以大小字母或中文开头，不能以 http:// 和 https:// 开头。可以包含数字、半角冒号（:）、下划线（\_）或者连字符（-）。默认值：空。

|
|SystemDisk.Description|String|否|系统盘描述。长度为 \[2, 256\] 个英文或中文字符，不能以 http:// 和 https:// 开头。默认值：空。

|
|DataDisk.n.Size|Integer|否|第n个数据盘的容量大小，n的取值范围为\[1, 16\]，内存单位为 GiB。取值范围：-   cloud：\[5, 2000\]
-   cloud\_efficiency：\[20, 32768\]
-   cloud\_ssd：\[20, 32768\]
-   ephemeral\_ssd：\[5, 800\]

该参数的取值必须大于等于参数 `SnapshotId` 指定的快照的大小。|
|DataDisk.n.Category|String|否|数据盘n的磁盘种类。取值范围：-   cloud：普通云盘
-   cloud\_efficiency：高效云盘
-   cloud\_ssd：SSD 云盘
-   ephemeral\_ssd：本地 SSD 盘

默认值：cloud|
|DataDisk.n.Encrypted|Boolean|否|数据盘n是否加密。默认值：false|
|DataDisk.n.SnapshotId|String|否|创建数据盘n使用的快照。 指定参数`DataDisk.n.SnapshotId`后，参数`DataDisk.n.Size`会被忽略，实际创建的磁盘大小为参数 `SnapshotId` 的大小。若 `SnapshotId` 的创建时间早于2013年7月15日（含），该次请求会被拒绝，且返回错误 `InvalidSnapshot.TooOld`。|
|DataDisk.n.DiskName|String|否|数据盘名称。长度为 \[2, 128\] 个英文或中文字符。必须以大小字母或中文开头，不能以 http:// 和 https:// 开头。可以包含数字、半角冒号（:）、下划线（\_）或者连字符（-）。默认值：空。

|
|DataDisk.n.Description|String|否|数据盘描述。长度为 \[2, 256\] 个英文或中文字符，不能以 http:// 和 https:// 开头。默认值：空。

|
|DataDisk.n.DeleteWithInstance|Boolean|否|表示数据盘是否随实例释放。默认值：true

这个参数只对独立云盘有效，即，参数`DataDisk.n.Category` 取值为 `cloud`、`cloud_efficiency` 或 `cloud_ssd` 的云盘，否则会报错。|
|HpcClusterId|String|否|实例所属的集群ID。|
|VSwitchId|String|否|如果是创建VPC类型的实例，需要指定虚拟交换机ID。|
|PrivateIpAddress|String|否|实例私网IP地址。该IP地址必须为 `VSwitchId` 网段的子集网址。|
|InstanceChargeType|String|否|实例的付费方式。取值范围：-   PrePaid：预付费，包年包月。选择该类付费方式时，您必须确认自己的账号支持余额支付/信用支付，否则将返回 `InvalidPayMethod` 的错误提示。
-   PostPaid（默认）：按量付费。

|
|SpotStrategy|String|否|后付费实例的抢占策略。当参数 `InstanceChargeType` 取值为 `PostPaid` 时生效。取值范围：-   NoSpot（默认）：正常按量付费实例。
-   SpotWithPriceLimit：设置上限价格的抢占式实例。
-   SpotAsPriceGo：系统自动出价，跟随当前市场实际价格。

|
|SpotPriceLimit|Float|否|设置实例的每小时最高价格。支持最大3位小数，参数 `SpotStrategy` 取值为 `SpotWithPriceLimit` 时生效。|
|Period|Integer|否|购买资源的时长，单位为：月。当参数 `InstanceChargeType` 取值为 `PrePaid` 时才生效且为必选值。一旦指定了 DedicatedHostId，则取值范围不能超过专有宿主机的订阅时长。取值范围：-   `PeriodUnit=Week`时，Period取值：\{“1”, “2”, “3”, “4”\}
-   `PeriodUnit=Month`时，Period取值：\{ “1”, “2”, “3”, “4”, “5”, “6”, “7”, “8”, “9”, “12”, “24”, “36”,”48”,”60”\}

|
|PeriodUnit|String|否|购买资源的时长。可选值：Week | Month。`PeriodUnit` 为 `Week` 时：

-   Period 取值 \{“1”, “2”, “3”, “4”\}
-   AutoRenewPeriod 取值 \{“1”, “2”, “3”\}

`PeriodUnit` 为 `Month` 时：-   Period 取值 \{ “1”, “2”, “3”, “4”, “5”, “6”, “7”, “8”, “9”, “12”, “24”, “36”,”48”,”60”\}
-   AutoRenewPeriod 取值 \{“1”, “2”, “3”, “6”, “12”\}

默认值：Month|
|AutoRenew|Boolean|否|是否要自动续费。当参数 `InstanceChargeType` 取值 `PrePaid` 时才生效。取值范围：-   True：自动续费。
-   False（默认）：不自动续费。

|
|AutoRenewPeriod|Integer|否|每次自动续费的时长，当参数`AutoRenew`取值`True`时为必填。取值范围：1 | 2 | 3 | 6 |12|
|UserData|String|否|实例自定义数据，需要以Base64方式编码，原始数据最多为16KB。|
|ClientToken|String|否| 保证请求幂等性。从您的客户端生成一个参数值，确保不同请求间该参数值唯一。只支持ASCII字符，且不能超过64个字符。更多详情，请参阅[如何保证幂等性](../intl.zh-CN/API 参考/附录/如何保证幂等性.md#)。

 |
|KeyPairName|String|否|密钥对名称。-   Windows实例，忽略该参数。默认为空。即使填写了该参数，仍旧只执行 `Password` 的内容。
-   Linux实例的密码登录方式会被初始化成禁止。

|
|DeploymentSetId|String|否|部署集ID。|
|RamRoleName|String|否|实例RAM角色名称。您可以使用 *RAM* API [ListRoles](../../../../../intl.zh-CN/API参考/API 参考（RAM）/角色管理接口/ListRoles.md#) 查询实例RAM角色名称。参考相关 API [CreateRole](../../../../../intl.zh-CN/API参考/API 参考（RAM）/角色管理接口/CreateRole.md#) 和 [ListRoles](../../../../../intl.zh-CN/API参考/API 参考（RAM）/角色管理接口/ListRoles.md#) 。|
|SecurityEnhancementStrategy|String|否|是否开启安全加固。取值范围：-   Active：启用安全加固，只对系统镜像生效。
-   Deactive：不启用安全加固，对所有镜像类型生效。

|
|Tag.n.Key|String|否|实例、磁盘和主网卡的标签键。n 的取值范围：\[1, 20\]。一旦传入该值，则不允许为空字符串。最多支持 64 个字符，不能以 aliyun、acs:、http:// 或者 https:// 开头。|
|Tag.n.Value|String|否|实例、磁盘和主网卡的标签值。n的取值范围：\[1, 20\]。一旦传入该值，可以为空字符串。最多支持 128 个字符，不能以 aliyun、acs:、http:// 或者 https:// 开头。|
|DryRun|Boolean|否|是否只预检此次请求。-   true：发送检查请求，不会创建实例。检查项包括是否填写了必需参数、请求格式、业务限制和ECS库存。如果检查不通过，则返回对应错误。如果检查通过，则返回错误码`DryRunOperation`。
-   false：发送正常请求，通过检查后直接创建实例。

默认值：false

|

## 返回参数 {#section_m5f_rjm_xdb .section}

|名称|类型|描述|
|:-|:-|:-|
|InstanceId|String|实例ID，是访问实例的唯一标识。|

## 示例 {#section_y3g_sjm_xdb .section}

**请求示例**

```
https://ecs.aliyuncs.com/?Action=CreateInstance
&RegionId=cn-hangzhou
&ImageId=_32_23c472_20120822172155_aliguest.vhd
&SecurityGroupId=sg-c0003e8b9
&HostName=Bctest01
&InstanceType=ecs.t1.small
&<公共请求参数>
```

**XML示例**

```
<CreateInstanceResponse>
    <RequestId>04F0F334-1335-436C-A1D7-6C044FE73368</RequestId>
    <InstanceId>i-instance1</InstanceId>
</CreateInstanceResponse>
```

**JSON示例**

```
{
    "RequestId": "04F0F334-1335-436C-A1D7-6C044FE73368",
    "InstanceId": "i-instance1"
}
```

## 错误码 {#section_oxx_skm_xdb .section}

以下为本接口特有的错误码。更多错误码，请访问[API错误中心](https://error-center.alibabacloud.com/status/product/Ecs)。

|错误代码|错误信息|HTTP状态码|说明|
|:---|:---|:------|:-|
|Account.Arrearage|Your account has an outstanding payment.|400|账号已经欠费。|
|DryRunOperation|Request validation has been passed with DryRun flag set.|400|此次DryRun预检请求合格。|
|IncorrectVSwitchStatus|The current status of virtual switch does not support this operation.|400|指定的VSwitch状态不正确。|
|InstanceDiskCategoryLimitExceed|The specified DataDisk.n.Size beyond the permitted range, or the capacity of snapshot exceeds the size limit of the specified disk category.|400|指定的磁盘大小超过了该类型磁盘上限。|
|InstanceDiskNumber.LimitExceed|The total number of specified disk in an instance exceeds.|400|镜像中包含的数据盘和数据盘参数合并后，数据盘的总数超出限制。|
|InvalidAutoRenewPeriod.ValueNotSupported|The specified autoRenewPeriod is not valid.|400|指定的`AutoRenewPeriod`不合法。|
|InvalidDataDiskCategory.ValueNotSupported|The specified parameter DataDisk.n.Category is not valid.|400|指定的`DataDisk.n.Category`不合法。|
|InvalidDataDiskCategory.ValueNotSupported|The specified parameter DataDisk.n.Category is not valid.|400|指定的`DataDisk.n.Category`不合法。|
|InvalidDataDiskSize.ValueNotSupported|The specified DataDisk.n.Size beyond the permitted range, or the capacity of snapshot exceeds the size limit of the specified disk category.|400|指定的`DataDisk.n.Size`不合法（超出范围）。|
|InvalidDescription.Malformed|The specified parameter Description is not valid.|400|指定的`Description`格式不合法。|
|InvalidDiskCategory.Mismatch|The specified disk categories’ combination is not supported.|400|指定的磁盘类型组合不支持。|
|InvalidDiskCategory.ValueNotSupported|The specified parameter DiskCategory is not valid.|400|指定的`DiskCategory`不合法。|
|InvalidDiskDescription.Malformed|The specified parameter SystemDisk.DiskDescription or DataDisk.n.Description is not valid.|400|指定的`SystemDisk.DiskDescription`或`DataDisk.n.Description`不合法。|
|InvalidDiskDescription.Malformed|The specified parameter SystemDisk.DiskDescription or DataDisk.n.Description is not valid.|400|指定的`SystemDisk.DiskDescription`或`DataDisk.n.Description`不合法。|
|InvalidDiskName.Malformed|The specified parameter SystemDisk.DiskName or DataDisk.n.DiskName is not valid.|400|指定的`SystemDisk.DiskName`或`DataDisk.n.DiskName`不合法。|
|InvalidHostName.Malformed|The specified parameter HostName is not valid.|400|指定的`HostName`格式不合法。|
|InvalidHpcClusterId.NotFound|The specified HpcClusterId is not found.|400|指定的`HpcClusterId`不存在。|
|InvalidHpcClusterId.Creating|The specified HpcClusterId is creating.|400|指定的`HpcClusterId`正在创建中。|
|InvalidHpcClusterId.Unnecessary|The specified HpcClusterId is unnecessary.|400|只有部分实例规格 `InstanceType` 支持指定集群ID。|
|InvalidVSwitchId.Necessary|The HpcClusterId is necessary.|400|该实例规格 `InstanceType` 需要指定E-HPC集群ID，您需要传入 `HpcClusterId`。|
|InvalidInstanceName.Malformed|The specified parameter InstanceName is not valid.|400|指定的`InstanceName`格式不合法。|
|InvalidInstanceType.ValueNotSupported|The specified InstanceType beyond the permitted range.|400|指定的`InstanceType`不合法（超出可选范围）。|
|InvalidInstanceType.ValueUnauthorized|The specified InstanceType is not authorized.|400|指定的`InstanceType`未授权使用。|
|InvalidInternetChargeType.ValueNotSupported|The specified InternetChargeType is not valid.|400|指定的`InternetChargeType`不存在。|
|InvalidIoOptimizedValue.ValueNotSupported|IoOptimized value not supported.|400|指定的`IoOptimized`参数不支持。|
|InvalidIPAddress.AlreadyUsed|The specified IPAddress is already used by other resource.|400|指定的IP地址已经被使用。|
|InvalidNetworkType.Mismatch|Specified parameter InternetMaxBandwidthIn or InternetMaxBandwidthOut conflict with instance network type.|400|指定的`InternetMaxBandwidthIn`或`InternetMaxBandwidthOut`与实例网络类型不符合。|
|InvalidSpotStrategy|The specified SpotStrategy is not valid.|400|`SpotStrategy`参数不合法。|
|InvalidSpotPriceLimit|The specified SpotPriceLimitis not valid.|400|`SpotPriceLimit`参数不合法。|
|InvalidSpotAuthorized|The specified Spot param is unauthorized.|400|该账号没有授权创建抢占式实例。|
|InvalidSpotPrepaid|The specified Spot type is not support PrePay Instance.|400|抢占式支持预付费。|
|InvalidSpotPriceLimit.LowerThanPublicPrice|The specified parameter spotPriceLimit can’t be lower than current public price.|400|出价低于当前系统公允价格。|
|InvalidNetworkType.Mismatch|Specified parameter InternetChargeType conflict with instance network type.|400|指定的`InternetChargeType`与实例网络类型不符合。|
|InvalidNodeControllerId.Malformed|The specified parameter NodeControllerId is not valid.|400|指定的`NodeControllerId`不合法。|
|InvalidParameter|The specified parameter InternetMaxBandwidthOut is not valid.|400|指定的`InternetMaxBandwidthOut` 不合法（不是数字或超出范围）。|
|InvalidParameter|The specified instance bandwidth is not valid.|400|指定的带宽值不合法。|
|InvalidParameter.Bandwidth|The specified parameter Bandwidth is not valid.|400|指定的带宽值不合法。|
|EncryptedOption.Conflict|Encryption value of disk and snapshot conflict.|400|磁盘的加密属性和快照的加密属性不一致。|
|InvalidParameter.Conflict|The specified image does not support the specified instance type.|400|指定的`InstanceType`上不允许使用该指定的镜像。|
|InvalidParameter.Encrypted.KmsNotEnabled|The encrypted disk need enable KMS.|400|您未开通KMS服务。|
|InvalidParameter.EncryptedIllegal|The value of parameter Encrypted is illegal.|400|传入的参数`Encrypted`非法。|
|InvalidParameter.EncryptedNotSupported|Encrypted disk is not support in this region.|400|所选择的地域不支持加密特性。|
|InvalidParameter.EncryptedNotSupported|Corresponding data disk category does not support encryption.|400|对应的磁盘种类不支持加密。|
|InvalidParameter.Mismatch|Specified security group and virtual switch are not in the same VPC.|400|指定安全组与VSwitch不属于同一个VPC。|
|InvalidParameter.Mismatch|Specified virtual switch is not in the specified zone.|400|指定的VSwitch不在指定Zone。|
|InvalidPassword.Malformed|The specified parameter Password is not valid.|400|指定的`Password`格式不合法。|
|InvalidPrivateIpAddress|Specified private IP address is not in the CIDR block of virtual switch.|400|指定的IP不属于该VSwitch。|
|InvalidPrivateIpAddress.Duplicated|Specified private IP address is duplicated.|400|指定的`PrivateIpAddress`重复。|
|InvalidPrivateIpAddress.Malformed|Specified private IP address is malformed.|400|指定的私有IP不合法。|
|InvalidPasswordParam.Mismatch|The input password should be null when passwdInherit is true.|400|指定了`PasswdInherit`后，您不能指定`Password`参数。|
|InvalidSnapshotId.BasedSnapshotTooOld|The specified snapshot is created before 2013-07-15.|400|使用了2013年07月15日之前创建的快照。|
|InvalidSpotAliUid|The specified UID is not authorized to use SPOT instance.|400|该账号不能使用抢占式|
|InvalidSystemDiskCategory.ValueNotSupported|The specified parameter SystemDisk.Category is not valid.|400|指定的`SystemDisk.Category`不合法。|
|InvalidUserData.NotSupported|The specified parameter UserData only support the vpc and IoOptimized Instance.|400|UserData只能使用在VPC和I/O优化实例上。|
|InvalidUserData.SizeExceeded|The specified parameter UserData exceeds the size.|400|指定的UserData过长。|
|MissingParameter|The input parameter VSwitchId that is mandatory for processing this request is not supplied.|400|缺少必填参数`VSwitchId`。|
|MissingParamter|The specified parameter Period is not null.|400|参数`Period`不能为空。|
|QuotaExceed.AfterpayInstance|The maximum number of Pay-As-You-Go instances is exceeded.|400|您的按量付费实例个数达到上限。|
|QuotaExceeded|Living instances quota exceeded in this VPC.|400|VPC中实例数量超限。|
|QuotaExceeded.PrivateIpAddress|Don’t have enough private IPs in this switch.|400|私有IP数量不足。|
|ResourceNotAvailable|Resource you requested is not available in this region or zone.|400|指定的地域或可用区内该资源不可用。|
|CategoryNotSupported|The specified zone does not offer the specified disk category.|403|该可用区无权创建指定种类的磁盘。|
|DeleteWithInstance.Conflict|The specified disk is not a portable disk and cannot be set to DeleteWithInstance attribute.|403|该磁盘不支持挂载与卸载。|
|DependencyViolation.WindowsInstance|The instance creating is window, cannot use ssh key pair to login.|403|Windows实例不能使用SSH 密钥对。|
|DeploymentSet.NoRoom|There is no room for more instance creation in the specified DeploymentSet.|403|指定的`DeploymentSet`中不能创建更多的实例。|
|Forbbiden|User not authorized to operate on the specified resource.|403|您暂时无法使用该资源。|
|ImageNotSubscribed|The specified image has not be subscribed.|403|没有订阅镜像市场的镜像。|
|ImageNotSupportInstanceType|The specified image don’t support the InstanceType instance.|403|指定镜像不支持该实例类型。|
|ImageRemovedInMarket|The specified market image is not available, or the specified custom image includes product code because it is based on an image subscribed from marketplace, and that image in marketplace including exact the same product code has been removed.|403|镜像市场的镜像已下架，或者自定义镜像中包含的 product code 对应的镜像市场镜像已经下架。|
|InstanceDiskCategoryLimitExceed|The total size of specified disk category in an instance exceeds.|403|指定的磁盘种类超过了单实例的最大容量。|
|InstanceDiskNumLimitExceed|The number of specified disk in an instance exceeds.|403|指定实例已经达到可挂载磁盘的最大值。|
|InvalidDiskCategory.Mismatch|The specified disk categories combination is not supported.|403|指定的磁盘类型组合不支持。|
|InvalidDiskCategory.NotSupported|The specified disk category is not support the specified instance type.|403|指定的磁盘类型不支持该实例类型。|
|InvalidDiskSize.TooSmall|Specified disk size is less than the size of snapshot.|403|指定的磁盘小于指定快照大小。|
|InvalidInstanceType.ZoneNotSupported|The specified zone does not support this InstanceType.|403|指定Zone不支持该实例类型。|
|InvalidNetworkType.MismatchRamRole|Ram role cannot be attached to instances of Classic network type.|403|实例RAM角色不能被用于经典网络。|
|InvalidParameter.ResourceOwnerAccount|ResourceOwnerAccount is Invalid.|403|指定的`ResourceOwnerAccount`不合法。|
|InvalidPayMethod|The specified billing method is not valid.|403|指定的付费类型不存在。|
|InvalidResourceType.NotSupported|This resource type is not supported; please try other resource types.|403|创建实例的配置暂无可用区支持，请选择其他配置创建。|
|InvalidSnapshotId.NotDataDiskSnapshot|The specified snapshot is system disk snapshot.|403|系统盘快照不能创建数据盘。|
|InvalidSnapshotId.NotReady|The specified snapshot has not completed yet.|403|快照没有完成。|
|InvalidSystemDiskCategory.ValueUnauthorized|The disk category is not authorized.|403|磁盘种类未被授权使用。|
|InvalidUser.PassRoleForbidden|The RAM user does not have the privilege to pass a role.|403|您使用的RAM用户账号暂不具有`PassRole`的权限，请联系主账号拥有者[授权](../intl.zh-CN/快速入门/为 RAM 用户授权.md#)PassRole权限。|
|InvalidVSwitchId.NotFound|The VSwitchId provided does not exist in our records.|403|指定的`VSwitchId`不存在。|
|IoOptimized.NotSupported|The specified image is not support IoOptimized Instance.|403|指定的镜像不支持I/O优化实例。|
|IoOptimized.NotSupported|Vpc is not support IoOptimized instance.|403|指定的VPC中无法创建I/O优化实例。|
|OperationDenied|The specified snapshot is not allowed to create disk.|403|特定磁盘的快照不能创建磁盘或者快照不能创建磁盘。|
|OperationDenied|The creation of Instance to the specified Zone is not allowed.|403|该可用区无权创建实例或者`ZoneId`和`RegionId`不匹配。|
|OperationDenied|The specified Image is disabled or is deleted.|403|指定的镜像找不到。|
|OperationDenied|Sales of this resource are temporarily suspended in the specified region; please try again later.|403|该地域暂时停售按量实例。|
|OperationDenied|The capacity of snapshot exceeds the size limit of the specified disk category or the specified category is not authorized.|403|指定的DataDisk.n.Size不合法（超出范围）或者磁盘种类未被授权使用。|
|OperationDenied|The type of the disk does not support the operation.|403|指定磁盘类型不支持该操作。|
|OperationDenied.NoStock|Sales of this resource are temporarily suspended in the specified region; please try again later.|403|库存不足，请尝试其它系列或者其它可用区/地域的实例。|
|QuotaExceed.BuyImage|The specified image is from the image market, You have not bought it or your quota has been exceeded.|403|指定镜像没有购买或超过限制。|
|QuotaExceed.PortableCloudDisk|The quota of portable cloud disk exceeds.|403|可挂载的云磁盘数量已经达到上限（最多16块）。|
|RegionUnauthorized|There is no authority to create instance in the specified region.|403|您暂时无法使用该地域的资源。|
|SecurityGroupInstanceLimitExceed|The maximum number of instances in a security group is exceeded.|403|该安全组内实例数量已经达到上限。|
|Zone.NotOnSale|The specified zone is not available for purchase.|403|创建实例的可用区已经关闭售卖，请更换其他可用区。或者无法在该可用区使用指定 VPC 的虚拟交换机。|
|Zone.NotOpen|The specified zone is not granted to you to buy resources yet.|403|您暂时无法在指定可用区创建实例。|
|ZoneId.NotFound|The specified zone does not exists.|403|指定的可用区不存在。|
|DependencyViolation.IoOptimized|The specified InstanceType must be IoOptimized instance.|404|指定的实例规格必须是I/O优化实例。|
|HOSTNAME\_ILLEGAL|hostname is not valid.|404|指定的`HostName`不合法。|
|InvalidDataDiskSnapshotId.NotFound|The specified parameter DataDisk.n.SnapshotId is not valid.|404|指定的`DataDisk.n.SnapshotId`不存在。|
|InvalidDataDiskSnapshotId.NotFound|The specified parameter DataDisk.n.SnapshotId is not valid.|404|指定的`DataDisk.n.SnapshotId`不存在。|
|InvalidDeploymentSetId.NotFound|The specified DeploymentSetId does not exist.|404|指定的`DeploymentSetId`不存在。|
|InvalidImageId.NotFound|The specified ImageId does not exist.|404|指定的镜像不存在。|
|InvalidInstanceChargeType.NotFound|The InstanceChargeType does not exist in our records.|404|指定的`InstanceChargeType`不存在。|
|InvalidKeyPairName.NotFound|The specified KeyPairName does not exist in our records.|404|指定的`KeyPairName`不存在。|
|InvalidRamRole.NotFound|The specified RamRoleName does not exist.|404|指定的`RamRoleName`不存在。|
|InvalidRegionId.NotFound|The specified RegionId does not exist.|404|指定的`RegionId`不存在。|
|InvalidSecurityGroupId.NotFound|The specified SecurityGroupId does not exist.|404|指定的`SecurityGroupId`不存在。或者您无法使用指定的安全组。|
|InvalidSystemDiskSize|The specified parameter SystemDisk.Size is invalid.|404|指定的`SystemDisk.Size`不合法。|
|InvalidSystemDiskSize.LessThanImageSize|The specified parameter SystemDisk.Size is less than the image size.|404|指定的`SystemDisk.Size`小于镜像大小。|
|InvalidSystemDiskSize.LessThanMinSize|The specified parameter SystemDisk.Size is less than the min size.|404|指定的`SystemDisk.Size`小于磁盘大小下限。|
|InvalidSystemDiskSize.MoreThanMaxSize|The specified parameter SystemDisk.Size is more than the max size.|404|指定的 `SystemDisk.Size` 大于磁盘大小上限。|
|InvalidVSwitchId.NotFound|Specified virtual switch does not exist.|404|指定的VSwitch不存在。|
|InvalidZoneId.NotFound|The specified ZoneId does not exist.|404|指定Zone 存在。|
|IoOptimized.NotSupported|The specified InstanceType is not support IoOptimized instance.|404|指定的实例类型不支持I/O优化实例。|
|OperationDenied|Another Instance is being created.|404|正在创建另外的实例。|
|PaymentMethodNotFound|No billing method has been registered on the account.|404|该账号下没有付款方式。|
|InternalError|The request processing has failed due to some unknown error,exception or failure.|500|内部错误。|

