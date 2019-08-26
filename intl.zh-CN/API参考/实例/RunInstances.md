# RunInstances {#doc_api_Ecs_RunInstances .reference}

调用RunInstances创建一台或多台按量付费或者预付费（包年包月）ECS实例。

## 接口说明 {#description .section}

创建实例前，您可以调用[DescribeAvailableResource](~~66186~~)查看指定地域或者可用区内的资源供给情况。

创建实例会涉及到资源计费，建议您提前了解云服务器ECS的计费方式。更多详情，请参见[计费概述](~~25398~~)。

调用该接口时，您需要注意：

-   单次最多能创建100台实例。
-   您可以指定参数`AutoReleaseTime`设置实例自动释放时间。
-   创建成功后会返回实例ID列表，您可以通过API [DescribeInstances](~~25506~~)查询新建实例状态。
-   创建实例前，您需要确保您已经有可用的安全组。更多详情，请参见[CreateSecurityGroup](~~25553~~)。
-   创建实例时，默认自动启动实例，直到实例状态变成运行中（`Running`）。
-   创建专有网络VPC类型实例前，您需要预先在相应的阿里云地域[创建VPC](~~65430~~)。
-   与[CreateInstance](~~25499~~)相比，通过`RunInstances`创建的实例如果参数`InternetMaxBandwidthOut`的值大于0，则自动为实例分配公网IP。
-   提交创建任务后，参数不合法或者库存不足的情况下会报错，具体的报错原因参见错误码。

 **最佳实践** 

`RunInstances`可以执行批量创建任务，为便于管理与检索，建议您为每批次启动的实例指定标签（`Tag.N.Key`和`Tag.N.Value`），并且为主机名（`HostName`）和实例名称（`InstanceName`）添加有序后缀（`UniqueSuffix`）。

实例启动模板能免除您每次创建实例时都需要填入大量配置参数，您可以创建实例启动模板（[CreateLaunchTemplate](~~74686~~)）后，在`RunInstances`请求中指定`LaunchTemplateId`和`LaunchTemplateVersion`使用启动模板。

您可以在[ECS管理控制台](https://ecs.console.aliyun.com/)创建ECS实例时获取`RunInstances`的最佳实践建议。确认订单时，左侧**API 工作流**罗列出`RunInstances`能使用的关联API以及请求参数的值。右侧提供面向编程语言的SDK示例，目前支持**Java**和**Python**示例。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=RunInstances)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|RegionId|String|是|cn-hangzhou|实例所属的地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。

 |
|Action|String|否|RunInstances|系统规定参数。对于您自行拼凑HTTP/HTTPS URL发起的API请求，`Action`为必选参数。取值：RunInstances

 |
|ZoneId|String|否|cn-hangzhou-g|实例所属的可用区编号，您可以调用[DescribeZones](~~25610~~)获取可用区列表。

 默认值：系统随机选择。

 |
|ImageId|String|否|win2008r2\_64\_ent\_sp1\_en-us\_40G\_alibase\_20170915.vhd|镜像ID，启动实例时选择的镜像资源。您可以通过[DescribeImages](~~25534~~)查询您可以使用的镜像资源。如果您不指定`LaunchTemplateId`或`LaunchTemplateName`以确定启动模板，`ImageId`为必选参数。

 |
|SecurityGroupId|String|否|sg-bp15ed6xe1yxeycg7o\*\*\*|指定新创建实例所属于的安全组ID。同一个安全组内的实例之间可以互相访问，一个安全组最多能管理1000台实例。

 **说明：** SecurityGroupId决定了实例的网络类型，例如，如果指定安全组的网络类型为专有网络VPC，实例则为VPC类型，并同时需要指定参数VSwitchId。

 如果您不指定`LaunchTemplateId`或`LaunchTemplateName`以确定启动模板，`SecurityGroupId`为必选参数。

 |
|VSwitchId|String|否|vsw-bp1s5fnvk4gn2tws03\*\*\*|虚拟交换机ID。如果您创建的是VPC类型ECS实例，需要指定虚拟交换机ID。

 |
|InstanceType|String|否|ecs.g5.large|实例的资源规格。更多详情，请参见[实例规格族](~~25378~~)，也可以调用[DescribeInstanceTypes](~~25620~~)接口获得最新的规格表。

 如果您不指定`LaunchTemplateId`或`LaunchTemplateName`以确定启动模板，`InstanceType`为必选参数。

 |
|InternetMaxBandwidthIn|Integer|否|200|公网入带宽最大值，单位为Mbit/s。取值范围：1~200

 默认值：200

 |
|InternetMaxBandwidthOut|Integer|否|5|公网出带宽最大值，单位为Mbit/s。取值范围：0~100

 默认值：0

 |
|InstanceName|String|否|JoshuaHost|实例名称。长度为2~128个英文或中文字符。必须以大小字母或中文开头，不能以http:// 和 https:// 开头。可以包含数字、半角冒号（:）、下划线（\_）或者连字符（-）。默认值为实例的`InstanceId`。

 **说明：** 创建多台实例时，您可以使用`UniqueSuffix`为这些实例设置不同的`InstanceName`。

 |
|HostName|String|否|JoshuaHost|云服务器的主机名。

 -   点号（.）和短横线（-）不能作为首尾字符，更不能连续使用。
-   Windows实例：字符长度为2~15，不支持点号（.），不能全是数字。允许大小写英文字母、数字和短横线（-）。
-   其他类型实例（Linux等）：字符长度为2~64，支持多个点号（.），点之间为一段，每段允许大小写英文字母、数字和短横线（-）。

 **说明：** 创建多台实例时，您可以使用`UniqueSuffix`为这些实例设置不同的`HostName`。

 |
|UniqueSuffix|Boolean|否|true|是否为`HostName`和`InstanceName`添加有序后缀，有序后缀从001开始递增，最大不能超过999。例如：`LocalHost001`，`LocalHost002`和`MyInstance001`，`MyInstance002`。默认值：false

 |
|Description|String|否|FinaceDept|实例的描述。长度为2~256个英文或中文字符，不能以 http:// 和 https:// 开头。

 |
|PasswordInherit|Boolean|否|false|是否使用镜像预设的密码。使用该参数时，Password参数必须为空，同时您需要确保使用的镜像已经设置了密码。

 |
|Password|String|否|EcsV587!|实例的密码。长度为8至30个字符，必须同时包含大小写英文字母、数字和特殊符号中的三类字符。特殊符号可以是：

 ```

()`~!@#$%^&*-_+=|{}[]:;'<>,.?/

```

 其中，Windows实例不能以斜线号（/）为密码首字符。

 **说明：** 如果传入`Password`参数，建议您使用HTTPS协议发送请求，避免密码泄露。

 |
|KeyPairName|String|否|Instancetest|密钥对名称。

 -   Windows实例，忽略该参数。默认为空。即使填写了该参数，仍旧只执行`Password`的内容。
-   Linux实例的密码登录方式会被初始化成禁止。

 |
|SystemDisk.Size|String|否|40|系统盘大小，单位为GiB。取值范围：20~500

 该参数的取值必须大于或者等于max\{20, ImageSize\}。默认值：max\{40, 参数ImageId对应的镜像大小\}

 |
|SystemDisk.Category|String|否|cloud\_ssd|系统盘的磁盘种类。[已停售的实例规格](~~55263~~)且非I/O优化实例默认值为cloud，否则默认值为cloud\_efficiency。取值范围：

 -   cloud：普通云盘
-   cloud\_efficiency：高效云盘
-   cloud\_ssd：SSD云盘
-   ephemeral\_ssd：本地SSD盘
-   cloud\_essd：ESSD云盘。

 |
|SystemDisk.DiskName|String|否|cloud\_ssdSystem|系统盘名称。长度为2~128个英文或中文字符。必须以大小字母或中文开头，不能以 http:// 和 https:// 开头。可以包含数字、半角冒号（:）、下划线（\_）或者连字符（-）。默认值：空。

 |
|SystemDisk.Description|String|否|FinanceDept|系统盘的描述。长度为2~256个英文或中文字符，不能以 http:// 和 https:// 开头。

 |
|DataDisk.N.Size|Integer|否|2000|第n个数据盘的容量大小，n的取值范围为1~16，内存单位为GiB。取值范围：

 -   cloud：5~2000
-   cloud\_efficiency：20~32768
-   cloud\_ssd：20~32768
-   cloud\_essd：20~32768
-   ephemeral\_ssd：5~800

 该参数的取值必须大于等于参数`SnapshotId`指定的快照的大小。

 |
|DataDisk.N.SnapshotId|String|否|s-bp17441ohwka0yuhx\*\*\*|创建数据盘n使用的快照。n的取值范围为1~16。指定参数`DataDisk.N.SnapshotId`后，参数`DataDisk.N.Size`会被忽略，实际创建的磁盘大小为指定的快照的大小。不能使用早于2013年7月15日（含）创建的快照，请求会报错被拒绝。

 |
|DataDisk.N.Category|String|否|cloud\_ssd|数据盘n的磁盘种类。取值范围：

 -   （默认）cloud：普通云盘
-   cloud\_efficiency：高效云盘
-   cloud\_ssd：SSD云盘
-   ephemeral\_ssd：本地SSD盘
-   cloud\_essd：ESSD云盘。

 |
|DataDisk.N.Encrypted|String|否|false|数据盘n是否加密。默认值：false

 |
|DataDisk.N.KMSKeyId|String|否|0e478b7a-4262-4802-b8cb-00d3fb408\*\*\*|数据盘对应的KMS密钥ID。

 |
|DataDisk.N.DiskName|String|否|cloud\_ssdData|数据盘名称。长度为2~128个英文或中文字符。必须以大小字母或中文开头，不能以 http:// 和 https:// 开头。可以包含数字、半角冒号（:）、下划线（\_）或者连字符（-）。默认值：空。

 |
|DataDisk.N.Description|String|否|FinanceDept|数据盘的描述。长度为2~256个英文或中文字符，不能以 http:// 和 https:// 开头。

 |
|DataDisk.N.Device|String|否|/dev/vda|数据盘的挂载点。

 **说明：** 该参数即将被弃用，为提高兼容性，请尽量使用其他参数。

 |
|DataDisk.N.DeleteWithInstance|Boolean|否|true|表示数据盘是否随实例释放。默认值：true

 |
|IoOptimized|String|否|optimized|是否为I/O优化实例。[已停售的实例规格](~~55263~~)实例默认值是none，其他实例规格默认值是optimized。取值范围：

 -   none：非I/O优化
-   optimized：I/O优化

 |
|NetworkInterface.N.PrimaryIpAddress|String|否|172.16.236.\*\*\*|添加一张辅助弹性网卡并设置主IP地址。N的取值范围为1。

 **说明：** 创建ECS实例时，您最多能添加一张辅助网卡。实例创建成功后，您可以调用[CreateNetworkInterface](~~58504~~)和[AttachNetworkInterface](~~58515~~)添加更多的辅助网卡。

 默认值：从网卡所属的交换机网段中随机选择一个IP地址。

 |
|NetworkInterface.N.VSwitchId|String|否|vsw-vswitchid2|辅助弹性网卡所属的虚拟交换机ID。N的取值范围为1。

 默认值：ECS实例所属的虚拟交换机。

 |
|NetworkInterface.N.SecurityGroupId|String|否|sg-securitygroupid2|辅助弹性网卡所属的安全组ID。N的取值范围为1。

 默认值：实例所属的安全组。

 |
|NetworkInterface.N.NetworkInterfaceName|String|否|FinanceJoshua|辅助弹性网卡名称。N的取值范围为1。

 |
|NetworkInterface.N.Description|String|否|FinanceDept|辅助弹性网卡的描述。N的取值范围为1。长度为2~256个英文或中文字符，不能以http://和https://开头。

 |
|RamRoleName|String|否|FinanceDept|实例RAM角色名称。您可以使用RAM API [ListRoles](~~28713~~)查询您已创建的实例RAM角色。

 |
|UserData|String|否|ZWNobyBoZWxsbyBlY3Mh|实例自定义数据。需要以Base64方式编码，原始数据最多为16 KB。

 |
|MinAmount|Integer|否|2|指定ECS实例最小购买数量。取值范围：1~100

 -   当ECS库存数量小于最小购买数量，会创建失败。
-   当ECS库存数量大于等于最小购买数量，按照库存数量创建。

 |
|Amount|Integer|否|3|指定创建ECS实例的数量。取值范围：1~100

 默认值：1

 |
|SpotPriceLimit|Float|否|0.97|设置实例的每小时最高价格。支持最大3位小数，参数`SpotStrategy`取值为`SpotWithPriceLimit`时生效。

 |
|SpotStrategy|String|否|NoSpot|按量实例的抢占策略。当参数`InstanceChargeType`取值为`PostPaid`时生效。取值范围：

 -   NoSpot（默认）：正常按量付费实例。
-   SpotWithPriceLimit：设置上限价格的抢占式实例。
-   SpotAsPriceGo：系统自动出价，跟随当前市场实际价格。

 |
|SpotInterruptionBehavior|String|否|Terminate|抢占实例中断模式。目前仅支持Terminate（默认）直接释放实例。

 |
|CreditSpecification|String|否|Standard|修改t5突发性能实例的运行模式。取值范围：

 -   Standard：标准模式，实例性能请参见[什么是突发性能实例](~~59977~~)下的性能约束模式章节。
-   Unlimited：无性能约束模式，实例性能请参见[什么是突发性能实例](~~59977~~)下的无性能约束模式章节。

 默认值：无。

 |
|SecurityEnhancementStrategy|String|否|Active|是否开启安全加固。取值范围：

 -   Active：启用安全加固，只对公共镜像生效。
-   Deactive：不启用安全加固，对所有镜像类型生效。

 |
|DeploymentSetId|String|否|ds-bp1brhwhoqinyjd6t\*\*\*|部署集ID。

 |
|DedicatedHostId|String|否|dh-dedicatedhost1|是否在专有宿主机上创建ECS实例。您可以通过[DescribeDedicatedHosts](~~94572~~)查询专有宿主机ID列表。

 由于专有宿主机不支持创建抢占式实例，指定`DedicatedHostId`参数后，会自动忽略请求中的`SpotStrategy`和`SpotPriceLimit`设置。

 |
|Tag.N.Key|String|否|FinanceDept|实例、磁盘和主网卡的标签键。N的取值范围：1~20。一旦传入该值，则不允许为空字符串。最多支持64个字符，不能以aliyun和acs:开头，不能包含 http:// 或者 https:// 。

 |
|Tag.N.Value|String|否|FinanceDept.Joshua|实例、磁盘和主网卡的标签值。N的取值范围：1~20。一旦传入该值，可以为空字符串。最多支持128个字符，不能以aliyun和acs:开头，不能包含 http:// 或者 https:// 。

 |
|HpcClusterId|String|否|hpc-clusterid|实例所属的EHPC集群ID。

 |
|ResourceGroupId|String|否|rg-resourcegroupid1|实例所在的企业资源组ID。

 |
|LaunchTemplateId|String|否|lt-bp1apo0bbbkuy0rj3\*\*\*|启动模板ID。更多详情，请调用[DescribeLaunchTemplates](~~73759~~)。

 您必须指定`LaunchTemplateId`或`LaunchTemplateName`以确定启动模板。

 |
|LaunchTemplateName|String|否|JoshuaWinPostPaid|启动模板名称。您必须指定`LaunchTemplateId`或`LaunchTemplateName`以确定启动模板。

 |
|LaunchTemplateVersion|Long|否|3|启动模板版本。如果您指定了`LaunchTemplateId`或`LaunchTemplateName`而不指定启动模板版本号，则采用默认版本。

 |
|DeletionProtection|Boolean|否|false|实例释放保护属性，指定是否支持通过控制台或API（[DeleteInstance](~~25507~~)）释放实例。

 -   true：开启实例释放保护。
-   false（默认）：关闭实例释放保护。

 **说明：** 该属性仅适用于按量付费实例，且只能限制手动释放操作，对系统释放操作不生效。

 |
|AutoReleaseTime|String|否|2018-01-01T12:05:00Z|自动释放时间。按照[ISO8601](~~25696~~)标准表示，使用UTC +0时间。格式为：yyyy-MM-ddTHH:mm:ssZ。

 -   如果秒（`ss`）取值不是`00`，则自动取为当前分钟（`mm`）开始时。
-   最短释放时间为当前时间半小时之后。
-   最长释放时间不能超过当前时间三年。

 |
|InternetChargeType|String|否|PayByTraffic|网络计费类型。取值范围：

 -   PayByTraffic（默认）：按使用流量计费

 |
|Period|Integer|否|1|购买资源的时长，单位为：月。当参数`InstanceChargeType`取值为`PrePaid`时才生效且为必选值。一旦指定了`DedicatedHostId`，则取值范围不能超过专有宿主机的订阅时长。取值范围：

 -   `PeriodUnit=Week`时，Period取值：\{“1”, “2”, “3”, “4”\}
-   `PeriodUnit=Month`时，Period取值：\{ “1”, “2”, “3”, “4”, “5”, “6”, “7”, “8”, “9”, “12”, “24”, “36”,”48”,”60”\}

 |
|AutoRenew|Boolean|否|true|是否要自动续费。当参数`InstanceChargeType`取值`PrePaid`时才生效。取值范围：

 -   True：自动续费。
-   False（默认）：不自动续费。

 |
|PeriodUnit|String|否|Month|购买资源的时长。可选值：

 -   Week
-   Month（默认）

 |
|AutoRenewPeriod|Integer|否|1|单次自动续费的续费时长。取值范围：

 -   `PeriodUnit=Week`时：\{“1”, “2”, “3”\}
-   `PeriodUnit=Month`时：\{“1”, “2”, “3”, “6”, “12”, "24", "36", "48", "60"\}

 默认值：1

 |
|InstanceChargeType|String|否|PrePaid|实例的付费方式。取值范围：

 -   PrePaid：预付费，包年包月。
-   PostPaid（默认）：按量付费。

 选择预付费时，您必须确认自己的账号支持信用支付，否则将返回`InvalidPayMethod`的错误提示。

 |
|Ipv6AddressCount|Integer|否|1|为弹性网卡指定随机生成的IPv6地址数量。

 **说明：** 您不能同时指定参数`Ipv6Addresses.N`和`Ipv6AddressCount`。

 |
|PrivateIpAddress|String|否|172.16.236.14X|实例私网IP地址。该IP地址必须为VSwitchId网段的子集网址。

 **说明：** 设置`PrivateIpAddress`时，`Amount`参数取值只能为1。

 |
|Ipv6Address.N|RepeatList|否|Ipv6Address.1=2001:db8:1234:1a00::\*\*\*|为弹性网卡指定一个或多个IPv6地址。目前，N的取值范围仅支持1。取值示例：`Ipv6Address.1=2001:db8:1234:1a00::***`

 **说明：** 您不能同时指定参数`Ipv6Addresses.N`和`Ipv6AddressCount`。

 |
|DryRun|Boolean|否|false|是否只预检此次请求。

 -   true：发送检查请求，不会创建实例。检查项包括是否填写了必需参数、请求格式、业务限制和ECS库存。如果检查不通过，则返回对应错误。如果检查通过，则返回错误码`DryRunOperation`。
-   false（默认）：发送正常请求，通过检查后直接创建实例。

 |
|ClientToken|String|否|123e4567-e89b-12d3-a456-426655440000|保证请求幂等性。从您的客户端生成一个参数值，确保不同请求间该参数值唯一。**ClientToken**只支持ASCII字符，且不能超过64个字符。更多详情，请参见[如何保证幂等性](~~25693~~)。

 |
|SecurityGroupIds.N|RepeatList|否|sg-bp15ed6xe1yxeycg7o\*\*\*|将实例同时加入多个安全组。N的取值范围与实例能够加入安全组上限有关，更多详情，请参见[安全组限制](~~101348~~)。

 **说明：** 不支持同时指定SecurityGroupId和SecurityGroupIds.N。

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

 -   default：创建非专有宿主机实例。
-   host：创建专有宿主机实例。若您不指定`DedicatedHostId`，则由阿里云自动选择专有宿主机放置实例。

 默认值：default

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|InstanceIdSets| |\["i-instanceid1", "i-instanceid2", "i-instanceid3"\]|实例ID（`InstanceId`）列表。

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=RunInstances
&RegionId=cn-hangzhou
&InstanceType=ecs.cm4.6xlarge
&SecurityGroupId=sg-securitygroupid
&Amount=3
&<公共请求参数>
```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<RunInstancesResponse>
  <RequestId>04F0F334-1335-436C-A1D7-6C044FE73368</RequestId>
  <InstanceIdSets>
    <InstanceIdSet>
      <InstanceId>i-instanceid1</InstanceId>
      <InstanceId>i-instanceid2</InstanceId>
      <InstanceId>i-instanceid3</InstanceId>
    </InstanceIdSet>
  </InstanceIdSets>
</RunInstancesResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"04F0F334-1335-436C-A1D7-6C044FE73368",
	"InstanceIdSets":{
		"InstanceIdSet":[
			"i-instanceid1",
			"i-instanceid2",
			"i-instanceid3"
		]
	}
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InvalidInstanceType.ValueUnauthorized|The specified InstanceType is not authorized.|指定的实例规格未授权使用。|
|404|InvalidSecurityGroupId|The specified SecurityGroupId is invalid or does not exist.|指定的安全组ID不存在。|
|400|InvalidInstanceType.ValueNotSupported|The specified InstanceType beyond the permitted range.|指定的实例规格不合法（超出可选范围）。|
|404|InvalidSecurityGroupId.NotFound|The SecurityGroupId provided does not exist in our records.|指定的安全组在该用户账号下不存在，请您检查安全组id是否正确。|
|400|InvalidDescription.Malformed|The specified parameter "Description" is not valid.|指定的资源描述格式不合法。长度为2-256个字符，不能以 http:// 和 https:// 开头。|
|400|InvalidInternetChargeType.ValueNotSupported|The specified InternetChargeType is not valid.|指定的实例升降配规格不存在。|
|400|InvalidParameter|The specified parameter "InternetMaxBandwidthOut" is not valid.|指定的 InternetMaxBandwidthOut 参数不合法。|
|400|InvalidHostName.Malformed|The specified parameter "HostName" is not valid.|指定的HostName格式不合法。|
|403|InvalidParams.InstanceNameExceed|The uniqueSuffix takes three naming places, please shorten your InstanceName.|uniqueSuffix参数会占用三个命名空间，请缩短您的实例名称。|
|403|InvalidParams.HostnameExceed|The uniqueSuffix takes three naming places, please shorten your Hostname.|uniqueSuffix参数会占用三个命名空间，请缩短您的主机名称。|
|400|InvalidPassword.Malformed|The specified parameter "Password" is not valid.|指定的 Password 参数不合法。|
|400|InvalidPasswordParam.Mismatch|The input password should be null when passwdInherit is true.|启用PasswdInherit后，不允许指定用户名密码。|
|400|InvalidSystemDiskCategory.ValueNotSupported|The specified parameter "SystemDisk.Category" is not valid.|指定的 SystemDisk.Category 不合法。|
|400|InvalidDiskName.Malformed|The specified parameter "SyatemDisk.DiskName or DataDisk.n.DiskName" is not valid.|磁盘名称格式不正确。长度为2-128个字符，以英文字母或中文开头，可包含数字，"."，"\_"或"-"。 不能以 http:// 和 https:// 开头。|
|400|InvalidDiskDescription.Malformed|The specified parameter "SyatemDisk.DiskDescription" or "DataDisk.n.Description" is not valid.|参数 SyatemDisk.DiskDescription 或 DataDisk.n.Description 不合法。|
|400|InvalidDataDiskSize.ValueNotSupported|The specified DataDisk.n.Size beyond the permitted range, or the capacity of snapshot exceeds the size limit of the specified disk category.|指定的数据盘大小已超过最大允许值。|
|400|InvalidDataDiskCategory.ValueNotSupported|The specified parameter "DataDisk.n.Category" is not valid.|指定的参数 DataDisk.n.Category 不合法。|
|404|InvalidDataDiskSnapshotId.NotFound|The specified parameter "DataDisk.n.SnapshotId" is not valid.|指定的参数 DataDisk.n.SnapshotId 不合法。|
|400|InvalidDataDevice.Malformed|The specified parameter "DataDisk.n.Device" is not valid.|指定的参数 DataDisk.n.Device 不合法。|
|400|InvalidNodeControllerId.Malformed|The specified parameter "NodeControllerId" is not valid.|指定的 NodeControllerId 不合法。|
|400|InvalidInnerIpAddress.Malformed|The specified parameter "InnerIpAddress" is not valid.|指定的 DiskDeviceMapping.n.DiskImageSize 超出最大限值。|
|400|InvalidInnerIpAddress.Unusable|The specified InnerIpAddress is already used or not found in usable ip range.|指定的 InnerIpAddress 不可用。|
|400|InvalidParameter.Conflict|The specified image does not support the specified instance type.|指定的镜像不能用于指定的实例规格。|
|400|ImageNotSupportCloudInit|The specified image does not support cloud-init.|指定的镜像不支持 cloud-init。|
|400|InvalidSnapshotId.BasedSnapshotTooOld|The specified snapshot is created before 2013-07-15.|指定的快照创建于 2013-07-15 之前。|
|400|QuotaExceed.AfterpayInstance|Living afterpay instances quota exceeded.|活跃的按量付费实例数已达上限。|
|403|ImageNotSubscribed|The specified image has not be subscribed.|指定的镜像未在镜像市场订阅。|
|403|InvalidSystemDiskCategory.ValueUnauthorized|The disk category is not authorized.|该磁盘类别未经授权。|
|403|InvalidSnapshotId.NotReady|The specified snapshot has not completed yet.|指定的快照未完成。|
|403|InstanceDiskCategoryLimitExceed|The total size of specified disk category in an instance exceeds.|磁盘种类总容量超过实例限制。|
|403|InvalidDevice.InUse|The specified device has been occupied.|指定的设备已经挂载了磁盘。|
|403|ImageRemovedInMarket|The specified market image is not available, Or the specified user defined image includes product code because it is based on an image subscribed from marketplace, and that image in marketplace includeing exact the same product code has been removed.|指定的云市场镜像不可用。|
|404|InvalidClusterId.NotFound|The ClusterId provided does not exist in our records.|指定的 ClusterId 不存在。|
|403|CategoryNotSupported|The specified zone does not offer the specified disk category.|指定的可用区没有提供该磁盘种类。|
|400|InvalidInstanceName.Malformed|The specified parameter "InstanceName" is not valid.|指定的实例名称格式不合法。长度为2-128个字符，以英文字母或中文开头，可包含数字，"."，"\_"或"-"。 不能以 http:// 和 https:// 开头。|
|400|InvalidDiskDescription.Malformed|The specified parameter "SyatemDisk.DiskDescription or DataDisk.n.Description" is not valid.|参数 SyatemDisk.DiskDescription 或 DataDisk.n.Description 不合法。|
|403|QuotaExceed.PortableCloudDisk|The quota of portable cloud disk exceeds.|可卸载磁盘数量已达上限。|
|500|InternalError|The request processing has failed due to some unknown error.|内部错误，请重试。如果多次尝试失败，请提交工单|
|400|InvalidParameter.Conflict|The speicified region and cluster do not match.|指定的地域与指定的集群不匹配。|
|403|SecurityGroupInstanceLimitExceed|Exceeding the allowed amount of instances of a security group.|安全组的实例数已达上限。|
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
|403|Forbbiden|User not authorized to operate on the specified resource.|用户未被授权操作指定的资源。|
|403|DeleteWithInstance.Conflict|The specified disk is not a portable disk and cannot be set to DeleteWithInstance attribute.|指定的磁盘不是可卸载磁盘，不支持随实例释放。|
|404|InvalidImageId.NotFound|The specified ImageId does not exist.|指定的镜像在该用户账号下不存在，请您检查镜像id是否正确。|
|403|InstanceDiskNumLimitExceed|The number of specified disk in an instance exceeds.|实例下磁盘数目超过限制。|
|403|IoOptimized.NotSupported|The specified image is not support IoOptimized Instance.|指定的镜像不支持 I/O 优化型实例。|
|404|IoOptimized.NotSupported|The specified instancetype is not support IoOptimized instance|指定的实例规格不支持 I/O 优化。|
|403|InvalidDiskSize.TooSmall|Specified disk size is less than the size of snapshot|指定的磁盘容量小于快照容量。|
|404|InvalidInstanceChargeType.NotFound|The InstanceChargeType does not exist in our records|指定的实例升降配规格不存在。|
|400|MissingParamter|The specified parameter "Period" is not null.|参数 Period 不得为空。|
|400|InvalidPeriod|The specified period is not valid.|指定的时段不合法。|
|403|InvalidDiskCategory.Mismatch|The specified disk categories combination is not supported.|不支持的磁盘种类搭配。|
|403|IoOptimized.NotSupported|Vpc is not support IoOptimized instance.|该 VPC 不支持 I/O 优化型实例。|
|400|InvalidDataDiskCategory.ValueNotSupported|The specified parameter " DataDisk.n.Category " is not valid.|指定的磁盘类型无效。|
|400|InvalidSystemDiskCategory.ValueNotSupported|The specified parameter " SystemDisk.Category " is not valid.|指定的磁盘类型无效。|
|403|InvalidDiskCategory.NotSupported|The specified disk category is not support the specified instance type.|指定的磁盘种类不支持该实例规格。|
|400|InstanceDiskCategoryLimitExceed|The specified DataDisk.n.Size beyond the permitted range, or the capacity of snapshot exceeds the size limit of the specified disk category.|指定的数据盘大小已超过最大允许值。|
|403|QuotaExceed.BuyImage|The specified image is from the image market?You have not bought it or your quota has been exceeded.|尚未从镜像市场购买指定的镜像，或已达上限。|
|404|DependencyViolation.IoOptimized|The specified instancetype must be IoOptimized instance.|指定的实例规格必须为 I/O 优化实例，请您检查实例规格是否正确。|
|404|PaymentMethodNotFound|No payment method has been registered on the account.|账户尚未注册支付方式。|
|400|InvalidInstanceType.ValueNotSupported|InternetMaxBandwidthOut should be set.|必须设置 InternetMaxBandwidthOut 参数。|
|400|InvalidInstanceType.ValueNotSupported|instancetype is not valid.|指定的 InstanceType 不合法。|
|400|InvalidClientToken.ValueNotSupported|clienttoken is not valid.|指定的 ClientToken 不合法。|
|400|InvalidIoOptimize.ValueNotSupported|The specified IoOptimize is not valid.|指定的I/O优化型实例无效。|
|400|InvalidHostName.Malformed|The specified parameter HostName is not valid.|指定的参数 HostName 不合法。|
|404|HOSTNAME\_ILLEGAL|hostname is not valid.|指定的主机名不合法。|
|400|InvalidInternetMaxBandwidthOut.Malformed|The specified parameter internetMaxBandwidthOut is not valid.|指定的 InternetMaxBandwidthOut 参数不合法。|
|400|InvalidInternetMaxBandwidthIn.Malformed|The specified parameter internetMaxBandwidthIn is not valid.|指定的 InternetMaxBandwidthIn 参数不合法。|
|400|InvalidSnapshotId.NotFound|The specified parameter SnapshotId is not exist.|指定的快照不存在，请您检查快照是否正确。|
|400|InvalidTagKey.Malformed|The specified Tag.n.Key is not valid.|指定的标签键不合法。|
|400|InvalidTagValue.Malformed|The specified Tag.n.Value is not valid.|指定的标签值不合法。|
|403|InvalidResourceId.NotSupported|The specified ResourceId does not support tagging.|指定的资源 ID 不支持标记。|
|400|InvalidTag.Mismatch|The specified Tag.n.Key and Tag.n.Value are not match.|指定的 Tag.n.Key 和 Tag.n.Value 不匹配。|
|400|InvalidTagCount|The specified tags are beyond the permitted range.|指定的标记超出取值范围。|
|400|InvalidMinAmount.Malformed|The specified parameter MinAmount is not valid.|指定的 MinAmount 无效，请您检查该参数是否正确。|
|400|InvalidMaxAmount.Malformed|The specified parameter MaxAmount is not valid.|指定的 MaxAmount 不合法。|
|400|InvalidAutoReleaseTime.Malformed|The specified parameter AutoReleaseTime is not valid.|自动释放格式错误。请您按照 ISO8601 标准表示，并需要使用 UTC 时间，格式为：yyyy-MM-ddTHH:mm:ssZ。|
|400|InvalidPrivateIpAddress.Malformed|The specified parameter PrivateIpAddress is not valid.|指定的 PrivateIpAddress 不合法。|
|400|InvalidInnerIpAddress.Malformed|The specified parameter InnerIpAddress is not valid.|指定的 InnerIpAddress 参数不合法。|
|404|InvalidSystemDiskSize.LessThanImageSize|The specified parameter SystemDisk.Size is less than the image size.|指定的参数 SytemDisk.Size 小于镜像文件大小数值。|
|404|InvalidSystemDiskSize.LessThanMinSize|The specified parameter SystemDisk.Size is less than the min size.|指定的系统盘小于最低容量。|
|404|InvalidSystemDiskSize.MoreThanMaxSize|The specified parameter SystemDisk.Size is more than the max size|指定的 SystemDisk.Size 超过最大值。|
|403|OperationDenied|The specified RegionId does not support the creation of the network type ECS instance.|指定的地域 ID 不支持创建网络类型的 ECS 实例，请您确认该网络类型在此地域有库存。|
|400|OperationDenied.NoVlan|The specified parameter "VlanId" is not valid or vlan has not enough IP address.|指定的 VLAN ID 不合法，或已超出最大 IP 地址数限制。|
|403|OperationDenied.ImageNotValid|The specified Image is disabled or is deleted.|指定的镜像不存在。|
|403|OperationDenied.SnapshotNotValid|The specified snapshot is not allowed to create disk.|指定的快照不支持创建磁盘。|
|403|OperationDenied.SnapshotNotAllowed|The specified snapshot is not allowed to create disk.|指定的快照不支持创建磁盘。|
|403|OperationDenied.ZoneNotAllowed|The creation of Instance to the specified Zone is not allowed.|指定的可用区不支持创建实例。|
|403|OperationDenied.ZoneSystemCategoryNotMatch|The specified Zone or cluster does not offer the specified disk category or the speicified zone and cluster do not match.|指定的可用区或集群中不存在指定磁盘类别，或指定的可用区与集群不匹配。|
|403|OperationDenied.ResourceControl|The specified region is in resource control, please try later.|指定的地域正在资源管理中，请稍后重试。|
|403|OperationDenied.NoStock|The resource is out of usage.|该实例不在运行状态，请您启动实例或检查操作是否合理。|
|403|OperationDenied.SnapshotParamsNotValid|The capacity of snapshot exceeds the size limit of the specified disk category or the specified category is not authorizied.|快照容量已达上限或用户未被授权指定类别。|
|404|OperationDenied.CreatingConflict|Another Instance has been creating|不允许创建新的实例。|
|403|OperationDenied.DiskTypeNotSupport|The type of the disk does not support the operation|制定操作不合法。|
|400|OperationDenied.QuotaExceed|The quota of tags on resource is beyond permitted range.|资源标签已达上限。|
|400|Account.Arrearage|Your account has been in arrears.|账户余额不足，请先充值再操作。|
|403|InvalidUserData.Forbidden|User not authorized to input the parameter "UserData", please apply for permission "UserData"|您未被授权设置UserDat。|
|400|InvalidUserData.SizeExceeded|The specified parameter "UserData" exceeds the size.|指定的 UserData 超过大小限制。|
|400|InvalidUserData.NotSupported|TThe specified parameter "UserData" only support the vpc and IoOptimized Instance.|指定的 UserData 仅支持 VPC 和 I/O 优化型实例。|
|400|InvalidUserData.NotSupported|The specified parameter "UserData" only support the vpc and IoOptimized Instance.|指定的 UserData 仅支持 VPC 和 I/O 优化型实例。|
|400|InvalidUserData.Base64FormatInvalid|The specified UserData is not valid|指定的 UaseData 不合法。|
|404|InvalidZoneId.NotFound|The specified zoneId does not exist.|指定的可用区 ID 不存在。|
|403|Zone.NotOpen|The specified zone is not granted to you to buy resources yet.|用户未被授权购买指定的可用区的资源。|
|403|Zone.NotOnSale|The resource in the specified zone is no longer available for sale. Please try other regions and zones.|指定的可用区暂停售卖。|
|403|InvalidClusterId.NotFound|The specified clusterId does not exist.|指定的 ClusterId 不存在。|
|403|InvalidResourceType.NotSupported|This resource type is not supported. Please try other resource types.|不支持指定的资源类型。|
|403|OperationDenied.NoStock|The resource is out of stock in the specified zone. Please try other types, or choose other regions and zones.|指定的可用区暂停售卖。|
|403|InvalidInstanceType.ZoneNotSupported|The specified zone does not support this instancetype.|指定的可用区里不支持指定的 InstanceType。|
|400|InstanceDiskNumber.LimitExceed|The total number of specified disk in an instance exceeds.|实例下磁盘数目超过限制。|
|400|InvalidDiskCategory.ValueNotSupported|The specified parameter "DiskCategory" is not valid.|参数 DiskCategory 不合法。|
|400|InvalidSpotStrategy|The specified SpotStrategy is not valid.|竞价实例不支持转换|
|400|InvalidSpotPriceLimit|The specified SpotPriceLimitis not valid.|指定的 SpotPriceLimit 不合法。|
|400|InvalidSpotDuration|The specified SpotDuration is not valid.|指定的 SpotDuration 不合法。|
|400|InvalidSpotAuthorized|The specified Spot param is unauthorized.|指定的 Spot 未获得授权。|
|400|InvalidSpotPrepaid|The specified Spot type is not support PrePay Instance.|指定的 Spot 类型不支持包年包月实例。|
|400|InvalidSpotAliUid|The specified UID is not authorized to use SPOT instance.|指定的 UID 无权使用 SPOT 实例。|
|400|InvalidParameter.Bandwidth|%s|参数不支持。|
|400|InvalidDataDiskCategory.ValueNotSupported|%s|参数不支持。|
|400|InvalidSystemDiskCategory.ValueNotSupported|%s|参数不支持。|
|400|InvalidParameter.Conflict|%s|参数冲突。|
|400|InvalidInternetChargeType.ValueNotSupported|%s|参数不支持。|
|400|InvalidInstanceType.ValueNotSupported|%s|实例类型属性不正确。|
|403|InstanceType.Offline|%s|实例规格不能使用。|
|400|RegionUnauthorized|%s|指定地域不支持。|
|400|Zone.NotOnSale|%s|可用区关闭。|
|400|InvalidSystemDiskSize.ValueNotSupported|%s|参数不支持。|
|400|InvalidDataDiskSize.ValueNotSupported|%s|参数不支持。|
|404|InvalidKeyPairName.NotFound|The specified parameter "KeyPairName" does not exist in our records.|密钥对不存在,|
|403|DependencyViolation.WindowsInstance|The instance creating is window, cannot use ssh key pair to login.|Windows操作系统不支持SSH密钥对。|
|400|InvalidInstanceType.ValueNotSupported|The specified parameter "KeyPairName" only support IoOptimized Instance.|非I/O优化实例不支持密钥对。|
|404|InvalidResourceGroup.NotFound|The ResourceGroup provided does not exist in our records.|资源组并不在记录中。|
|403|InvalidNetworkType.MismatchRamRole|A RAM role can?t be used for classic instance.|经典网络类型实例不支持RAM角色。|
|403|InvalidUser.PassRoleForbidden|The RAM user does not have the privilege to pass a RAM role.|该 RAM 用户无权传递 RAM 角色。|
|404|InvalidRamRole.NotFound|The specified parameter "RAMRoleName" does not exist.|指定的RAM角色不存在。|
|404|InvalidLaunchTemplate.NotFound|%s|指定的模板名称未找到。|
|404|InvalidLaunchTemplateVersion.NotFound|%s|指定的模板版本未找到。|
|400|InvalidInstanceType.ElasticNetworkInterfaceNotSupported|The specified instance type does not support Elastic Network Interface, you can not attach Elastic Network Interface to generation I instances.|指定的实例规格不支持弹性网卡。|
|400|InvalidParameter.EncryptedIllegal|%s|参数不支持（加密盘）。|
|400|InvalidParameter.EncryptedNotSupported|%s|参数不支持（加密盘）。|
|400|InvalidParameter.Encrypted.KmsNotEnabled|The encrypted disk need enable KMS|加密磁盘需要启用密钥管理服务。|
|500|InternalError|The request processing has failed due to some unknown error, exception or failure.|发生未知错误。|
|403|Forbidden.RiskControl|This operation is forbidden by Aliyun RiskControl system.|该操作被风险控制系统禁止。|
|403|InvalidInstance.UnPaidOrder|The specified Instance has unpaid order.|指定的实例有未支付的订单，请您先支付再进行操作。|
|403|RealNameAuthenticationError|Your account has not passed the real-name authentication yet.|您的帐户尚未通过实名认证，请先实名认证后再操作。|
|403|InvalidInstanceType.NotSupported|The specified InstanceType is not Supported.|不支持指定的 InstanceType。|
|403|InvalidPayMethod|The specified pay method is not valid.|没有可用的付费方式|
|403|InvalidAccountStatus.NotEnoughBalance|Your account does not have enough balance.|账号余额不足，请您先充值再进行该操作。|
|400|InvalidSpotPriceLimit.LowerThanPublicPrice|The specified parameter "spotPriceLimit" can't be lower than current public price.|指定的参数sotPriceLimit不能低于目前的公开价格。|
|400|InvalidRelationResource.NotFound|The relation resource has been deleted.|关联资源已被删除。|
|400|IncorrectRecycleBinStatus|The operation is not permitted due to resource status.|资源状态不支持操作。|
|400|InvalidHpcClusterId.Unnecessary|The specified HpcClusterId is unnecessary|无需指定HPC集群ID。|
|400|InvalidVSwitchId.Necessary|The VSwitchId is necessary|缺失必需参数。|
|400|InvalidHpcClusterId.Necessary|The HpcClusterId is necessary|缺失必需参数。|
|400|InvalidHpcClusterId.NotFound|The specified HpcClusterId is not found|指定的参数不存在。|
|400|InvalidHpcClusterId.Creating|The specified HpcClusterId is creating|指定的HPC集群正在创建中。|
|404|InvalidVSwitchId.NotExist|%s|指定的VSwitch不存在。|
|403|ImageNotSupportInstanceType|The specified image does not support the specified InstanceType.|指定的镜像不支持改实例规格。|
|400|InvalidSecurityGroup.NotInDefaultVpc|%s|指定的安全组不是DefaultVPC中的安全组。|
|400|VpcNotFound|Vpc is not found according to the specified VSwitch or the vpc does not belong to you.|指定的VPC不存在。|
|400|InvalidSystemDiskSize.ImageNotSupportResize|The specified image does not support resize.|指定的镜像不支持扩容。|
|403|OperationDenied.InvalidNetworkType|%s|网络类型不支持。|
|400|InvalidSpotInterruptionBehavior|%s|SpotInterruptionBehavior不支持。|
|403|InvalidSpotInterruptionBehavior.ClassicNetworkNotSupport|The specified SpotInterruptionBehavior does not support Classic network Instance.|抢占式实例不能是经典网络类型。|
|403|InvalidSpotInterruptionBehavior.LocalDiskNotSupport|The specified SpotInterruptionBehavior does not support local disk instance.|抢占是实例不支持本地盘实例。|
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
|400|MissingParameter|The input parameter ImageId that is mandatory for processing this request is not supplied.|缺失必需参数。|
|400|MissingParameter|The input parameter InstanceType that is mandatory for processing this request is not supplied.|缺失必需参数。|
|400|ChargeTypeViolation.PostPaidDedicatedHost|Prepaid instance onto postpaid dedicated host is not allowed.|专有宿主机不支持更换计费方式。|
|400|InvalidParam.NetworkInterface|%s|指定的参数无效。|
|403|OperationDenied.ImageNotValid|%s|镜像不支持此操作。|
|403|QuotaExceed.PostPaidDisk|Living postPaid disks quota exceeded.|按量付费磁盘数量已超出允许数量。|
|401|InvalidRamRole.NotEcsRole|The specified ram role is not authorized for ecs, please check your role policy.|RAM角色不具备访问ECS的权限。|
|403|InvalidParameter.NotMatch|%s|参数冲突。|
|403|InvalidVSwitch.DefaultVSwitchNotSupport|The specified zone in vpc can't support create default vSwitch.|可用区内的VPC不支持创建默认交换机。|
|400|InvalidParameter.CreditSpecification|The specified CreditSpecification is not supported in this region.|当前地域不支持指定的CreditSpecification。|
|404|InvalidMarketImage.NotFound|The specified marketplace image does not exist, please change the imageId and try again.|云市场不存在指定的镜像。|
|400|IncorrectVpcStatus|Current VPC status does not support this operation.|当前专有网络VPC的状态无法支持这个操作。|
|400|InvalidInstanceType.NotSupported|The specified instanceType is not supported by the deployment set.|部署集不支持该实例规格。|
|400|InvalidVpcZone.NotSupported|The specified operation is not allowed in the zone to which your VPC belongs, please try in other zones.|指定可用区不允许该操作。|
|400|IncorrectDefaultVpcStatus|The status of the default VPC is invalid.|默认VPC的状态不正确。|
|404|DeploymentSet.NotFound|The specified deployment set does not exist.|指定的部署集不存在。|
|400|InvalidAutoRenewPeriod.ValueNotSupported|The specified autoRenewPeriod is invalid.|指定的自动续费时长无效。|
|403|OperationDenied.LocalDiskUnsupported|The configuration change is not allowed when the specified instance has local disks mounted.|实例挂载本地盘后不支持规格变配。|
|403|OperationDenied.InconsistentNetwork|The specified security group and vswitch are not in the same vpc.|安全组和交换机的VPC必须相同。|
|403|OperationDenied|If the network segment of the vswitch is the same as that of its VPC. Therefore, the VPC cannot create other vswitchs across the region.|VPC与虚拟交换机的网段相同，无法在多可用区内创建其他交换机。|
|403|DefaultVswitch.Existed|The default vswitch for VPC already exists.|VPC已存在默认交换机。|
|400|InvalidMarketImageChargeType.NotSupport|The specified chargeType of marketImage is unsupported.|云市场镜像的计费方式无效。|
|403|OperationDenied.NoStock|The requested resource is sold out in the specified zone; try other types of resources or other regions and zones.|库存不足。|
|403|IncorrectInstanceStatus|The current status of the resource does not support this operation.|该资源目前的状态不支持此操作。|
|403|CategoryViolation|The specified instance does not support this operation because of its disk category.|挂载有本地磁盘的实例不支持升降配。|
|400|InvalidPeriodType.ValueNotSupported|The specified parameter PeriodType is invalid.|指定的PeriodType无效。|
|403|ResourcesNotInSameZone|The specified instance and dedicated host are not in the same zone.|实例和专有宿主机必须在同一地域下。|
|403|InvalidDisk.SystemDiskSize|The specified SystemDiskSize beyond the permitted range.|系统盘大小超出最大允许值。|
|400|InvalidClientToken.ValueNotSupported|The ClientToken provided is invalid.|指定的 ClientToken 不合法。|
|400|OperationDenied|The current user does not support this operation.|当前用户不支持该操作。|
|400|IncorrectImageStatus|The specified marketplace image is not available.|指定的市场镜像不可用。|
|403|InsufficientBalance|Your account does not have enough balance.|账户余额不足，请先充值再操作。|
|400|InvalidInstanceType.ValueNotSupported|The specified InstanceType does not exist or beyond the permitted range.|指定的实例规格不支持。|
|400|InvalidParam.Tenancy|The specified Tenancy is invalid.|您指定的Tenancy参数值无效。|
|403|MaxEniIpv6IpsCountExceeded|%s|弹性网卡挂载 IPv6 个数达到上限。|
|403|InvalidIp.IpRepeated|%s|指定的 IP 重复。|
|403|InvalidIp.IpAssigned|%s|指定的 IP 已被分配。|
|403|InvalidIp.Address|%s|指定的 IPv6 地址不合法。|
|403|InvalidOperation.Ipv4CountExceeded|%s|IPv4 个数达到上限。|
|403|InvalidOperation.Ipv6CountExceeded|%s|IPv6 个数达到上限。|
|403|InvalidOperation.Ipv6NotSupport|%s|实例规格不支持 IPv6。|
|403|InvalidVSwitch.Ipv6NotTurnOn|%s|交换机未开启 IPv6 功能。|
|403|InvalidParam.Amount|%s|指定的Amount参数无效。|
|403|InvalidVSwitchId.IpInvalid|%s|指定的私网ip不合法。|
|403|Forbidden.RegionId|%s|前区域暂不支持此功能。|
|400|IncorrectVpcStatus|The current status of vpc does not support this operation.|VPC当前的状态不支持该操作。|
|403|QuotaExceed.DeploymentSetInstanceQuotaFull|instance quota in one deployment set exceeded.|当前部署集内的实例数量已满额。|
|403|InvalidRegion.NotSupport|The specified region does not support byok.|该地域不支持BYOK。|
|403|UserNotInTheWhiteList|The user is not in byok white list.|您暂时不能使用BYOK服务。|
|400|InvalidParameter.EncryptedIllegal|The specified parameter Encrypted must be true when kmsKeyId is not empty.|设置KmsKeyId后，您必须开启加密属性。|
|400|IoOptimized.NotSupported|The specified instance must be IoOptimized instance when kmsKeyId is not empty.|设置KmsKeyId后，您必须使用I/O优化实例。|
|404|InvalidParameter.KMSKeyId.NotFound|The specified KMSKeyId does not exist.|指定的参数值不存在。|
|403|InvalidParameter.KMSKeyId.KMSUnauthorized|ECS service have no right to access your KMS.|ECS未被授权访问您的KMS资源。|
|403|SecurityRisk.3DVerification|We have detected a security risk with your default credit or debit card. Please proceed with verification via the link in your email.|您的支付方式有安全风险，请根据通知指导排查。|
|400|Duplicate.TagKey|The Tag.N.Key contain duplicate key.|标签键中存在重复的键。|
|404|InvalidSecurityGroupId.NotFound|%s|指定的安全组ID不存在。|
|404|InvalidDiskIds.NotPortable|The specified DiskId is not portable.|指定的磁盘是不可移植的。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ecs)查看更多错误码。

