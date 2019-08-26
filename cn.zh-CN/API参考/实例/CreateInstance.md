# CreateInstance {#doc_api_Ecs_CreateInstance .reference}

调用CreateInstance创建一台包年包月或者按量付费ECS实例。

## 接口说明 {#description .section}

**说明：** 创建一台实例前，您可以调用[DescribeAvailableResource](~~66186~~)查看指定地域或者可用区内的实例资源供给情况。若您希望批量创建实例并且实例自动进入运行中（Running）状态，推荐您使用[RunInstances](~~63440~~)接口。

创建实例会涉及到资源计费，建议您提前了解云服务器ECS的计费方式。更多详情，请参见[计费概述](~~25398~~)。若实例计费方式为包年包月实例（`PrePaid`），则在付款时默认会使用您可用的优惠券。

创建实例需要通过实名认证。您可以参见[账号实名认证相关文档](~~48263~~)完成认证。

根据请求参数创建实例时，您需要注意以下几类请求参数的使用说明。

使用说明：**实例规格**

-   创建实例时，可以通过参数`IoOptimized`指定是否创建I/O优化实例。
-   如果选择创建本地SSD盘（`ephemeral_ssd`）的实例，一旦创建就不能修改实例规格。

使用说明：**镜像**

在创建实例时，必须要选择镜像，确定新创建实例的系统盘配置。基于镜像创建实例后，实例的系统盘即为此镜像的完全克隆。

-   实例内存为512 MiB时不能使用除Windows Server 1709之外的Windows镜像。
-   实例内存为4 GiB以上时不能使用32位操作系统的镜像。

使用说明：**网络配置**

-   专有网络VPC类型实例只能在创建时指定，必须且只能属于一个交换机。
-   指定`VSwitchId`时，`SecurityGroupId`和`VSwitchId`要属于同一个VPC。
-   `VSwitchId`和`PrivateIpAddress`同时指定时，`PrivateIpAddress`要包含在交换机的CidrBlock之内。
-   `PrivateIpAddress`依赖于`VSwitchId`，不能单独指定`PrivateIpAddress`。
-   使用本接口创建的实例将不会分配公网IP，您可以调用[AllocatePublicIpAddress](~~25544~~)分配公网IP。
-   在创建实例时，`InternetChargeType`和`InternetMaxBandwidthOut`的设置决定可能发生的带宽费用。`InternetMaxBandwidthIn`的值在任何情况下都与计费无关，实例的入数据流量是免费的。
-   `InternetChargeType=PayByBandwidth`表示按固定带宽付费，则`InternetMaxBandwidthOut`为所选的固定带宽值。
-   `InternetChargeType=PayByTraffic`表示按使用流量付费，则`InternetMaxBandwidthOut`取带宽的上限设置，计费以实际使用的网络流量为依据。

使用说明：**安全组**

-   安全组需要预先创建，可通过[CreateSecurityGroup](~~25553~~)创建。
-   可以在新创建实例时指定安全组，也可通过[ModifyInstanceAttribute](~~25503~~)的接口变更实例所属安全组。
-   在同一个安全组内的实例内网可以相互访问。不同安全组之间默认隔离，不可相互访问，但是可以授权访问。更多详情，请参见[AuthorizeSecurityGroup](~~25554~~)和[AuthorizeSecurityGroupEgress](~~25560~~)。
-   同一个安全组内的实例数量不能超过1000台。

使用说明：**存储**

-   不同类型云盘的最大容量不同：
    -   单块普通云盘（`cloud`）容量最大不能超过2000 GiB。
    -   单块高效云盘（`cloud_efficiency`）容量最大不超过32 TiB（32768 GiB）。
    -   单块SSD云盘（`cloud_ssd`）容量最大不能超过32 TiB（32768 GiB）。
    -   单块ESSD云盘（`cloud_essd`）容量最大不能超过32 TiB（32768 GiB）。
    -   单块本地SSD盘（`ephemeral_ssd`）容量最大不能超过800 GiB。
-   创建实例时，我们根据您指定的镜像为实例分配一个相应大小的系统盘。系统盘容量必须大于或者等于max\{20, ImageSize\}。系统盘的种类有普通云盘（`cloud`）、高效云盘（`cloud_efficiency`）、SSD云盘（`cloud_ssd`）、和本地SSD盘（`ephemeral_ssd`）。
-   当系统盘是普通云盘（`cloud`）、高效云盘（`cloud_efficiency`）或SSD云盘（`cloud_ssd`）时，数据盘不能是本地SSD盘`ephemeral_ssd`。
-   当实例选择为I/O优化实例时，系统盘只能选择高效云盘（`cloud_efficiency`）及SSD云盘（`cloud_ssd`）。
-   一个实例最多添加16块数据盘。数据盘挂载点由系统默认顺序分配，/dev/xvdb开始到/dev/xvdz。数据盘选择本地SSD盘`ephemeral_ssd`时，系统盘必须为本地SSD盘，同时一个实例的本地SSD盘总容量不超过1 TiB（1024 GiB，不包括系统盘）。
-   本地SSD盘`ephemeral_ssd`必须在创建实例时指定，实例创建完成后不能再添加。更多详情，请参见[实例规格族](~~25378~~)。

使用说明：**自定义数据**

若实例满足使用[实例自定义数据](~~49121~~)的限制，您可传入UserData信息。UserData以Base64的方式编码。UserData将以不加密的方式传入，不要以明文方式传入机密的信息，例如密码和私钥等。如果必须传入，建议加密后，然后以Base64的方式编码后再传入，在实例内部以同样的方式反解密。

使用说明：**其他**

在阿里云CLI及SDK中使用API时，部分带点号（.）的入参需要去掉点号（.）再使用，包括：`SystemDisk.Category`、`SystemDisk.Size`、`SystemDisk.Description`、`DataDisk.N.Size`、`DataDisk.N.Category`、`DataDisk.N.SnapshotId`、`DataDisk.N.DiskName`、`DataDisk.N.Description`、`DataDisk.N.DeleteWithInstance`、`DataDisk.N.PerformanceLevel`。

例如，在[阿里云CLI](~~66653~~)及[SDK](https://github.com/aliyun)中使用`SystemDiskCategory`表示入参`SystemDisk.Category`。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=CreateInstance&type=RPC&version=2014-05-26)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|ImageId|String|是|win2008r2\_64\_ent\_sp1\_en-us\_40G\_alibase\_20170915.vhd|镜像文件ID，启动实例时选择的镜像资源。如需使用云市场镜像，您可以在云市场镜像商详情页查看`ImageId`。

 |
|InstanceType|String|是|ecs.g5.large|实例的资源规格。更多详情，请参见[实例规格族](~~25378~~)，也可以调用[DescribeInstanceTypes](~~25620~~)接口获得最新的规格表。

 |
|RegionId|String|是|cn-hangzhou|实例所属的地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。

 |
|Action|String|否|CreateInstance|系统规定参数。对于您自行拼凑HTTP/HTTPS URL发起的API请求，`Action`为必选参数。取值：CreateInstance

 |
|SecurityGroupId|String|否|sg-bp15ed6xe1yxeycg7\*\*\*|指定新创建实例所属于的安全组代码，同一个安全组内的实例之间可以互相访问。

 |
|InstanceName|String|否|yk201812061032|实例的名称。长度为2~128个英文或中文字符。必须以大小字母或中文开头，不能以 http:// 和 https:// 开头。可以包含数字、半角冒号（:）、下划线（\_）或者连字符（-）。如果没有指定该参数，默认值为实例的InstanceId。

 |
|AutoRenew|Boolean|否|true|是否要自动续费。当参数`InstanceChargeType`取值`PrePaid`时才生效。取值范围：

 -   true：自动续费。
-   false（默认）：不自动续费。

 |
|InternetChargeType|String|否|PayByTraffic|网络计费类型。取值范围：

 -   PayByBandwidth：按固定带宽计费
-   PayByTraffic（默认）：按使用流量计费

 |
|AutoRenewPeriod|Integer|否|2|每次自动续费的时长，当参数AutoRenew取值True时为必填。

 PeriodUnit为Week时，AutoRenewPeriod取值\{“1”, “2”, “3”\}

 PeriodUnit为Month时，AutoRenewPeriod取值\{“1”, “2”, “3”, “6”, “12”\}

 |
|InternetMaxBandwidthIn|Integer|否|200|公网入带宽最大值，单位为Mbit/s。取值范围：1~200

 默认值：200

 |
|InternetMaxBandwidthOut|Integer|否|5|公网出带宽最大值，单位为Mbit/s。取值范围：0~100

 默认值：0

 |
|HostName|String|否|LocalHost|云服务器的主机名。

 -   点号（.）和短横线（-）不能作为首尾字符，更不能连续使用。
-   Windows实例：字符长度为2~15，不支持点号（.），不能全是数字。允许大小写英文字母、数字和短横线（-）。
-   其他类型实例（Linux等）：字符长度为2~64，支持多个点号（.），点之间为一段，每段允许大小写英文字母、数字和短横线（-）。

 |
|Password|String|否|EcsV587!|实例的密码。长度为8至30个字符，必须同时包含大小写英文字母、数字和特殊符号中的三类字符。特殊符号可以是：

 ```

()`~!@#$%^&*-_+=|{}[]:;'<>,.?/

```

 其中，Windows实例不能以斜线号（/）为密码首字符。

 **说明：** 如果传入`Password`参数，建议您使用HTTPS协议发送请求，避免密码泄露。

 |
|PasswordInherit|Boolean|否|false|是否使用镜像预设的密码。使用该参数时，Password参数必须为空，同时您需要确保使用的镜像已经设置了密码。

 |
|DeploymentSetId|String|否|ds-bp1brhwhoqinyjd6t\*\*\*|部署集ID。

 |
|ZoneId|String|否|cn-hangzhou-g|实例所属的可用区ID。更多详情，请参见[DescribeZones](~~25610~~)获取可用区列表。

 默认值：空，表示随机选择。

 |
|ClusterId|String|否|c-clusterid1|实例所在的集群ID。

 **说明：** 该参数即将被弃用，为提高兼容性，请尽量使用其他参数。

 |
|ClientToken|String|否|123e4567-e89b-12d3-a456-426655440000|保证请求幂等性。从您的客户端生成一个参数值，确保不同请求间该参数值唯一。**ClientToken**只支持ASCII字符，且不能超过64个字符。更多详情，请参见[如何保证幂等性](~~25693~~)。

 |
|VlanId|String|否|10|实例的VLAN ID。

 |
|InnerIpAddress|String|否|10.0.0.0|实例的内网IP。

 |
|SystemDisk.Size|Integer|否|40|系统盘大小，单位为GiB。取值范围：20~500

 该参数的取值必须大于或者等于max\{20, ImageSize\}。

 默认值：max\{40, ImageSize\}

 |
|SystemDisk.Category|String|否|cloud\_ssd|系统盘的云盘种类。[已停售的实例规格](~~55263~~)且非I/O优化实例默认值为cloud，否则默认值为cloud\_efficiency。取值范围：

 -   cloud：普通云盘
-   cloud\_efficiency：高效云盘
-   cloud\_ssd：SSD云盘
-   ephemeral\_ssd：本地SSD盘
-   cloud\_essd：ESSD云盘。

 |
|SystemDisk.DiskName|String|否|SystemDisk|系统盘名称。长度为2~128个英文或中文字符。必须以大小字母或中文开头，不能以 http:// 和 https:// 开头。可以包含数字、半角冒号（:）、下划线（\_）或者连字符（-）。默认值：空。

 |
|SystemDisk.Description|String|否|SystemDiskFinance|系统盘描述。长度为2~256个英文或中文字符，不能以 http:// 和 https:// 开头。默认值：空。

 |
|DataDisk.N.Size|Integer|否|2000|第n个数据盘的容量大小，n的取值范围为1~16，内存单位为GiB。取值范围：

 -   cloud：5~2000
-   cloud\_efficiency：20~32768
-   cloud\_ssd：20~32768
-   cloud\_essd：20~32768
-   ephemeral\_ssd：5~800

 该参数的取值必须大于等于参数`SnapshotId`指定的快照的大小。

 |
|DataDisk.N.SnapshotId|String|否|s-bp17441ohwka0yuhx\*\*\*|创建数据盘n使用的快照。n的取值范围为1~16。指定参数`DataDisk.N.SnapshotId`后，参数`DataDisk.N.Size`会被忽略，实际创建的云盘大小为指定的快照的大小。不能使用早于2013年7月15日（含）创建的快照，请求会报错被拒绝。

 |
|DataDisk.N.Category|String|否|cloud\_ssd|数据盘n的云盘种类。取值范围：

 -   （默认）cloud：普通云盘
-   cloud\_efficiency：高效云盘
-   cloud\_ssd：SSD云盘
-   ephemeral\_ssd：本地SSD盘
-   cloud\_essd：ESSD云盘。

 |
|DataDisk.N.DiskName|String|否|DataDisk|数据盘名称。长度为2~128个英文或中文字符。必须以大小字母或中文开头，不能以 http:// 和 https:// 开头。可以包含数字、半角冒号（:）、下划线（\_）或者连字符（-）。默认值：空。

 |
|DataDisk.N.Description|String|否|DataDiskFinance|数据盘描述。长度为2~256个英文或中文字符，不能以 http:// 和 https:// 开头。默认值：空。

 |
|DataDisk.N.Device|String|否|/dev/xvda|挂载点。

 |
|DataDisk.N.DeleteWithInstance|Boolean|否|true|表示数据盘是否随实例释放。默认值：true

 |
|DataDisk.N.Encrypted|Boolean|否|false|数据盘n是否加密。默认值：false

 |
|Description|String|否|InstanceFinance|实例的描述。长度为2~256个英文或中文字符，不能以 http:// 和 https:// 开头。默认值：空。

 |
|VSwitchId|String|否|vsw-bp1s5fnvk4gn2tws03\*\*\*|如果是创建VPC类型的实例，需要指定虚拟交换机ID。

 |
|PrivateIpAddress|String|否|172.16.236.14X|实例私网IP地址。该IP地址必须为VSwitchId网段的子集网址。

 |
|IoOptimized|String|否|optimized|是否为I/O优化实例。[已停售的实例规格](~~55263~~)实例默认值是none，其他实例规格默认值是optimized。取值范围：

 -   none：非I/O优化
-   optimized：I/O优化

 |
|UseAdditionalService|Boolean|否|true|是否使用阿里云提供的虚拟机系统配置（Windows：NTP、KMS；Linux：NTP、YUM）。

 |
|InstanceChargeType|String|否|PrePaid|实例的付费方式。取值范围：

 -   PrePaid：包年包月。选择该类付费方式时，您必须确认自己的账号支持余额支付/信用支付，否则将返回 `InvalidPayMethod`的错误提示。
-   PostPaid（默认）：按量付费。

 |
|Period|Integer|否|1|购买资源的时长，单位为：月。当参数`InstanceChargeType`取值为`PrePaid`时才生效且为必选值。一旦指定了`DedicatedHostId`，则取值范围不能超过专有宿主机的订阅时长。取值范围：

 PeriodUnit为Week时，Period取值：\{“1”, “2”, “3”, “4”\}

 PeriodUnit为Month时，Period取值：\{ “1”, “2”, “3”, “4”, “5”, “6”, “7”, “8”, “9”, “12”, “24”, “36”,”48”,”60”\}

 |
|PeriodUnit|String|否|Month|购买资源的时长。可选值：Week和Month（默认）。

 |
|Tag.N.Key|String|否|FinanceDept|实例、云盘和主网卡的标签键。N的取值范围：1~20。一旦传入该值，则不允许为空字符串。最多支持64个字符，不能以aliyun和acs:开头，不能包含 http:// 或者 https:// 。

 |
|Tag.N.Value|String|否|FinanceDeptJoshua|实例、云盘和主网卡的标签值。N的取值范围：1~20。一旦传入该值，可以为空字符串。最多支持128个字符，不能以aliyun和acs:开头，不能包含 http:// 或者 https:// 。

 |
|UserData|String|否|ZWNobyBoZWxsbyBlY3Mh|实例自定义数据，需要以Base64方式编码，原始数据最多为16KB。

 |
|SpotStrategy|String|否|NoSpot|后付费实例的抢占策略。当参数`InstanceChargeType`取值为`PostPaid`时生效。取值范围：

 -   NoSpot（默认）：正常按量付费实例。
-   SpotWithPriceLimit：设置上限价格的抢占式实例。
-   SpotAsPriceGo：系统自动出价，跟随当前市场实际价格。

 |
|KeyPairName|String|否|Instancetest|密钥对名称。

 -   Windows实例，忽略该参数。默认为空。即使填写了该参数，仍旧只执行`Password`的内容。
-   Linux实例的密码登录方式会被初始化成禁止。为提高实例安全性，强烈建议您使用密钥对的连接方式。

 |
|SpotPriceLimit|Float|否|0.98|设置实例的每小时最高价格。支持最大3位小数，参数`SpotStrategy`取值为`SpotWithPriceLimit`时生效。

 |
|SpotInterruptionBehavior|String|否|Terminate|抢占实例中断模式。目前仅支持Terminate（默认）直接释放实例。

 |
|RamRoleName|String|否|FinanceDept|实例RAM角色名称。您可以使用RAM API [ListRoles](~~28713~~) 查询您已创建的实例RAM角色。

 |
|SecurityEnhancementStrategy|String|否|Active|是否开启安全加固。取值范围：

 -   Active：启用安全加固，只对系统镜像生效。
-   Deactive：不启用安全加固，对所有镜像类型生效。

 |
|ResourceGroupId|String|否|rg-resourcegroupid|实例所在的企业资源组ID。

 |
|HpcClusterId|String|否|hpc-hpcclusterid|实例所属的HPC集群ID。

 |
|DryRun|Boolean|否|false|是否只预检此次请求。

 -   true：发送检查请求，不会创建实例。检查项包括是否填写了必需参数、请求格式、业务限制和ECS库存。如果检查不通过，则返回对应错误。如果检查通过，则返回错误码`DryRunOperation`。
-   false（默认）：发送正常请求，通过检查后直接创建实例。

 |
|DedicatedHostId|String|否|dh-dedicatedhost1|是否在专有宿主机上创建ECS实例。您可以通过[DescribeDedicatedHosts](~~94572~~)查询专有宿主机ID列表。

 由于专有宿主机不支持创建抢占式实例，指定`DedicatedHostId`参数后，会自动忽略请求中的`SpotStrategy`和`SpotPriceLimit`设置。

 |
|CreditSpecification|String|否|Standard|修改t5突发性能实例的运行模式。取值范围：

 -   Standard：标准模式，实例性能请参见[什么是突发性能实例](~~59977~~)下的性能约束模式章节。
-   Unlimited：无性能约束模式，实例性能请参见[什么是突发性能实例](~~59977~~)下的无性能约束模式章节。

 默认值：无。

 |
|DeletionProtection|Boolean|否|false|实例释放保护属性，指定是否支持通过控制台或API（[DeleteInstance](~~25507~~)）释放实例。

 -   true：开启实例释放保护。
-   false（默认）：关闭实例释放保护。

 **说明：** 该属性仅适用于按量付费实例，且只能限制手动释放操作，对系统释放操作不生效。

 |
|SystemDisk.PerformanceLevel|String|否|PL1|创建ESSD云盘作为系统盘使用时，设置云盘的性能等级。取值范围：

 -   PL1（默认）：单盘最高随机读写IOPS 5万。
-   PL2：单盘最高随机读写IOPS 10万。
-   PL3：单盘最高随机读写IOPS 100万。

 有关如何选择ESSD性能等级，请参见[ESSD云盘](~~122389~~)。

 |
|DataDisk.N.PerformanceLevel|String|否|PL2|创建ESSD云盘作为数据盘使用时，设置云盘的性能等级。N的取值必须和`DataDisk.N.Category=cloud_essd`中的N保持一致。取值范围：

 -   PL1（默认）：单盘最高随机读写IOPS 5万。
-   PL2：单盘最高随机读写IOPS 10万。
-   PL3：单盘最高随机读写IOPS 100万。

 有关如何选择ESSD性能等级，请参见[ESSD云盘](~~122389~~)。

 |
|Affinity|String|否|default|专有宿主机实例是否与专有宿主机关联。取值范围：

 -   default：实例不与专有宿主机关联。已开启停机不收费功能的实例，停机后再次启动时，若原专有宿主机可用资源不足，则实例被放置在自动部署资源池的其它专有宿主机上。
-   host：实例与专有宿主机关联。已开启停机不收费功能的实例，停机后再次启动时，仍放置在原专有宿主机上。若原专有宿主机可用资源不足，则实例重启失败。

 默认值：default

 |
|Tenancy|String|否|default|是否在专有宿主机上创建实例。取值范围：

 -   default：在非专有宿主机上创建实例。
-   host：在专有宿主机上创建实例。若您不指定`DedicatedHostId`，则由阿里云自动选择专有宿主机放置实例。

 默认值：default

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|InstanceId|String|i-instanceid1|实例ID，是访问实例的唯一标识。

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。无论调用接口成功与否，我们都会返回请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=CreateInstance
&RegionId=cn-hangzhou
&ImageId=_32_23c472_20120822172155_aliguest.vhd
&SecurityGroupId=sg-bp15ed6xe1yxeycg7***
&HostName=Bctest01
&InstanceType=ecs.t1.small
&<公共请求参数>
```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<CreateInstanceResponse>
      <RequestId>04F0F334-1335-436C-A1D7-6C044FE73368</RequestId>
      <InstanceId>i-instance1</InstanceId>
</CreateInstanceResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"InstanceId":"i-instance1",
	"RequestId":"04F0F334-1335-436C-A1D7-6C044FE73368"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InvalidInstanceType.ValueUnauthorized|The specified InstanceType is not authorized.|指定的实例规格未授权使用。|
|400|InvalidInternetChargeType.ValueNotSupported|The specified InternetChargeType is not valid.|指定的实例升降配规格不存在。|
|400|InvalidParameter|The specified parameter "InternetMaxBandwidthOut" is not valid.|指定的 InternetMaxBandwidthOut 参数不合法。|
|400|InvalidSystemDiskCategory.ValueNotSupported|The specified parameter " SystemDisk.Category " is not valid.|指定的磁盘类型无效。|
|404|IoOptimized.NotSupported|The specified instancetype is not support IoOptimized instance|指定的实例规格不支持 I/O 优化。|
|400|InvalidDataDiskSize.ValueNotSupported|The specified DataDisk.n.Size beyond the permitted range, or the capacity of snapshot exceeds the size limit of the specified disk category.|指定的数据盘大小已超过最大允许值。|
|403|InvalidDiskCategory.NotSupported|The specified disk category is not support the specified instance type.|指定的磁盘种类不支持该实例规格。|
|400|InvalidInstanceType.ValueNotSupported|The specified InstanceType does not exist or beyond the permitted range.|指定的实例规格不支持。|
|404|InvalidSecurityGroupId.NotFound|The specified SecurityGroupId does not exist.|指定的安全组在该用户账号下不存在，请您检查安全组id是否正确。|
|400|InvalidDescription.Malformed|The specified parameter "Description" is not valid.|指定的资源描述格式不合法。长度为2-256个字符，不能以 http:// 和 https:// 开头。|
|400|InvalidHostName.Malformed|The specified parameter "HostName" is not valid.|指定的HostName格式不合法。|
|400|InvalidPassword.Malformed|The specified parameter "Password" is not valid.|指定的 Password 参数不合法。|
|400|InvalidPasswordParam.Mismatch|The input password should be null when passwdInherit is true.|启用PasswdInherit后，不允许指定用户名密码。|
|400|InvalidSystemDiskCategory.ValueNotSupported|The specified parameter "SystemDisk.Category" is not valid.|指定的 SystemDisk.Category 不合法。|
|400|InvalidDiskName.Malformed|The specified parameter "SystemDisk.DiskName or DataDisk.n.DiskName" is not valid.|参数 SystemDisk.DiskName 或 DataDisk.n.DiskName 不合法。|
|400|InvalidDiskDescription.Malformed|The specified parameter "SystemDisk.DiskDescription" or "DataDisk.n.Description" is not valid.|参数 SyatemDisk.DiskDescription 或 DataDisk.n.Description 不合法。|
|400|InvalidDataDiskCategory.ValueNotSupported|The specified parameter "DataDisk.n.Category" is not valid.|指定的参数 DataDisk.n.Category 不合法。|
|404|InvalidDataDiskSnapshotId.NotFound|The specified parameter "DataDisk.n.SnapshotId" is not valid.|指定的参数 DataDisk.n.SnapshotId 不合法。|
|400|InvalidDataDevice.Malformed|The specified parameter "DataDisk.n.Device" is not valid.|指定的参数 DataDisk.n.Device 不合法。|
|400|InvalidNodeControllerId.Malformed|The specified parameter "NodeControllerId" is not valid.|指定的 NodeControllerId 不合法。|
|400|InvalidInnerIpAddress.Malformed|The specified parameter "InnerIpAddress" is not valid.|指定的 DiskDeviceMapping.n.DiskImageSize 超出最大限值。|
|400|InvalidInnerIpAddress.Unusable|The specified InnerIpAddress is already used or not found in usable ip range.|指定的 InnerIpAddress 不可用。|
|400|OperationDenied|The specified parameter "VlanId" is not valid or vlan has not enough IP address.|指定的 VlanId 不合法，或已超出最大 IP 地址数限制。|
|400|InvalidParameter.Conflict|The specified image does not support the specified instance type.|指定的镜像不能用于指定的实例规格。|
|400|ImageNotSupportCloudInit|The specified image does not support cloud-init.|指定的镜像不支持 cloud-init。|
|400|InvalidSnapshotId.BasedSnapshotTooOld|The specified snapshot is created before 2013-07-15.|指定的快照创建于 2013-07-15 之前。|
|400|QuotaExceed.AfterpayInstance|The maximum number of Pay-As-You-Go instances is exceeded: %s|已经达到允许创建按量实例数量的最大值。|
|403|ImageNotSubscribed|The specified image has not be subscribed.|指定的镜像未在镜像市场订阅。|
|400|InvalidMarketImageChargeType.NotSupport|The specified chargeType of marketImage is unsupported.|云市场镜像的计费方式无效。|
|403|OperationDenied|The specified Image is disabled or is deleted.|指定的镜像被禁用或被删除。|
|403|InvalidSystemDiskCategory.ValueUnauthorized|The disk category is not authorized.|该磁盘类别未经授权。|
|403|InvalidSnapshotId.NotReady|The specified snapshot has not completed yet.|指定的快照未完成。|
|403|OperationDenied|The specified snapshot is not allowed to create disk.|指定快照不支持创建磁盘。|
|403|InstanceDiskCategoryLimitExceed|The total size of specified disk category in an instance exceeds.|磁盘种类总容量超过实例限制。|
|403|InvalidDevice.InUse|The specified device has been occupied.|指定的设备已经挂载了磁盘。|
|403|ImageRemovedInMarket|The specified market image is not available, Or the specified user defined image includes product code because it is based on an image subscribed from marketplace, and that image in marketplace includeing exact the same product code has been removed.|指定的云市场镜像不可用。|
|404|InvalidClusterId.NotFound|The ClusterId provided does not exist in our records.|指定的 ClusterId 不存在。|
|403|OperationDenied|The creation of Instance to the specified Zone is not allowed.|指定的可用区不支持创建实例。|
|403|CategoryNotSupported|The specified zone does not offer the specified disk category.|指定的可用区没有提供该磁盘种类。|
|403|OperationDenied|The specified Zone or cluster does not offer the specified disk category or the speicified zone and cluster do not match.|指定的可用区或集群中不存在指定磁盘类别，或指定的可用区与集群不匹配。|
|403|OperationDenied.NoStock|The requested resource is sold out in the specified zone; try other types of resources or other regions and zones.|库存不足。|
|400|InvalidInstanceName.Malformed|The specified parameter "InstanceName" is not valid.|指定的实例名称格式不合法。长度为2-128个字符，以英文字母或中文开头，可包含数字，"."，"\_"或"-"。 不能以 http:// 和 https:// 开头。|
|400|InvalidDiskDescription.Malformed|The specified parameter "SystemDisk.DiskDescription or DataDisk.n.Description" is not valid.|参数 SyatemDisk.DiskDescription 或 DataDisk.n.Description 不合法。|
|403|QuotaExceed.PortableCloudDisk|The quota of portable cloud disk exceeds.|可卸载磁盘数量已达上限。|
|500|InternalError|The request processing has failed due to some unknown error.|内部错误，请重试。如果多次尝试失败，请提交工单。|
|403|OperationDenied|Sales of this resource are temporarily suspended in the specified region; please try again later.|指定地域关闭。|
|400|InvalidParameter.Conflict|The specified region and cluster do not match.|指定的地域与指定的集群不匹配。|
|403|SecurityGroupInstanceLimitExceed|The maximum number of instances in a security group is exceeded.|安全组中实例数量超限。|
|403|NodeControllerUnavailable|The Node Controller is temporarily unavailable.|节点控制器暂不可用。|
|403|RegionUnauthorized|There is no authority to create instance in the specified region.|用户未被授权在指定的地域创建实例。|
|403|CategoryNotSupported|The specified Zone or cluster does not offer the specified disk category.|指定的可用区或集群没有提供该磁盘种类。|
|403|InvalidSnapshotId.NotDataDiskSnapshot|The specified snapshot is system disk snapshot.|指定的快照为系统磁盘快照。|
|403|CategoryNotSupported|The specified cluster does not offer the specified disk category.|指定的集群没有提供该磁盘种类。|
|404|InvalidVSwitchId.NotFound|Specified virtual switch does not exist.|指定的虚拟交换机ID不存在。|
|400|InvalidParameter.Mismatch|Specified security group and virtual switch are not in the same VPC.|指定的安全组与虚拟交换机不在同一专有网络中。|
|400|InvalidNetworkType.Mismatch|Specified parameter "InternetMaxBandwidthIn" or "InternetMaxBandwidthOut" conflict with instance network type.|网络类型不匹配,|
|400|InvalidNetworkType.Mismatch|Specified parameter "InternetChargeType" conflict with instance network type.|实例的网络类型不支持指定的网络计费方式。|
|400|InvalidPrivateIpAddress|Specified private IP address is not in the CIDR block of virtual switch.|指定的私有 IP 地址不属于交换机的 CIDR 网段。|
|400|InvalidPrivateIpAddress.Malformed|Specified private IP address is malformed.|指定的私有IP不合法。|
|400|InvalidPrivateIpAddress.Duplicated|Specified private IP address is duplicated.|指定的私网IP已经被使用，请您更换IP再重试。|
|400|QuotaExceeded.PrivateIpAddress|Don't have enough private IPs in this switch|虚拟交换机下的私有IP已经被使用完，请您使用其他的虚拟交换机。|
|400|QuotaExceeded|Living instances quota exceeded in this VPC.|活跃的实例已达上限。|
|400|IncorrectVSwitchStatus|The current status of virtual switch does not support this operation.|指定的虚拟交换机处于pending状态，无法删除。|
|400|InvalidParameter.Mismatch|Specified virtual switch is not in the specified zone.|指定的虚拟交换机在指定的可用区里不存在。|
|400|ResourceNotAvailable|Resource you requested is not available in this region or zone.|指定的地域或可用区不支持专有网络VPC。|
|400|MissingParameter|The input parameter "VSwitchId" that is mandatory for processing this request is not supplied.|参数 VSwitchId 不得为空。|
|400|InvalidDiskCategory.Mismatch|The specified disk categories' combination is not supported.|不支持的磁盘种类搭配。|
|403|DeleteWithInstance.Conflict|The specified disk is not a portable disk and cannot be set to DeleteWithInstance attribute.|指定的磁盘不是可卸载磁盘，不支持随实例释放。|
|404|InvalidImageId.NotFound|The specified ImageId does not exist.|指定的镜像在该用户账号下不存在，请您检查镜像id是否正确。|
|403|InstanceDiskNumLimitExceed|The number of specified disk in an instance exceeds.|实例下磁盘数目超过限制。|
|403|IoOptimized.NotSupported|The specified image is not support IoOptimized Instance.|指定的镜像不支持 I/O 优化型实例。|
|403|ImageNotSupportInstanceType|The specified image don't support the InstanceType instance.|指定的镜像不支持此类实例规格。|
|400|InvalidIoOptimizedValue.ValueNotSupported|IoOptimized value not supported.|不支持指定的 I/O 优化值。|
|404|OperationDenied|Another Instance has been creating|不允许创建新的实例。|
|403|InvalidDiskSize.TooSmall|Specified disk size is less than the size of snapshot|指定的磁盘容量小于快照容量。|
|403|OperationDenied|The type of the disk does not support the operation|此磁盘种类不支持指定的操作。|
|404|InvalidInstanceChargeType.NotFound|The InstanceChargeType does not exist in our records|指定的实例升降配规格不存在。|
|400|MissingParamter|The specified parameter "Period" is not null.|参数 Period 不得为空。|
|400|InvalidPeriod|The specified period is not valid.|指定的时段不合法。|
|403|InvalidDiskCategory.Mismatch|The specified disk categories combination is not supported.|不支持的磁盘种类搭配。|
|403|IoOptimized.NotSupported|Vpc is not support IoOptimized instance.|该 VPC 不支持 I/O 优化型实例。|
|400|InvalidDataDiskCategory.ValueNotSupported|The specified parameter " DataDisk.n.Category " is not valid.|指定的磁盘类型无效。|
|400|InstanceDiskCategoryLimitExceed|The specified DataDisk.n.Size beyond the permitted range, or the capacity of snapshot exceeds the size limit of the specified disk category.|指定的数据盘大小已超过最大允许值。|
|403|OperationDenied|The resource is out of usage.|该实例不在运行状态，请您启动实例或检查操作是否合理。|
|403|QuotaExceed.BuyImage|The specified image is from the image market, You have not bought it or your quota has been exceeded.|指定镜像市场镜像不可用。|
|404|DependencyViolation.IoOptimized|The specified instancetype must be IoOptimized instance.|指定的实例规格必须为 I/O 优化实例，请您检查实例规格是否正确。|
|404|PaymentMethodNotFound|No payment method has been registered on the account.|账户尚未注册支付方式。|
|404|HOSTNAME\_ILLEGAL|hostname is not valid.|指定的主机名不合法。|
|404|InvalidSystemDiskSize.LessThanImageSize|The specified parameter SystemDisk.Size is less than the image size.|指定的参数 SytemDisk.Size 小于镜像文件大小数值。|
|404|InvalidSystemDiskSize.LessThanMinSize|The specified parameter SystemDisk.Size is less than the min size.|指定的系统盘小于最低容量。|
|404|InvalidSystemDiskSize.MoreThanMaxSize|The specified SystemDisk.Size parameter exceeds the maximum size.|指定的系统盘大小超出最大容量。|
|404|InvalidDataDiskSnapshotId.NotFound|The specified parameter DataDisk.n.SnapshotId is not valid.|指定的数据盘快照 ID 不合法。|
|403|InvalidVSwitchId.NotFound|The VSwitchId provided does not exist in our records.|指定的虚拟交换机 ID 不存在。|
|400|InvalidParameter|The specified vm bandwidth is not valid.|指定的虚拟机带宽无效。|
|400|InvalidSystemDiskCategory.ValueNotSupported|The specified parameter SystemDisk.Category is not valid.|指定的 SystemDisk.Category 不合法。|
|403|InvalidParameter.ResourceOwnerAccount|ResourceOwnerAccount is Invalid.|指定的 ResourceOwnerAccount 不合法。|
|404|InvalidSystemDiskSize|The specified parameter SystemDisk.Size is invalid.|指定的 SystemDisk.Size 不合法。|
|400|InvalidParameter.Bandwidth|The specified parameter Bandwidth is not valid.|指定的 Bandwidth 不合法。|
|400|InvalidIPAddress.AlreadyUsed|The specified IPAddress is already used by other resource.|其他资源正在使用指定的 IpAddress。|
|403|InvalidUserData.Forbidden|User not authorized to input the parameter "UserData", please apply for permission "UserData"|您未被授权设置UserDat。|
|400|InvalidUserData.SizeExceeded|The specified parameter "UserData" exceeds the size.|指定的 UserData 超过大小限制。|
|400|InvalidUserData.NotSupported|The specified parameter "UserData" only support the vpc and IoOptimized Instance.|指定的 UserData 仅支持 VPC 和 I/O 优化型实例。|
|403|Zone.NotOpen|The specified zone is not granted to you to buy resources yet.|用户未被授权购买指定的可用区的资源。|
|403|Zone.NotOnSale|The specified zone is not available for purchase.|指定可用区已经售罄，请您更换实例规格或者更换地域创建。|
|403|InvalidClusterId.NotFound|The specified clusterId does not exist.|指定的 ClusterId 不存在。|
|403|InvalidResourceType.NotSupported|This resource type is not supported; please try other resource types.|指定的资源搭配不存在（没有库存）。|
|403|InvalidInstanceType.ZoneNotSupported|The specified zone does not support this instancetype.|指定的可用区里不支持指定的 InstanceType。|
|400|InstanceDiskNumber.LimitExceed|The total number of specified disk in an instance exceeds.|实例下磁盘数目超过限制。|
|400|Account.Arrearage|Your account has an outstanding payment.|账号存在未支付款项。|
|400|InvalidDiskCategory.ValueNotSupported|The specified parameter "DiskCategory" is not valid.|参数 DiskCategory 不合法。|
|400|InvalidAutoRenewPeriod.ValueNotSupported|The specified autoRenewPeriod is not valid.|指定的参数 AutoReleaseTime 不合法。|
|400|QuotaExceed.AfterpayInstance|The maximum number of Pay-As-You-Go instances is exceeded.|按量付费的实例数超限。|
|400|InvalidSpotStrategy|The specified SpotStrategy is not valid.|竞价实例不支持转换|
|400|InvalidSpotParam.EmptyZoneID|The specified ZoneId is empty when SpotStrategy is set.|设置 SpotStrategy 时 ZoneId 为空。|
|400|InvalidSpotPriceLimit|The specified SpotPriceLimitis not valid.|指定的 SpotPriceLimit 不合法。|
|400|InvalidSpotDuration|The specified SpotDuration is not valid.|指定的 SpotDuration 不合法。|
|400|InvalidSpotAuthorized|The specified Spot param is unauthorized.|指定的 Spot 未获得授权。|
|400|InvalidSpotPrepaid|The specified Spot type is not support PrePay Instance.|指定的 Spot 类型不支持包年包月实例。|
|400|InvalidSpotAliUid|The specified UID is not authorized to use SPOT instance.|指定的 UID 无权使用 SPOT 实例。|
|403|InvalidPayMethod|The specified pay method is not valid.|没有可用的付费方式。|
|403|OperationDenied.ImageNotValid|The specified Image is disabled or is deleted.|指定的镜像不存在。|
|403|InvalidUserData.Base64FormatInvalid|The specified UserData is not valid|指定的 UaseData 不合法。|
|400|InvalidTagKey.Malformed|The specified Tag.n.Key is not valid.|指定的标签键不合法。|
|400|InvalidParameter.Bandwidth|%s|参数不支持。|
|400|InvalidDataDiskCategory.ValueNotSupported|%s|参数不支持。|
|400|InvalidSystemDiskCategory.ValueNotSupported|%s|参数不支持。|
|400|InvalidParameter.Conflict|%s|参数冲突。|
|400|InvalidInternetChargeType.ValueNotSupported|%s|参数不支持。|
|400|InvalidInstanceType.ValueNotSupported|%s|实例类型属性不正确。|
|403|InstanceType.Offline|%s|实例规格不能使用。|
|400|RegionUnauthorized|%s|指定地域不支持。|
|500|InternalError|%s|内部错误。|
|400|Zone.NotOnSale|%s|可用区关闭。|
|400|InvalidSystemDiskSize.ValueNotSupported|%s|参数不支持。|
|400|InvalidDataDiskSize.ValueNotSupported|%s|参数不支持。|
|404|InvalidKeyPairName.NotFound|The specified parameter "KeyPairName" does not exist in our records.|密钥对不存在,|
|403|DependencyViolation.WindowsInstance|The instance creating is window, cannot use ssh key pair to login.|Windows操作系统不支持SSH密钥对。|
|400|InvalidInstanceType.ValueNotSupported|The specified parameter "KeyPairName" only support IoOptimized Instance.|非I/O优化实例不支持密钥对。|
|403|RealNameAuthenticationError|Your account has not passed the real-name authentication yet.|您的帐户尚未通过实名认证，请先实名认证后再操作。|
|403|InvalidNetworkType.MismatchRamRole|Ram role cannot be applied to instances of Classic network type.|实例 RAM 角色不能被用于经典网络实例，RAM 角色只能使用在 VPC 实例上。|
|403|InvalidUser.PassRoleForbidden|The RAM user does not have the privilege to pass a RAM role.|该 RAM 用户无权传递 RAM 角色。|
|404|InvalidRamRole.NotFound|The specified RAMRoleName does not exist.|指定的 RamRoleName 不存在。|
|400|OperationDenied|The specified InstanceType or Zone is not available or not authorized.|指定的实例规格或可用区不可用或者未授权。|
|403|InvalidAccountStatus.NotEnoughBalance|Your account does not have enough balance.|账号余额不足，请您先充值再进行该操作。|
|500|InternalError|The request processing has failed due to some unknown error, exception or failure.|发生未知错误。|
|404|InvalidResourceGroup.NotFound|The ResourceGroup provided does not exist in our records.|资源组并不在记录中。|
|403|IncorrectVpcStatus|Current VPC status does not support this operation.|当前专有网络VPC的状态无法支持这个操作。|
|400|InvalidParameter.EncryptedIllegal|%s|参数不支持（加密盘）。|
|400|InvalidParameter.EncryptedNotSupported|%s|参数不支持（加密盘）。|
|400|EncryptedOption.Conflict|%s|参数不支持（加密盘）。|
|400|InvalidParameter.Encrypted.KmsNotEnabled|The encrypted disk need enable KMS|加密磁盘需要启用密钥管理服务。|
|400|InvalidSpotPriceLimit.LowerThanPublicPrice|The specified parameter "soptPriceLimit" can't be lower than current public price.|SpotPriceLimit参数不能低于当前价。|
|400|InvalidHpcClusterId.Unnecessary|The specified HpcClusterId is unnecessary.|HpcClusterId参数不支持。|
|400|InvalidVSwitchId.Necessary|The VSwitchId is necessary.|必须指定VSwitch。|
|400|InvalidHpcClusterId.Necessary|The HpcClusterId is necessary.|必须指定HpcClusterId。|
|400|InvalidHpcClusterId.NotFound|The specified HpcClusterId is not found.|指定的HPC集群ID不存在。|
|400|InvalidHpcClusterId.Creating|The specified HpcClusterId is creating.|指定的HPC集群正在创建中。|
|400|QuotaExceeded.PrivateIpAddress|Don't have enough private IPs in this switch.|VSwitch中可用ip不足。|
|400|InvalidPeriodUnit.ValueNotSupported|The specified parameter PeriodUnit is not valid.|市场单位不支持。|
|400|IncorrectImageStatus|Encrypted snapshots do not support this operation.|加密快照不支持该操作。|
|400|InvalidTagValue.Malformed|The specified Tag.n.Value is not valid.|指定的标签值不合法。|
|400|InvalidSecurityGroup.NotInDefaultVpc|%s|指定的安全组不是DefaultVPC中的安全组。|
|400|VpcNotFound|Vpc is not found according to the specified VSwitch or the vpc does not belong to you.|指定的VPC不存在。|
|403|InvalidParameter.NotMatch|%s|参数冲突。|
|403|OperationDenied.InvalidNetworkType|%s|网络类型不支持。|
|400|InvalidSpotInterruptionBehavior|%s|SpotInterruptionBehavior不支持。|
|403|InvalidSpotInterruptionBehavior.ClassicNetworkNotSupport|The specified SpotInterruptionBehavior does not support Classic network Instance.|抢占式实例不能是经典网络类型。|
|403|InvalidSpotInterruptionBehavior.LocalDiskNotSupport|The specified SpotInterruptionBehavior does not support local disk instance.|抢占是实例不支持本地盘实例。|
|400|OperationDenied.IllegalPaymentPolicy|The current payment policy is illegal, please connect your service provider to authenticate relative agreement.|支付策略不支持。|
|400|InvalidDeploymentOnHost|%s|部署集不支持宿主机。|
|400|InvalidInstanceChargeType.NotSupport|The Dedicated host not support the specified Instance charge type.|专有宿主机不支持该计费方式。|
|400|InvalidNetworkType.NotSupported|The classic networkType not support create ECS on dedicatedHost|专有宿主机不支持经典网络。|
|400|InvalidDedicatedHostId.NotFound|The specified DedicatedHostId does not exist.|指定的专有宿主机ID不存在。|
|400|InvalidDedicatedHostStatus.NotSupport|Operation denied due to dedicated host status.|资源状态不支持操作。|
|400|IncorrectDedicatedHostStatus|The current status of the resource does not support this operation.|资源状态不支持操作。|
|400|ChargeTypeViolation.PostPaidDedicatedHost|Prepaid instance onto postpaid dedicated host is not allowed|专有宿主机不支持更换计费方式。|
|400|InvalidPeriod.ExceededDedicatedHost|Instance expired date can't exceed dedicated host expired date.|实例的自动订阅时长不能晚于专有宿主机订阅时长。|
|400|InvalidInstanceType.ValueUnauthorized|The specified InstanceType is not authorize.|您未被授权使用该实例规格。|
|400|DedicatedHostType.Unmatched|The specified DedicatedHostType doesn?t match the instance type.|抢占是实例不支持该实例规格。|
|400|ChargeTypeViolation.PostPaidDedicatedHost|Prepaid instance onto postpaid dedicated host is not allowed.|专有宿主机不支持更换计费方式。|
|403|OperationDenied.ImageNotValid|%s|镜像不支持此操作。|
|403|QuotaExceed.PostPaidDisk|Living postPaid disks quota exceeded.|按量付费磁盘数量已超出允许数量。|
|403|QuotaExceed.DeploymentSetInstanceQuotaFull|instance quota in one deployment set exceeded.|当前部署集内的实例数量已满额。|
|403|InvalidDiskCategory.NotSupported|The specified disk category is not supported.|该云盘类型不支持。|
|403|InvalidVSwitch.DefaultVSwitchNotSupport|The specified zone in vpc can't support create default vSwitch.|可用区内的VPC不支持创建默认交换机。|
|400|InvalidParameter.CreditSpecification|The specified CreditSpecification is not supported in this region.|当前地域不支持指定的CreditSpecification。|
|400|IncorrectImageStatus|The specified Image is not available.|指定的源镜像状态不正确。|
|403|OperationDenied.ImageNotValid|the specified image is not published in the region.|当前地域暂未提供该镜像。|
|403|OperationDenied.ImageNotValid|the specified image is not found in marketplace.|云市场不存在指定的镜像。|
|404|InvalidMarketImage.NotFound|The specified marketplace image does not exist, please change the imageId and try again.|云市场不存在指定的镜像。|
|400|InvalidInstanceType.NotSupported|The specified instanceType is not supported by the deployment set.|部署集不支持该实例规格。|
|400|InvalidVpcZone.NotSupported|Zone of the specified VSwitch is not available for creating, please try in other zones.|指定的可用区不支持创建DefaultVswitch。|
|400|IncorrectDefaultVpcStatus|The status of the default VPC is invalid.|默认VPC的状态不正确。|
|404|DeploymentSet.NotFound|The specified deployment set does not exist.|指定的部署集不存在。|
|403|OperationDenied.LocalDiskUnsupported|The configuration change is not allowed when the specified instance has local disks mounted.|实例挂载本地盘后不支持规格变配。|
|403|OperationDenied.InconsistentNetwork|The specified security group and vswitch are not in the same vpc.|安全组和交换机的VPC必须相同。|
|403|OperationDenied|If the network segment of the vswitch is the same as that of its VPC. Therefore, the VPC cannot create other vswitchs across the region.|VPC与虚拟交换机的网段相同，无法在多可用区内创建其他交换机。|
|403|DefaultVswitch.Existed|The default vswitch for VPC already exists.|VPC已存在默认交换机。|
|403|IncorrectInstanceStatus|The current status of the resource does not support this operation.|该资源目前的状态不支持此操作。|
|403|CategoryViolation|The specified instance does not support this operation because of its disk category.|挂载有本地磁盘的实例不支持升降配。|
|403|ResourcesNotInSameZone|The specified instance and dedicated host are not in the same zone.|实例和专有宿主机必须在同一地域下。|
|403|InvalidRegion.NotSupport|The specified region does not support byok.|该地域不支持BYOK。|
|403|UserNotInTheWhiteList|The user is not in byok white list.|您暂时不能使用BYOK服务。|
|400|InvalidParameter.EncryptedIllegal|The specified parameter Encrypted must be true when kmsKeyId is not empty.|设置KmsKeyId后，您必须开启加密属性。|
|400|IoOptimized.NotSupported|The specified instance must be IoOptimized instance when kmsKeyId is not empty.|设置KmsKeyId后，您必须使用I/O优化实例。|
|404|InvalidParameter.KMSKeyId.NotFound|The specified KMSKeyId does not exist.|指定的参数值不存在。|
|403|InvalidParameter.KMSKeyId.KMSUnauthorized|ECS service have no right to access your KMS.|ECS未被授权访问您的KMS资源。|
|403|SecurityRisk.3DVerification|We have detected a security risk with your default credit or debit card. Please proceed with verification via the link in your email.|您的支付方式有安全风险，请根据通知指导排查。|
|403|InvalidDisk.SystemDiskSize|The specified SystemDiskSize beyond the permitted range.|系统盘大小超出最大允许值。|
|400|InvalidClientToken.ValueNotSupported|The ClientToken provided is invalid.|指定的 ClientToken 不合法。|
|400|OperationDenied|The current user does not support this operation.|当前用户不支持该操作。|
|403|InsufficientBalance|Your account does not have enough balance.|账户余额不足，请先充值再操作。|
|400|Duplicate.TagKey|The Tag.N.Key contain duplicate key.|标签键中存在重复的键。|
|400|InvalidParam.Tenancy|The specified Tenancy is invalid.|您指定的Tenancy参数值无效。|
|404|InvalidSecurityGroupId.NotFound|%s|指定的安全组ID不存在。|
|403|InvalidVSwitchId.IpInvalid|%s|指定的私网ip不合法。|
|404|InvalidDiskIds.NotPortable|The specified DiskId is not portable.|指定的磁盘是不可移植的。|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

