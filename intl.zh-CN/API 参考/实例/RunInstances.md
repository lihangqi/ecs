# RunInstances {#RunInstances .reference}

创建一台或多台按量付费实例。

## 描述 {#BestPractice .section}

创建实例前，您可以调用[DescribeAvailableResource](intl.zh-CN/API 参考/地域/DescribeAvailableResource.md#)查看指定地域或者可用区内的资源供给情况。

创建实例会涉及到资源计费，建议您提前了解云服务器ECS的计费方式。更多详情，请参阅[计费概述](../intl.zh-CN/产品定价/计费概述.md#)。

调用该接口时，您需要注意：

-   单次最多能创建100台实例。
-   您可以指定参数`AutoReleaseTime`设置实例自动释放时间。
-   创建成功后会返回实例ID列表，您可以通过API [DescribeInstances](intl.zh-CN/API 参考/实例/DescribeInstances.md#)查询新建实例状态。
-   创建实例前，您需要确保您已经有可用的安全组。更多详情，请参阅[CreateSecurityGroup](intl.zh-CN/API 参考/安全组/CreateSecurityGroup.md#)。
-   创建实例时，默认自动启动实例，直到实例状态变成运行中（`Running`）。
-   创建专有网络VPC类型实例前，您需要预先在相应的阿里云地域 [创建 VPC](../../../../../intl.zh-CN/快速入门/搭建专有网络.md#)。
-   与[CreateInstance](intl.zh-CN/API 参考/实例/CreateInstance.md#)相比，通过`RunInstances`创建的实例如果参数`InternetMaxBandwidthOut`的值大于0，则自动为实例分配公网IP。
-   提交创建任务后，参数不合法或者库存不足的情况下会报错，具体的报错原因参阅[错误码](#ErrorCode)。

**最佳实践**

RunInstances 可以执行批量创建任务，为便于管理与检索，建议您为每批次启动的实例指定标签（Tag.n.Key和Tag.n.Value），并且为主机名（HostName）和实例名称（InstanceName）添加有序后缀（**UniqueSuffix**）。

实例启动模板能免除您每次创建实例时都需要填入大量配置参数，您可以创建实例启动模板（[CreateLaunchTemplate](intl.zh-CN/API 参考/启动模板/CreateLaunchTemplate.md#)）后，在RunInstances请求中指定LaunchTemplateId和LaunchTemplateVersion使用启动模板。

您可以在 [ECS 管理控制台](https://ecs.console.aliyun.com/)创建 ECS 实例时获取 RunInstances 的最佳实践建议。确认订单时，左侧 **API 工作流** 罗列出 RunInstances 能使用的关联 API 以及请求参数的值。右侧提供面向编程语言的 SDK 示例，目前支持 **Java** 和 **Python** 示例。

## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：RunInstances|
|RegionId|String|是|实例所属的地域ID。您可以调用[DescribeRegions](../intl.zh-CN/API 参考/地域/DescribeRegions.md#)查看最新的阿里云地域列表。|
|ZoneId|String|否|实例所属的可用区编号，您可以调用[DescribeZones](intl.zh-CN/API 参考/地域/DescribeZones.md#)获取可用区列表。默认值：系统随机选择。

|
|LaunchTemplateId|String|否|启动模板ID。更多详情，请调用[`DescribeLaunchTemplates`](intl.zh-CN/API 参考/启动模板/DescribeLaunchTemplates.md#)。您必须指定`LaunchTemplateId`或`LaunchTemplateName`以确定启动模板。|
|LaunchTemplateName|String|否|启动模板名称。您必须指定`LaunchTemplateId`或`LaunchTemplateName`以确定启动模板。|
|LaunchTemplateVersion|String|否|启动模板版本。如果您指定了`LaunchTemplateId`或`LaunchTemplateName`而不指定启动模板版本号，则采用默认版本。|
|ImageId|String|否|镜像ID，启动实例时选择的镜像资源。您可以通过[DescribeImages](intl.zh-CN/API 参考/镜像/DescribeImages.md#)查询您可以使用的镜像资源。如果您不指定`LaunchTemplateId`或`LaunchTemplateName`以确定启动模板，`ImageId`为必需参数。

|
|InstanceType|String|否|实例的资源规格。更多详情，请参阅[实例规格族](../intl.zh-CN/产品简介/实例规格族.md#)，也可以调用[DescribeInstanceTypes](intl.zh-CN/API 参考/实例/DescribeInstanceTypes.md#)获得最新的规格列表。如果您不指定`LaunchTemplateId`或`LaunchTemplateName`以确定启动模板，`InstanceType`为必需参数。

|
|CreditSpecification|String|否| 修改突发性能 t5 实例的运行模式。取值范围：

 -   Standard：标准模式，实例性能请参阅 [t5性能约束实例](../intl.zh-CN/产品简介/实例/突发性能实例/t5性能约束实例.md#)。
-   Unlimited：无性能约束模式，实例性能请参阅 [t5无性能约束实例](../intl.zh-CN/产品简介/实例/突发性能实例/t5无性能约束实例.md#)。

 默认值：无。

 |
|SecurityGroupId|String|否|指定新创建实例所属于的安全组ID。同一个安全组内的实例之间可以互相访问，一个安全组最多能管理1000台实例。**说明：** SecurityGroupId决定了实例的网络类型，例如，如果指定安全组的网络类型为专有网络VPC，实例则为VPC类型，并同时需要指定参数VSwitchId。

如果您不指定`LaunchTemplateId`或`LaunchTemplateName`以确定启动模板，`SecurityGroupId`为必需参数。

|
|VSwitchId|String|否|虚拟交换机ID。如果您创建的是VPC类型ECS实例，需要指定虚拟交换机ID。|
|Period|Integer|否|购买资源的时长。当参数`InstanceChargeType`取值为`PrePaid`时才生效且为必选值。一旦指定了 DedicatedHostId，则取值范围不能超过专有宿主机的订阅时长。取值范围：-   `PeriodUnit=Week`时，Period取值：\{“1”, “2”, “3”, “4”\}
-   `PeriodUnit=Month`时，Period取值：\{ “1”, “2”, “3”, “4”, “5”, “6”, “7”, “8”, “9”, “12”, “24”, “36”,”48”,”60”\}

|
|InternetChargeType|String|否|网络计费类型。取值范围：-   PayByTraffic（默认）：按使用流量计费

|
|IoOptimized|String|否|是否为I/O优化实例。取值范围：-   none：非I/O优化
-   optimized：I/O优化

`InstanceType`为[已停售的实例规格](https://www.alibabacloud.com/help/faq-detail/55263.htm) 的规格默认值：none

`InstanceType`为非系列I的规格默认值：optimized

|
|SystemDisk.Category|String|否|系统盘的磁盘种类。取值范围：-   cloud：普通云盘
-   cloud\_efficiency：高效云盘
-   cloud\_ssd：SSD 云盘
-   ephemeral\_ssd：本地 SSD 盘

`InstanceType`为[已停售的实例规格](https://www.alibabacloud.com/help/faq-detail/55263.htm) 的规格且参数`IoOptimized`取值为`none`时，默认值：cloud

其余情况，默认值：cloud\_efficiency

|
|SystemDisk.Size|String|否|系统盘大小，单位为GiB。取值范围：\[20, 500\]该参数的取值必须大于或者等于max\{20, ImageSize\}。默认值：max\{40, 参数ImageId对应的镜像大小\}

|
|SystemDisk.DiskName|String|否|系统盘名称。长度为 \[2, 128\] 个英文或中文字符。必须以大小字母或中文开头，不能以 http:// 和 https:// 开头。可以包含数字、半角冒号（:）、下划线（\_）或者连字符（-）。|
|SystemDisk.Description|String|否|系统盘描述。长度为 \[2, 256\] 个英文或中文字符，不能以 http:// 和 https:// 开头。|
|DataDisk.n.Category|String|否|数据盘n的磁盘种类，`n`的取值范围为\[1, 16\]。取值范围：-   cloud：普通云盘
-   cloud\_efficiency：高效云盘
-   cloud\_ssd：SSD 云盘
-   ephemeral\_ssd：本地 SSD 盘

默认值：cloud|
|DataDisk.n.Size|Integer|否|第n个数据盘的容量大小，`n`的取值范围为 \[1, 16\]，内存单位为GiB。取值范围：-   cloud：\[5, 2000\]
-   cloud\_efficiency：\[20, 32768\]
-   cloud\_ssd：\[20, 32768\]
-   ephemeral\_ssd：\[5, 800\]

该参数的取值必须大于等于参数`SnapshotId`指定的快照的大小。|
|DataDisk.n.SnapshotId|String|否|创建数据盘n使用的快照。`n`的取值范围为\[1, 16\]。指定参数`DataDisk.n.SnapshotId`后，参数`DataDisk.n.Size`会被忽略，实际创建的磁盘大小为指定的快照的大小。不能使用早于2013年7月15日（含）创建的快照，请求会报错被拒绝。|
|DataDisk.n.Encrypted|Boolean|否|数据盘n是否加密，`n`的取值范围为\[1, 16\]。默认值：false

|
|DataDisk.n.DiskName|String|否|数据盘名称，`n`的取值范围为\[1, 16\]。长度为 \[2, 128\] 个英文或中文字符。必须以大小字母或中文开头，不能以 http:// 和 https:// 开头。可以包含数字、半角冒号（:）、下划线（\_）或者连字符（-）。|
|DataDisk.n.Description|String|否|数据盘描述，`n`的取值范围为\[1, 16\]。长度为 \[2, 256\] 个英文或中文字符，不能以 http:// 和 https:// 开头。|
|DataDisk.n.DeleteWithInstance|Boolean|否|表示数据盘是否随实例释放，`n`的取值范围为\[1, 16\]。取值范围：-   true（默认）：实例释放时，这块磁盘随实例一起释放。
-   false：实例释放时，这块磁盘保留不释放。

这个参数只对参数`DataDisk.n.Category`取值为`cloud`、`cloud_efficiency`或`cloud_ssd`的云盘，否则会报错。

|
|HpcClusterId|String|否|实例所属的集群ID。|
|PrivateIpAddress|String|否|实例私网IP地址。该IP地址必须为VSwitchId网段的子集网址。**说明：** 设置PrivateIpAddress时，Amount参数取值只能为1。

|
|InternetMaxBandwidthIn|Integer|否|公网入带宽最大值，单位为Mbit/s。取值范围：\[1, 200\] 默认值：200

|
|InternetMaxBandwidthOut|Integer|否|公网出带宽最大值，单位为Mbit/s。取值范围：\[0, 100\]默认值：0

|
|InstanceName|String|否|实例名称。长度为 \[2, 128\] 个英文或中文字符。必须以大小字母或中文开头，不能以 http:// 和 https:// 开头。可以包含数字、半角冒号（:）、下划线（\_）或者连字符（-）。默认值为实例的`InstanceId`。

**说明：** 创建多台实例时，您可以使用[`UniqueSuffix`](#UniqueSuffix)为这些实例设置不同的`InstanceName`。

|
|HostName|String|否|云服务器的主机名。-   点号（.）和短横线（-）不能作为首尾字符，更不能连续使用。
-   Windows 实例：字符长度为 \[2, 15\]，不支持点号（.），不能全是数字。允许大小写英文字母、数字和短横线（-）。
-   其他类型实例（Linux 等）：字符长度为 \[2, 64\]，支持多个点号（.），点之间为一段，每段允许大小写英文字母、数字和短横线（-）。

**说明：** 创建多台实例时，您可以使用[`UniqueSuffix`](#UniqueSuffix)为这些实例设置不同的`HostName`。

|
|UniqueSuffix|Boolean|否|是否为`HostName`和`InstanceName`添加有序后缀，有序后缀从001开始递增，最大不能超过999。例如：`LocalHost001`，`LocalHost002`和`MyInstance001`，`MyInstance002`。默认值：false

|
|Description|String|否|实例的描述。长度为 \[2, 256\] 个英文或中文字符，不能以 http:// 和 https:// 开头。|
|Password|String|否|实例的密码。长度为 8 至 30 个字符，必须同时包含大小写英文字母、数字和特殊符号。特殊符号可以是\(\)\` ~!@\#$%^&\*-+=|\{\}\[\]:;‘<\>,.?/。其中，Windows 实例不能以斜线号（/）为密码首字符。**说明：** 如果传入参数`Password`，建议您使用HTTPS协议调用API，避免密码泄露。

|
|PasswordInherit|Boolean|否|是否使用镜像预设的密码。使用该参数时，`Password`参数必须为空，同时您需要确保使用的镜像已经设置了密码。|
|Amount|String|否|指定创建ECS实例的数量。取值范围：\[1, 100\]默认值：1

|
|AutoReleaseTime|String|否|自动释放时间。按照[ISO8601](../intl.zh-CN/API 参考/附录/时间格式.md#)标准表示，并需要使用UTC时间，格式为yyyy-MM-ddTHH:mm:ssZ。-   如果秒不是00，则自动取为当前分钟开始时。
-   最短在当前时间之后半小时。
-   最久不能超过当前时间起三年。

|
|UserData|String|否|实例自定义数据。需要以Base64方式编码，原始数据最多为16 KB。|
|KeyPairName|String|否|密钥对名称。-   Windows实例：忽略该参数。默认为空。即使填写了该参数，仍旧只执行参数`Password`的内容。
-   Linux实例：如果指定该参数，默认禁用密码登录方式。

|
|DeploymentSetId|String|否|部署集ID。|
|RamRoleName|String|否|实例RAM角色名称。您可以使用 *RAM* API [ListRoles](../../../../../intl.zh-CN/API参考/API 参考（RAM）/角色管理接口/ListRoles.md#)查询实例RAM角色名称。参考相关API [CreateRole](../../../../../intl.zh-CN/API参考/API 参考（RAM）/角色管理接口/CreateRole.md#)和[ListRoles](../../../../../intl.zh-CN/API参考/API 参考（RAM）/角色管理接口/ListRoles.md#)。|
|SecurityEnhancementStrategy|String|否|是否开启安全加固。取值范围：-   Active：启用安全加固，只对系统镜像生效。
-   Deactive：不启用安全加固，对所有镜像类型生效。

|
|Tag.n.Key|String|否|实例、磁盘和主网卡的标签键。n 的取值范围：\[1, 20\]。一旦传入该值，则不允许为空字符串。最多支持 64 个字符，不能以 aliyun、acs:、http:// 或者 https:// 开头。|
|Tag.n.Value|String|否|实例、磁盘和主网卡的标签值。n的取值范围：\[1, 20\]。一旦传入该值，可以为空字符串。最多支持 128 个字符，不能以 aliyun、acs:、http:// 或者 https:// 开头。|
|SpotStrategy|String|否|后付费实例的抢占策略。当参数`InstanceChargeType`取值为`PostPaid`时生效。取值范围：-   NoSpot（默认）：正常按量付费实例。
-   SpotWithPriceLimit：设置上限价格的抢占式实例。
-   SpotAsPriceGo：系统自动出价，跟随当前市场实际价格。

|
|SpotPriceLimit|Float|否|设置实例的每小时最高价格。支持最大3位小数，参数`SpotStrategy`取值为`SpotWithPriceLimit`时生效。|
|DryRun|Boolean|否|是否只预检此次请求。-   true（默认）：发送检查请求，不会创建实例。检查项包括是否填写了必需参数、请求格式、业务限制和ECS库存。如果检查不通过，则返回对应错误。如果检查通过，则返回错误码`DryRunOperation`。
-   false：发送正常请求，通过检查后直接创建实例。

**说明：** `DryRun=true`时，Amount参数只能设置为1。

|
|ClientToken|String|否| 用于保证请求的幂等性。由客户端生成该参数值，要保证在不同请求间唯一。只支持ASCII字符，且不能超过64个字符。更多详情，请参阅[如何保证幂等性](intl.zh-CN/API 参考/附录/如何保证幂等性.md#)。

 |

## 返回参数 {#ResponseParameter .section}

|名称|类型|描述|
|:-|:-|:-|
|InstanceIdSets|[InstanceIdSet](#InstanceIdSet)|实例ID列表。|

**数据类型InstanceIdSet**

|名称|类型|描述|
|:-|:-|:-|
|InstanceId|String|全局唯一的实例ID，是访问实例的唯一标识。|

## 示例 { .section}

**请求示例**

```
https://ecs.aliyuncs.com/?Action=RunInstances
&RegionId=cn-hangzhou
&InstanceType=ecs.cm4.6xlarge
&SecurityGroupId=sg-securitygroupid
&Amount=3
&<公共请求参数>
```

**返回示例**

**XML格式**

```
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

**JSON格式**

```
{
    "InstanceIdSets": {
        "InstanceIdSet": [
            "i-instanceid1",
            "i-instanceid2",
            "i-instanceid3"
        ]
    },
    "RequestId": "04F0F334-1335-436C-A1D7-6C044FE73368"
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问 [API 错误中心](https://error-center.alibabacloud.com/status/product/Ecs)。

|错误代码|错误信息|HTTP状态码|说明|
|:---|:---|:------|:-|
|Account.Arrearage|Your account has an outstanding payment.|400|您的账号已经欠费。|
|EncryptedOption.Conflict|Encryption value of disk and snapshot conflict.|400|磁盘的加密属性和快照的加密属性不一致。|
|DryRunOperation|Request validation has been passed with DryRun flag set.|400|此次DryRun预检请求合格。|
|IncorrectVSwitchStatus|The current status of virtual switch does not support this operation.|400|指定的虚拟交换机状态不正确。|
|InstanceDiskCategoryLimitExceed|The specified DataDisk.n.Size beyond the permitted range, or the capacity of snapshot exceeds the size limit of the specified disk category.|400|指定的磁盘大小超过了该类型磁盘上限。|
|InstanceDiskNumber.LimitExceed|The total number of specified disk in an instance exceeds.|400|镜像中包含的数据盘和数据盘参数合并后，数据盘的总数超出限制。|
|InvalidAutoRenewPeriod.ValueNotSupported|The specified autoRenewPeriod is not valid.|400|指定的`AutoRenewPeriod`不合法。|
|InvalidDataDiskSize.ValueNotSupported|The specified DataDisk.n.Size beyond the permitted range, or the capacity of snapshot exceeds the size limit of the specified disk category.|400|指定的`DataDisk.n.Size`不合法或者超出范围。|
|InvalidDescription.Malformed|The specified parameter Description is not valid.|400|指定的资源描述格式错误。|
|InvalidDiskCategory.ValueNotSupported|The specified parameter DiskCategory is not valid.|400|指定的磁盘种类不合法。|
|InvalidDiskDescription.Malformed|The specified parameter SystemDisk.DiskDescription or DataDisk.n.Description is not valid.|400|指定的参数`SystemDisk.DiskDescription`或参数`DataDisk.n.Description`不合法。|
|InvalidDiskName.Malformed|The specified parameter SystemDisk.DiskName or DataDisk.n.DiskName is not valid.|400|指定的参数`SystemDisk.DiskName`或`DataDisk.n.DiskName`不合法。|
|InvalidHostName.Malformed|The specified parameter HostName is not valid.|400|指定的`HostName`格式错误。|
|InvalidInstanceName.Malformed|The specified parameter InstanceName is not valid.|400|指定的`InstanceName`格式不合法。|
|InvalidInstanceType.ValueNotSupported|The specified InstanceType beyond the permitted range.|400|指定的`InstanceType`不合法或者超出可选范围。|
|InvalidInstanceType.ValueUnauthorized|The specified InstanceType is not authorized.|400|指定的`InstanceType`未授权使用。|
|InvalidInternetChargeType.ValueNotSupported|The specified InternetChargeType is not valid.|400|指定的`InternetChargeType`不存在。|
|InvalidIoOptimizedValue.ValueNotSupported|IoOptimized value not supported.|400|指定的`IoOptimized`参数不支持。|
|InvalidNetworkType.Mismatch|Specified parameter InternetMaxBandwidthIn or InternetMaxBandwidthOut conflict with instance network type.|400|指定的`InternetMaxBandwidthIn`或`InternetMaxBandwidthOut`与实例网络类型不符合。|
|InvalidNetworkType.Mismatch|Specified parameter InternetChargeType conflict with instance network type.|400|指定的`InternetChargeType`与实例网络类型不符合。|
|InvalidParameter|The specified parameter InternetMaxBandwidthOut is not valid.|400|指定的`InternetMaxBandwidthOut`取值为数字且不能超过100。|
|InvalidParameter|The specified instance bandwidth is not valid.|400|指定的带宽值不合法。|
|InvalidParameter|The specified parameter Amount is not valid.|400|指定的`Amount`取值不能超过100。|
|InvalidParameter.Bandwidth|The specified parameter Bandwidth is not valid.|400|指定的带宽值不合法。|
|InvalidParameter.Conflict|The specified image does not support the specified instance type.|400|指定的实例规格不允许使用指定的镜像。|
|InvalidParameter.Encrypted.KmsNotEnabled|The encrypted disk need enable KMS.|400|您还未开通KMS服务。|
|InvalidParameter.EncryptedIllegal|The value of parameter Encrypted is illegal.|400|指定的`DataDisk.n.Encrypted`不合法。|
|InvalidParameter.EncryptedNotSupported|Encrypted disk is not support in this region.|400|指定的地域不支持磁盘加密。|
|InvalidParameter.EncryptedNotSupported|Corresponding data disk category does not support encryption.|400|指定的磁盘类型不支持加密。|
|InvalidParameter.Mismatch|Specified security group and virtual switch are not in the same VPC.|400|指定安全组与虚拟交换机不属于同一个VPC。|
|InvalidParameter.Mismatch|Specified virtual switch is not in the specified zone.|400|指定的虚拟交换机不在指定的可用区。|
|InvalidPassword.Malformed|The specified parameter Password is not valid.|400|指定的`Password`格式错误。|
|InvalidPasswordParam.Mismatch|The input password should be null when passwdInherit is true.|400|指定了`PasswordInherit`后，您不能指定`Password`参数。|
|InvalidSnapshotId.BasedSnapshotTooOld|The specified snapshot is created before 2013-07-15.|400|不能使用早于2013年7月15日（含）创建的快照。|
|InvalidSpotAliUid|The specified UID is not authorized to use SPOT instance.|400|您的账号暂不能使用抢占式实例资源。|
|InvalidSpotAuthorized|The specified Spot param is unauthorized.|400|您的账号暂未授权使用抢占式实例资源。|
|InvalidSpotPrepaid|The specified Spot type is not support PrePay Instance.|400|抢占式实例不支持预付费计费方式。|
|InvalidSpotPriceLimit|The specified SpotPriceLimitis not valid.|400|指定的`SpotPriceLimit`不合法。|
|InvalidSpotPriceLimit.LowerThanPublicPrice|The specified parameter spotPriceLimit can’t be lower than current public price.|400|指定的`SpotPriceLimit`不能低于我们设定的最低市场价格。|
|InvalidSpotStrategy|The specified SpotStrategy is not valid.|400|指定的`SpotStrategy`不合法。|
|InvalidSystemDiskCategory.ValueNotSupported|The specified parameter SystemDisk.Category is not valid.|400|指定的`SystemDisk.Category`不合法。|
|InvalidUserData.NotSupported|The specified parameter UserData only support the vpc and IoOptimized Instance.|400|实力自定义数据`UserData`只能使用在VPC类型和I/O优化实例上。|
|InvalidUserData.SizeExceeded|The specified parameter UserData exceeds the size.|400|指定的`UserData`在Base64编码前不能超过64KB。|
|InvalidHpcClusterId.NotFound|The specified HpcClusterId is not found.|400|指定的`HpcClusterId`不存在。|
|InvalidHpcClusterId.Creating|The specified HpcClusterId is creating.|400|指定的`HpcClusterId`正在创建中。|
|InvalidHpcClusterId.Unnecessary|The specified HpcClusterId is unnecessary.|400|只有部分实例规格`InstanceType`支持指定集群 ID。|
|InvalidVSwitchId.Necessary|The HpcClusterId is necessary.|400|该实例规格`InstanceType`需要指定集群ID，您需要传入`HpcClusterId`。|
|MissingParameter|The input parameter VSwitchId that is mandatory for processing this request is not supplied.|400|您必须为VPC类型实例指定 `VSwitchId`。|
|QuotaExceed.AfterpayInstance|The maximum number of Pay-As-You-Go instances is exceeded.|400|您能创建的按量付费实例数达到上限。更多详情，请参阅[使用限制](../intl.zh-CN/用户指南/使用限制.md#)。|
|QuotaExceeded|Living instances quota exceeded in this VPC.|400|指定的VPC中实例数量已超限。|
|ResourceNotAvailable|Resource you requested is not available in this region or zone.|400|指定的地域或者可用区该资源不可用。|
|CategoryNotSupported|The specified zone does not offer the specified disk category.|403|指定的可用区暂无指定的磁盘种类。|
|DeleteWithInstance.Conflict|The specified disk is not a portable disk and cannot be set to DeleteWithInstance attribute.|403|指定的磁盘类型不支持设置`DeleteWithInstance`属性。|
|DependencyViolation.WindowsInstance|The instance creating is window, cannot use ssh key pair to login.|403|Windows实例不能使用SSH密钥对。|
|Forbidden|User not authorized to operate on the specified resource.|403|您暂时没有权限。|
|ImageNotSubscribed|The specified image has not be subscribed.|403|指定的镜像来自镜像市场，您没有订阅镜像市场的镜像。|
|ImageNotSupportInstanceType|The specified image don’t support the InstanceType instance.|403|指定镜像不能运行在指定规格的实例上。|
|ImageRemovedInMarket|The specified market image is not available, or the specified custom image includes product code because it is based on an image subscribed from marketplace, and that image in marketplace including exact the same product code has been removed.|403|镜像市场的镜像已下架，或者自定义镜像中包含的`product-code`对应的镜像市场镜像已经下架。|
|InstanceDiskCategoryLimitExceed|The total size of specified disk category in an instance exceeds.|403|指定的磁盘种类超过了单实例的最大容量。|
|InstanceDiskNumLimitExceed|The number of specified disk in an instance exceeds.|403|指定实例已经达到可挂载磁盘的最大值。|
|InvalidDiskCategory.Mismatch|The specified disk categories combination is not supported.|403|指定的磁盘类型组合不支持。|
|InvalidDiskCategory.NotSupported|The specified disk category is not support the specified instance type.|403|指定的磁盘类型不支持该实例类型。|
|InvalidDiskSize.TooSmall|Specified disk size is less than the size of snapshot.|403|指定的磁盘小于指定快照大小。|
|InvalidInstanceType.ZoneNotSupported|The specified zone does not support this InstanceType.|403|指定的可用区不支持该实例规格。|
|InvalidNetworkType.MismatchRamRole|Ram role cannot be attached to instances of Classic network type.|403|实例RAM角色不能用于经典网络类型实例。|
|InvalidPayMethod|The specified billing method is not valid.|403|指定的计费方式不存在。|
|InvalidResourceType.NotSupported|This resource type is not supported; please try other resource types.|403|创建实例的配置暂无可用区支持，请选择其他配置创建。|
|InnerServiceFailed|The request processing has failed due to some inner service error.|403|服务器内部错误。|
|InvalidSnapshotId.NotDataDiskSnapshot|The specified snapshot is system disk snapshot.|403|系统盘快照不能创建数据盘。|
|InvalidSnapshotId.NotReady|The specified snapshot has not completed yet.|403|指定的快照正在创建中，请稍后再试。|
|InvalidSystemDiskCategory.ValueUnauthorized|The disk category is not authorized.|403|您暂时无法使用指定的磁盘类型。|
|InvalidUser.PassRoleForbidden|The RAM user does not have the privilege to pass a role.|403|您使用的RAM用户账号暂不具有`PassRole`的权限，请联系主账号拥有者[授权](../intl.zh-CN/快速入门/为 RAM 用户授权.md#)PassRole权限。|
|InvalidUserData.Forbidden|User not authorized to input the parameter UserData, please apply for permission UserData.|403|您暂时无法设置实例自定义数据。|
|InvalidVSwitchId.NotFound|The VSwitchId provided does not exist in our records.|403|指定的`VSwitchId`不存在。|
|IoOptimized.NotSupported|The specified image is not support IoOptimized Instance.|403|指定的镜像不支持I/O优化实例。|
|IoOptimized.NotSupported|Vpc is not support IoOptimized instance.|403|VPC不支持I/O优化实例。|
|OperationDenied|The specified snapshot is not allowed to create disk.|403|特定磁盘的快照不能创建磁盘或者快照不能创建磁盘。|
|OperationDenied|The creation of Instance to the specified Zone is not allowed.|403|您无法在该可用区创建实例。或者指定的可用区和地域不匹配。|
|OperationDenied|The specified Image is disabled or is deleted.|403|指定的镜像不存在。|
|OperationDenied|Sales of this resource are temporarily suspended in the specified region; please try again later.|403|指定的地域暂时停售按量付费实例。|
|OperationDenied|The capacity of snapshot exceeds the size limit of the specified disk category or the specified category is not authorized.|403|指定的`DataDisk.n.Size`不合法或者超出范围。或者您暂时无法使用指定的磁盘类型。|
|OperationDenied|The type of the disk does not support the operation.|403|指定磁盘类型不支持该操作。|
|OperationDenied.NoStock|Sales of this resource are temporarily suspended in the specified region; please try again later.|403|指定的可用区内实例规格库存不足，请尝试其它实例规格或者可用区。|
|QuotaExceed.BuyImage|The specified image is from the image market, You have not bought it or your quota has been exceeded.|403|您没有订阅指定的镜像。或者您的镜像额度超过限制，更多详情，请参阅[使用限制](../intl.zh-CN/用户指南/使用限制.md#)。|
|QuotaExceed.PortableCloudDisk|The quota of portable cloud disk exceeds.|403|可挂载的云磁盘数量不能超过16块。|
|RegionUnauthorized|There is no authority to create instance in the specified region.|403|您暂时无法使用指定地域中的资源。|
|SecurityGroupInstanceLimitExceed|The maximum number of instances in a security group is exceeded.|403|一个安全组最多能管理1000台实例。|
|Zone.NotOnSale|The specified zone is not available for purchase.|403|指定的可用区暂时无法创建实例，请更换其他可用区/地域。或者您创建的是VPC类型实例，指定的虚拟交换机有可用区限制。|
|Zone.NotOpen|The specified zone is not granted to you to buy resources yet.|403|指定的可用区暂时无法创建实例。|
|ZoneId.NotFound|The specified zone does not exists.|403|指定的可用区不存在。|
|DependencyViolation.IoOptimized|The specified InstanceType must be IoOptimized instance.|404|指定的实例规格必须是I/O优化实例。|
|HOSTNAME\_ILLEGAL|hostname is not valid.|404|指定的`HostName`参数不合法。|
|InvalidDataDiskSnapshotId.NotFound|The specified parameter DataDisk.n.SnapshotId is not valid.|404|指定的`DataDisk.n.SnapshotId`不存在。|
|InvalidImageId.NotFound|The specified ImageId does not exist.|404|指定的镜像不存在。|
|InvalidInstanceChargeType.NotFound|The InstanceChargeType does not exist in our records.|404|指定的`InstanceChargeType`不存在。|
|InvalidKeyPairName.NotFound|The specified KeyPairName does not exist in our records.|404|指定的`KeyPairName`不存在。|
|InvalidLaunchTemplate.NotFound|The specified LaunchTemplateId “\{0\}” LaunchTemplateName “\{1\}” is not found.|404|指定的`LaunchTemplateId`或`LaunchTemplateName`不存在。|
|InvalidLaunchTemplateVersion.NotFound|The specified LaunchTemplateId “\{0\}” Version “\{1\}” is not found.|404|指定的`LaunchTemplateVersion`不存在。|
|InvalidRamRole.NotFound|The specified RamRoleName does not exist.|404|指定的`RamRoleName`不存在。|
|InvalidRegionId.NotFound|The specified RegionId does not exist.|404|指定的地域不存在。|
|InvalidSecurityGroupId|The specified SecurityGroupId is invalid or does not exist.|404|指定的`SecurityGroupId`不合法或不存在。或者您无法使用指定的安全组。|
|InvalidSystemDiskSize|The specified parameter SystemDisk.Size is invalid.|404|指定的`SystemDisk.Size`不合法。|
|InvalidSystemDiskSize.LessThanImageSize|The specified parameter SystemDisk.Size is less than the image size.|404|指定的`SystemDisk.Size`不能小于镜像文件大小。|
|InvalidSystemDiskSize.LessThanMinSize|The specified parameter SystemDisk.Size is less than the min size.|404|指定的`SystemDisk.Size`不能小于20 GiB。|
|InvalidSystemDiskSize.MoreThanMaxSize|The specified parameter SystemDisk.Size is more than the max size.|404|指定的`SystemDisk.Size`不能超过500 GiB。|
|InvalidVSwitchId.NotFound|Specified virtual switch does not exist.|404|指定的虚拟交换机不存在。|
|InvalidZoneId.NotFound|The specified ZoneId does not exist.|404|指定的可用区不存在。|
|IoOptimized.NotSupported|The specified InstanceType is not support IoOptimized instance.|404|指定的实例类型不支持I/O优化实例。|
|OperationDenied|Another Instance is being created.|404|正在创建另外的实例，请稍后再试。|
|PaymentMethodNotFound|No billing method has been registered on the account.|404|您的账号还未设置付费方式。|
|InternalError|The request processing has failed due to some unknown error,exception or failure.|500|内部错误，请稍后再试。|

