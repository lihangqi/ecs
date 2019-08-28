# CreateLaunchTemplateVersion {#doc_api_Ecs_CreateLaunchTemplateVersion .reference}

调用CreateLaunchTemplateVersion根据指定的实例启动模板创建一个版本。

## 接口说明 {#description .section}

每个实例启动模板最多创建30个版本。我们不提供模板修改接口，但是提供版本迭代接口（`CreateLaunchTemplateVersion`）。当您想修改某个版本的参数时，能通过新建模板版本的方式修改。更多详情，请参见[CreateLaunchTemplate](~~74686~~)。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=CreateLaunchTemplateVersion&type=RPC&version=2014-05-26)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|RegionId|String|是|cn-hangzhou|地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。

 |
|Action|String|否|CreateLaunchTemplateVersion|系统规定参数。取值：CreateLaunchTemplateVersion

 |
|AutoReleaseTime|String|否|2018-01-01T12:05:00Z|自动释放时间。按照[ISO8601](~~25696~~)标准表示，并需要使用UTC时间。格式为：yyyy-MM-ddTHH:mm:ssZ。

 -   如果秒（`ss`）取值不是`00`，则自动取为当前分钟（`mm`）开始时。
-   最短释放时间为当前时间半小时之后。
-   最长释放时间不能超过当前时间三年。

 |
|DataDisk.N.Category|String|否|cloud\_ssd|数据盘n的云盘种类。取值范围：

 -   cloud：普通云盘
-   cloud\_efficiency：高效云盘
-   cloud\_ssd：SSD云盘
-   cloud\_essd：ESSD云盘

 |
|DataDisk.N.DeleteWithInstance|Boolean|否|true|表示数据盘是否随实例释放。

 |
|DataDisk.N.Description|String|否|FinanceDept|实例描述。长度为2~256个英文或中文字符，不能以http://和https://开头。

 |
|DataDisk.N.DiskName|String|否|cloud\_ssdData|数据盘名称。长度为2~128个英文或中文字符。必须以大小字母或中文开头，不能以http://和https://开头。可以包含数字、半角冒号（:）、下划线（\_）或者连字符（-）。

 |
|DataDisk.N.Encrypted|String|否|false|数据盘n是否加密。

 |
|DataDisk.N.Size|Integer|否|2000|第n个数据盘的容量大小，n的取值范围为1~16，内存单位为GiB。取值范围：

 -   cloud：5~2000
-   cloud\_efficiency：20~32768
-   cloud\_ssd：20~32768
-   cloud\_essd：20~32768

 该参数的取值必须大于等于参数`SnapshotId`指定的快照的大小。

 |
|DataDisk.N.SnapshotId|String|否|s-bp17441ohwka0yuhx\*\*\*|创建数据盘n使用的快照。n的取值范围为1~16。指定参数`DataDisk.N.SnapshotId`后，参数`DataDisk.N.Size`会被忽略，实际创建的云盘大小为指定的快照的大小。

 不能使用早于2013年7月15日（含）创建的快照，请求会报错被拒绝。

 |
|Description|String|否|FinaceDept|实例描述。长度为2~256个英文或中文字符，不能以http://和https://开头。

 |
|EnableVmOsConfig|Boolean|否|false|是否启用实例操作系统配置。

 |
|HostName|String|否|JoshuaHost|云服务器的主机名。

 -   点号（.）和短横线（-）不能作为首尾字符，更不能连续使用。
-   Windows实例：字符长度为2~15，不支持点号（.），不能全是数字。允许大小写英文字母、数字和短横线（-）。
-   其他类型实例（Linux等）：字符长度为2~64，支持多个点号（.），点之间为一段，每段允许大小写英文字母、数字和短横线（-）。

 |
|ImageId|String|否|win2008r2\_64\_ent\_sp1\_en-us\_40G\_alibase\_20170915.vhd|镜像ID，启动实例时选择的镜像资源。您可以通过[DescribeImages](~~25534~~)查询您可以使用的镜像资源。

 |
|ImageOwnerAlias|String|否|system|镜像来源。

 **说明：** 该参数即将被弃用，为提高兼容性，请尽量使用其他参数。

 |
|InstanceChargeType|String|否|PrePaid|实例的计费方式。取值范围：

 -   PrePaid：包年包月。选择该类计费方式时，您必须确认自己的账号支持余额支付和信用支付，否则将返回`InvalidPayMethod`的错误提示。
-   PostPaid：按量付费。

 |
|InstanceName|String|否|JoshuaHost|实例名称。长度为2~128个英文或中文字符。必须以大小字母或中文开头，不能以http://和https://开头。可以包含数字、半角冒号（:）、下划线（\_）或者连字符（-）。

 |
|InstanceType|String|否|ecs.g5.large|实例的资源规格。更多详情，请参见[实例规格族](~~25378~~)，也可以调用[DescribeInstanceTypes](~~25620~~)接口获得最新的规格表。

 |
|InternetChargeType|String|否|PayByTraffic|网络计费方式。取值范围：

 -   PayByBandwidth：按固定带宽计费
-   PayByTraffic：按使用流量计费

 |
|InternetMaxBandwidthIn|Integer|否|200|公网入带宽最大值，单位为Mbit/s。取值范围：1~200

 |
|InternetMaxBandwidthOut|Integer|否|5|公网出带宽最大值，单位为Mbit/s。取值范围：0~100

 |
|IoOptimized|String|否|optimized|是否为I/O优化实例。取值范围：

 -   none：非I/O优化
-   optimized：I/O优化

 |
|KeyPairName|String|否|Instancetest|密钥对名称。

 -   Windows实例，忽略该参数。即使填写了该参数，仍旧只执行`Password`的内容。
-   Linux实例的密码登录方式会被初始化成禁止。

 |
|LaunchTemplateId|String|否|lt-m5eiaupmvm2op9dxxxxx|启动模板ID。更多详情，请调用[DescribeLaunchTemplates](~~73759~~)。您必须指定`LaunchTemplateId`或`LaunchTemplateName`以确定启动模板。

 |
|LaunchTemplateName|String|否|JoshuaWinPrePaid|实例启动模板名称。长度为2~128个英文或中文字符。必须以大小字母或中文开头，不能以http://和https://开头。可以包含数字、半角冒号（:）、下划线（\_）或者连字符（-）。

 |
|NetworkInterface.N.Description|String|否|FinnanceDept|弹性网卡描述信息。长度为2~256个英文或中文字符，不能以http://和https://开头。

 **说明：** 弹性网卡相关请求参数`NetworkInterface.N`的N取值不能大于1。

 |
|NetworkInterface.N.NetworkInterfaceName|String|否|FinnanceJoshua|弹性网卡名称。

 **说明：** 弹性网卡相关请求参数`NetworkInterface.N`的N取值不能大于1。

 |
|NetworkInterface.N.PrimaryIpAddress|String|否|192.168.2.XXX|弹性网卡的主私有IP地址。

 **说明：** 弹性网卡相关请求参数`NetworkInterface.N`的N取值不能大于1。

 |
|NetworkInterface.N.SecurityGroupId|String|否|sg-bp15ed6xe1yxeycg7\*\*\*|弹性网卡所属安全组的ID。弹性网卡的安全组和实例的安全组必须在同一个VPC下。

 **说明：** 弹性网卡相关请求参数`NetworkInterface.N`的N取值不能大于1。

 |
|NetworkInterface.N.VSwitchId|String|否|vsw-bp1s5fnvk4gn2tws03\*\*\*|弹性网卡所属的虚拟交换机ID。实例与弹性网卡必须在同一VPC的同一可用区中，可以分属于不同交换机。

 **说明：** 弹性网卡相关请求参数`NetworkInterface.N`的N取值不能大于1。

 |
|NetworkType|String|否|vpc|实例网络类型。取值范围：

 -   classic
-   vpc

 |
|Period|Integer|否|1|购买资源的时长，单位为：月。当参数`InstanceChargeType`取值为`PrePaid`时才生效且为必选值。一旦指定了DedicatedHostId，则取值范围不能超过专有宿主机的订阅时长。取值范围：

 -   `PeriodUnit=Week`时，Period取值：\{“1”, “2”, “3”, “4”\}
-   `PeriodUnit=Month`时，Period取值：\{ “1”, “2”, “3”, “4”, “5”, “6”, “7”, “8”, “9”, “12”, “24”, “36”,”48”,”60”\}

 |
|RamRoleName|String|否|FinanceDept|实例RAM角色名称。您可以使用RAM API [ListRoles](~~28713~~)查询您已创建的实例RAM角色。

 |
|ResourceGroupId|String|否|rg-resourcegroupid|资源组ID。

 |
|SecurityEnhancementStrategy|String|否|Active|是否为操作系统开启安全加固。取值范围：

 -   Active：启用安全加固，只对公共镜像生效。
-   Deactive：不启用安全加固，对所有镜像类型生效。

 |
|SecurityGroupId|String|否|sg-bp15ed6xe1yxeycg7\*\*\*|指定新创建实例所属于的安全组ID。同一个安全组内的实例之间可以互相访问。

 |
|SpotDuration|Integer|否|1|实例保护周期。

 **说明：** 该参数即将被弃用，为提高兼容性，请尽量使用其他参数。

 |
|SpotPriceLimit|Float|否|0.97|设置实例的每小时最高价格。支持最大3位小数。

 |
|SpotStrategy|String|否|NoSpot|按量实例的抢占策略。当参数`InstanceChargeType`取值为`PostPaid`时生效。取值范围：

 -   NoSpot：正常按量付费实例。
-   SpotWithPriceLimit：设置上限价格的抢占式实例。
-   SpotAsPriceGo：系统自动出价，跟随当前市场实际价格。

 |
|SystemDisk.Category|String|否|cloud\_ssd|系统盘的云盘种类。取值范围：

 -   cloud：普通云盘
-   cloud\_efficiency：高效云盘
-   cloud\_ssd：SSD云盘
-   cloud\_essd：ESSD云盘

 |
|SystemDisk.Description|String|否|FinanceDept|系统盘描述。长度为2~256个英文或中文字符，不能以http://和https://开头。

 |
|SystemDisk.DiskName|String|否|cloud\_ssdSystem|系统盘名称。长度为2~128个英文或中文字符。必须以大小字母或中文开头，不能以http://和https://开头。可以包含数字、半角冒号（:）、下划线（\_）或者连字符（-）。

 |
|SystemDisk.Size|Integer|否|40|系统盘大小，单位为GiB。取值范围：20~500

 该参数的取值必须大于或者等于max\{20, ImageSize\}。

 |
|Tag.N.Key|String|否|FinanceDept|实例、块存储和主网卡的标签键。N的取值范围：1~5。一旦传入该值，则不允许为空字符串。最多支持64个字符，不能以aliyun和acs:开头，不能包含http://或者https://。

 |
|Tag.N.Value|String|否|FinanceDept.Joshua|实例、块存储和主网卡的标签值。N的取值范围：1~5。一旦传入该值，可以为空字符串。最多支持128个字符，不能以aliyun和acs:开头，不能包含http://或者https://。

 |
|UserData|String|否|ZWNobyBoZWxsbyBlY\*\*\*|实例自定义数据，需要以Base64方式编码，原始数据最多为16KB。

 |
|VSwitchId|String|否|vsw-bp1s5fnvk4gn2tws03\*\*\*|创建VPC类型实例时需要指定虚拟交换机ID。

 |
|VersionDescription|String|否|LTFinanceJoshua|实例启动模板版本的描述。长度为2~256个英文或中文字符，不能以http://和https://开头。

 |
|VpcId|String|否|vpc-bp12433upq1y5sceni\*\*\*|专有网络VPC ID。

 |
|ZoneId|String|否|cn-hangzhou-g|实例所属的可用区ID。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|LaunchTemplateVersionNumber|Long|2|实例启动模板版本号。

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=CreateLaunchTemplateVersion
&RegionId=cn-hangzhou
&LaunchTemplateId=lt-m5eiaupmvm2op9d*****
&LaunchTemplateName=JoshuaWinPrePaid
&VersionDescription=LTFinanceJoshua
&ImageId=win2008r2_64_ent_sp1_en-us_40G_alibase_20170915.vhd
&InstanceType=ecs.g5.large
&SecurityGroupId=sg-bp15ed6xe1yxeycg7***
&VpcId=vpc-bp12433upq1y5sceni07X
&VSwitchId=vsw-bp1s5fnvk4gn2tws03***
&InstanceName=JoshuaHost
&Description=FinaceDept
&InternetMaxBandwidthIn=200
&InternetMaxBandwidthOut=5
&HostName=JoshuaHost
&ZoneId=cn-hangzhou-g
&SystemDisk.Category=cloud_ssd
&SystemDisk.Size=40
&SystemDisk.DiskName=cloud_ssdSystem
&SystemDisk.Description=FinanceDept
&DataDisk.1.Size=2000
&DataDisk.1.SnapshotId=s-bp17441ohwka0yuhx***
&DataDisk.1.Category=cloud_ssd
&DataDisk.1.Encrypted=false
&DataDisk.1.DiskName=cloud_ssdData
&DataDisk.1.Description=FinanceDept
&DataDisk.1.DeleteWithInstance=true
&IoOptimized=optimized
&NetworkInterface.1.PrimaryIpAddress=192.168.2.XXX
&NetworkInterface.1.VSwitchId=vsw-bp1s5fnvk4gn2tws03***
&NetworkInterface.1.SecurityGroupId=sg-bp15ed6xe1yxeycg7***
&NetworkInterface.1.1etworkInterfaceName=FinnanceJoshua
&NetworkInterface.1.Description=FinnanceDept
&InstanceChargeType=PrePaid
&Period=1
&InternetChargeType=PayByTraffic
&NetworkType=vpc
&UserData=ZWNobyBoZWxsbyBlY3Mh
&KeyPairName=Instancetest
&RamRoleName=FinanceDept
&AutoReleaseTime=2018-01-01T12:05:00Z
&SpotStrategy=NoSpot
&SpotPriceLimit=0.97
&SecurityEnhancementStrategy=Active
&Tag.1.Key=FinanceDept
&Tag.1.Value=FinanceDept.Joshua
&<公共请求参数>
```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<CreateLaunchTemplateVersionResponse>
      <RequestId>04F0F334-1335-436C-A1D7-6C044FExxxxx</RequestId>
      <LaunchTemplateVersionNumber>2</LaunchTemplateVersionNumber>
</CreateLaunchTemplateVersionResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"04F0F334-1335-436C-A1D7-6C044FExxxxx",
	"LaunchTemplateVersionNumber":2
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InvalidRegion.NotExist|%s|指定的Region不存在。|
|403|LaunchTemplateVersionLimitExceed|%s|启动模板版本数量达到上限。|
|404|InvalidLaunchTemplate.NotFound|%s|指定的模板名称未找到。|
|400|MissingParameter|%s|缺失必需参数。|
|400|InvalidParameter|%s|参数格式不正确。|
|400|InvalidDescription.Malformed|The specified parameter "Description" is not valid.|指定的资源描述格式不合法。长度为2-256个字符，不能以 http:// 和 https:// 开头。|
|403|InnerServiceFailed|%s|内部服务调用失败。|
|400|InvalidUserData.SizeExceeded|%s|UserData大小超出限制。|
|400|InvalidUserData.Base64FormatInvalid|%s|指定的模板版本描述格式无效。|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

