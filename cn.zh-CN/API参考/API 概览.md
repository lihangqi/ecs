# API 概览 {#AvailableActions .reference}

本文汇总了云服务器ECS所有可调用API，具体接口信息请参见相关文档。

更多API资源，请访问[API Explorer](https://api.aliyun.com/)。

## 实例相关接口 {#section_vvj_q2h_vdb .section}

|接口|描述|
|:-|:-|
|[RunInstances](cn.zh-CN/API参考/实例/RunInstances.md#)|创建一台或者多台预付费（包年包月）、按量付费或者抢占式实例。|
|[CreateInstance](cn.zh-CN/API参考/实例/CreateInstance.md#)|创建一台预付费（包年包月）、按量付费或者抢占式实例。|
|[StartInstance](cn.zh-CN/API参考/实例/StartInstance.md#)|启动一台指定的实例。|
|[StopInstance](cn.zh-CN/API参考/实例/StopInstance.md#)|停止运行一台指定的实例。|
|[RebootInstance](cn.zh-CN/API参考/实例/RebootInstance.md#)|重启指定的实例。|
|[DeleteInstance](cn.zh-CN/API参考/实例/DeleteInstance.md#)|根据传入的实例名称释放您的实例资源。|
|[AttachInstanceRamRole](cn.zh-CN/API参考/实例/AttachInstanceRamRole.md#)|为您的实例授予实例RAM角色。|
|[DetachInstanceRamRole](cn.zh-CN/API参考/实例/DetachInstanceRamRole.md#)|收回实例的实例RAM角色。|
|[DescribeInstanceStatus](cn.zh-CN/API参考/实例/DescribeInstanceStatus.md#)|批量获取当前用户所有实例的状态信息。|
|[DescribeInstances](cn.zh-CN/API参考/实例/DescribeInstances.md#)|查询所有实例的详细信息。|
|[DescribeInstanceVncUrl](cn.zh-CN/API参考/实例/DescribeInstanceVncUrl.md#)|查询实例的Web管理终端地址。|
|[DescribeUserdata](cn.zh-CN/API参考/实例/DescribeUserData.md#)|查询您的实例的自定义数据。|
|[DescribeInstanceAutoRenewAttribute](cn.zh-CN/API参考/实例/DescribeInstanceAutoRenewAttribute.md#)|查询实例自动续费状态。|
|[DescribeInstanceRamRole](cn.zh-CN/API参考/实例/DescribeInstanceRamRole.md#)|查询一台或者多台实例上的已赋予的实例RAM角色的信息。|
|[DescribeSpotPriceHistory](cn.zh-CN/API参考/实例/DescribeSpotPriceHistory.md#)|查询抢占式实例历史价格。最多能查询30天内的历史价格记录。|
|[DescribeInstanceTypeFamilies](cn.zh-CN/API参考/实例/DescribeInstanceTypeFamilies.md#)|查询云服务器ECS提供的实例规格族资源。|
|[DescribeInstanceTypes](cn.zh-CN/API参考/实例/DescribeInstanceTypes.md#)|查询云服务器ECS提供的实例规格资源。|
|[ModifyInstanceVpcAttribute](cn.zh-CN/API参考/实例/ModifyInstanceVpcAttribute.md#)|修改实例的VPC属性。|
|[ModifyInstanceAttribute](cn.zh-CN/API参考/实例/ModifyInstanceAttribute.md#)|修改实例密码、实例名称和安全组等属性信息。|
|[ModifyInstanceVncPasswd](cn.zh-CN/API参考/实例/ModifyInstanceVncPasswd.md#)|修改实例的Web管理终端密码。|
|[ModifyInstanceAutoReleaseTime](cn.zh-CN/API参考/实例/ModifyInstanceAutoReleaseTime.md#)|为实例设定自动释放时间。|
|[ModifyInstanceAutoRenewAttribute](cn.zh-CN/API参考/实例/ModifyInstanceAutoRenewAttribute.md#)|设置实例的自动续费状态。|
|[ModifyInstanceChargeType](cn.zh-CN/API参考/实例/ModifyInstanceChargeType.md#)|修改实例付费类型，支持按量付费实例换成预付费实例。|
|[ModifyInstanceSpec](cn.zh-CN/API参考/实例/ModifyInstanceSpec.md#)|调整按量付费实例的实例规格和公网带宽大小。|
|[ModifyPrepayInstanceSpec](cn.zh-CN/API参考/实例/ModifyPrepayInstanceSpec.md#)|升级或者降低预付费实例规格。|
|[RenewInstance](cn.zh-CN/API参考/实例/RenewInstance.md#)|为预付费（包年包月）实例续费。|

## 启动模板相关接口 {#section_fsy_hzw_d2b .section}

|接口|描述|
|:-|:-|
|[CreateLaunchTemplate](cn.zh-CN/API参考/启动模板/CreateLaunchTemplate.md#)|创建一个实例启动模板，简称模板。实例启动模板能免除您每次创建实例时都需要填入大量配置参数。|
|[CreateLaunchTemplateVersion](cn.zh-CN/API参考/启动模板/CreateLaunchTemplateVersion.md#)|根据指定的实例启动模板创建一个版本。|
|[DeleteLaunchTemplate](cn.zh-CN/API参考/启动模板/DeleteLaunchTemplate.md#)|删除一个实例启动模板。|
|[DeleteLaunchTemplateVersion](cn.zh-CN/API参考/启动模板/DeleteLaunchTemplateVersion.md#)|删除指定实例启动模板的一个版本。不支持删除默认版本，您需要通过[DeleteLaunchTemplate](cn.zh-CN/API参考/启动模板/DeleteLaunchTemplate.md#)删除整个实例启动模板才能删除默认版本。|
|[DescribeLaunchTemplates](cn.zh-CN/API参考/启动模板/DescribeLaunchTemplates.md#)|查询可用的实例启动模板。|
|[DescribeLaunchTemplateVersions](cn.zh-CN/API参考/启动模板/DescribeLaunchTemplateVersions.md#)|查询实例启动模板版本。|
|[ModifyLaunchTemplateDefaultVersion](cn.zh-CN/API参考/启动模板/ModifyLaunchTemplateDefaultVersion.md#)|切换启动模板的某个版本为该模板的默认版本。如果您在创建实例（[RunInstances](cn.zh-CN/API参考/实例/RunInstances.md#)）时不指定模板版本号，会采用默认版本。|

## 磁盘相关接口 {#section_t3s_t2h_vdb .section}

|接口|描述|
|:-|:-|
|[CreateDisk](cn.zh-CN/API参考/磁盘/CreateDisk.md#)|创建可卸载云盘的数据盘。|
|[DeleteDisk](cn.zh-CN/API参考/磁盘/DeleteDisk.md#)|释放一块云盘。|
|[DescribeDisks](cn.zh-CN/API参考/磁盘/DescribeDisks.md#)|查询您已经创建的磁盘。|
|[AttachDisk](cn.zh-CN/API参考/磁盘/AttachDisk.md#)|为实例挂载数据盘。|
|[DetachDisk](cn.zh-CN/API参考/磁盘/DetachDisk.md#)|将一块云盘从一台实例上卸载。|
|[ModifyDiskChargeType](cn.zh-CN/API参考/磁盘/ModifyDiskChargeType.md#)|修改一台实例上挂载的一块或最多16块磁盘的计费方式。|
|[ModifyDiskAttribute](cn.zh-CN/API参考/磁盘/ModifyDiskAttribute.md#)|修改您的磁盘的属性或者明细。|
|[ReplaceSystemDisk](cn.zh-CN/API参考/磁盘/ReplaceSystemDisk.md#)|更换实例的系统盘或者操作系统。|
|[ReInitDisk](cn.zh-CN/API参考/磁盘/ReInitDisk.md#)|初始化云盘到创建时的初始状态。|
|[ResetDisk](cn.zh-CN/API参考/磁盘/ResetDisk.md#)|使用磁盘的历史快照回滚至某一阶段的磁盘状态。|
|[ResizeDisk](cn.zh-CN/API参考/磁盘/ResizeDisk.md#)|扩容一块磁盘。|

## 镜像相关接口 {#section_image_t2h_vdb .section}

|接口|描述|
|:-|:-|
|[CreateImage](cn.zh-CN/API参考/镜像/CreateImage.md#)|创建一份自定义镜像。|
|[ImportImage](cn.zh-CN/API参考/镜像/ImportImage.md#)|导入您已有的镜像文件到云服务器ECS环境中，并作为自定义镜像出现在相应地域中。|
|[ExportImage](cn.zh-CN/API参考/镜像/ExportImage.md#)|导出自定义镜像到与该自定义镜像同一地域的对象存储OSS bucket里。|
|[CopyImage](cn.zh-CN/API参考/镜像/CopyImage.md#)|将一个地域下的自定义镜像复制到其他地域。|
|[CancelCopyImage](cn.zh-CN/API参考/镜像/CancelCopyImage.md#)|取消正在进行中的复制镜像（`CopyImage`）任务。|
|[DescribeImages](cn.zh-CN/API参考/镜像/DescribeImages.md#)|查询您可以使用的镜像资源。|
|[DeleteImage](cn.zh-CN/API参考/镜像/DeleteImage.md#)|删除一份自定义镜像。|
|[DescribeImageSharePermission](cn.zh-CN/API参考/镜像/DescribeImageSharePermission.md#)|查询一份自定义镜像已经共享的所有用户。|
|[ModifyImageAttribute](cn.zh-CN/API参考/镜像/ModifyImageAttribute.md#)|修改自定义镜像的名称和描述。|
|[ModifyImageSharePermission](cn.zh-CN/API参考/镜像/ModifyImageSharePermission.md#)|管理镜像共享权限。|
|[DescribeImageSupportInstanceTypes](cn.zh-CN/API参考/镜像/DescribeImageSupportInstanceTypes.md#)|查询指定镜像支持的实例规格。|

## 快照相关接口 {#section_snapshot_t2h_vdb .section}

|接口|描述|
|:-|:-|
|[CreateSnapshot](cn.zh-CN/API参考/快照/CreateSnapshot.md#)|为指定的磁盘创建快照。|
|[CreateAutoSnapshotPolicy](cn.zh-CN/API参考/快照/CreateAutoSnapshotPolicy.md#)|创建一条自动快照策略。|
|[ApplyAutoSnapshotPolicy](cn.zh-CN/API参考/快照/ApplyAutoSnapshotPolicy.md#)|为一块或者多块磁盘应用自动快照策略。|
|[DeleteSnapshot](cn.zh-CN/API参考/快照/DeleteSnapshot.md#)|删除指定的快照。|
|[CancelAutoSnapshotPolicy](cn.zh-CN/API参考/快照/CancelAutoSnapshotPolicy.md#)|取消一块或者多块磁盘的自动快照策略。|
|[DeleteAutoSnapshotPolicy](cn.zh-CN/API参考/快照/DeleteAutoSnapshotPolicy.md#)|删除一条自动快照策略。|
|[DescribeAutoSnapshotPolicyEx](cn.zh-CN/API参考/快照/DescribeAutoSnapshotPolicyEX.md#)|查询您已创建的自动快照策略。|
|[DescribeSnapshots](cn.zh-CN/API参考/快照/DescribeSnapshots.md#)|查询某台实例磁盘设备所有的快照列表。|
|[DescribeSnapshotLinks](cn.zh-CN/API参考/快照/DescribeSnapshotLinks.md#)|查询磁盘快照链。|
|[ModifyAutoSnapshotPolicyEx](cn.zh-CN/API参考/快照/ModifyAutoSnapshotPolicyEx.md#)|修改一条自动快照策略。|
|[DescribeSnapshotsUsage](cn.zh-CN/API参考/快照/DescribeSnapshotsUsage.md#)|查询您在一个地域下的快照数量以及快照容量。|
|[DescribeSnapshotPackage](cn.zh-CN/API参考/快照/DescribeSnapshotPackage.md#)|查询您在一个阿里云地域下已经购买了用于可以抵扣快照存储容量的对象存储OSS（存储包）。|

## 安全组相关接口 {#section_securitygroup_t2h_vdb .section}

|接口|描述|
|:-|:-|
|[CreateSecurityGroup](cn.zh-CN/API参考/安全组/CreateSecurityGroup.md#)|新建一个安全组。|
|[AuthorizeSecurityGroup](cn.zh-CN/API参考/安全组/AuthorizeSecurityGroup.md#)|增加一条安全组入方向规则。|
|[AuthorizeSecurityGroupEgress](cn.zh-CN/API参考/安全组/AuthorizeSecurityGroupEgress.md#)|增加一条安全组出方向规则。|
|[RevokeSecurityGroup](cn.zh-CN/API参考/安全组/RevokeSecurityGroup.md#)|删除一条安全组入方向规则。|
|[RevokeSecurityGroupEgress](cn.zh-CN/API参考/安全组/RevokeSecurityGroupEgress.md#)|删除一条安全组出方向规则。|
|[JoinSecurityGroup](cn.zh-CN/API参考/安全组/JoinSecurityGroup.md#)|将一台实例加入到指定的安全组。|
|[LeaveSecurityGroup](cn.zh-CN/API参考/安全组/LeaveSecurityGroup.md#)|将一台实例移出指定的安全组。|
|[DeleteSecurityGroup](cn.zh-CN/API参考/安全组/DeleteSecurityGroup.md#)|删除一个安全组。|
|[DescribeSecurityGroupAttribute](cn.zh-CN/API参考/安全组/DescribeSecurityGroupAttribute.md#)|查询安全组详情。|
|[DescribeSecurityGroups](cn.zh-CN/API参考/安全组/DescribeSecurityGroups.md#)|查询您创建的安全组的基本信息，例如安全组ID和安全组描述等。|
|[DescribeSecurityGroupReferences](cn.zh-CN/API参考/安全组/DescribeSecurityGroupReferences.md#)|查询一个安全组和其他哪些安全组有安全组级别的授权行为。|
|[ModifySecurityGroupAttribute](cn.zh-CN/API参考/安全组/ModifySecurityGroupAttribute.md#)|修改指定安全组的属性，包括修改安全组名称和描述。|
|[ModifySecurityGroupPolicy](cn.zh-CN/API参考/安全组/ModifySecurityGroupPolicy.md#)|修改安全组内网连通策略。|
|[ModifySecurityGroupRule](cn.zh-CN/API参考/安全组/ModifySecurityGroupRule.md#)|修改一条安全组入方向规则的描述信息。|

## 部署集相关接口 {#DeploymentSet .section}

|接口|描述|
|:-|:-|
|[CreateDeploymentSet](cn.zh-CN/API参考/部署集/CreateDeploymentSet.md#)|在指定的地域内创建一个部署集。|
|[ModifyInstanceDeployment](cn.zh-CN/API参考/部署集/ModifyInstanceDeployment.md#)|在同一地域下，修改一台ECS实例的宿主机。|
|[ModifyDeploymentSetAttributes](cn.zh-CN/API参考/部署集/ModifyDeploymentSetAttributes.md#)|将一台实例加入一个部署集，或者将实例从一个部署集调整到另外一个部署集。|
|[DescribeDeploymentSets](cn.zh-CN/API参考/部署集/DescribeDeploymentSets.md#)|查询一个或多个部署集的属性列表。|
|[DeleteDeploymentSet](cn.zh-CN/API参考/部署集/DeleteDeploymentSet.md#)|删除一个部署集。|

## SSH 密钥对相关接口 {#section_keypair_t2h_vdb .section}

|接口|描述|
|:-|:-|
|[CreateKeyPair](cn.zh-CN/API参考/SSH 密钥对/CreateKeyPair.md#)|创建一对SSH密钥对。|
|[ImportKeyPair](cn.zh-CN/API参考/SSH 密钥对/ImportKeyPair.md#)|导入由其他工具产生的SSH密钥对的公钥部分。|
|[AttachKeyPair](cn.zh-CN/API参考/SSH 密钥对/AttachKeyPair.md#)|绑定SSH密钥对到一台或者多台Linux实例。|
|[DetachKeyPair](cn.zh-CN/API参考/SSH 密钥对/DetachKeyPair.md#)|为一台或者多台Linux实例解绑SSH密钥对。|
|[DeleteKeyPairs](cn.zh-CN/API参考/SSH 密钥对/DeleteKeyPairs.md#)|删除一对或多对SSH密钥对。|
|[DescribeKeyPairs](cn.zh-CN/API参考/SSH 密钥对/DescribeKeyPairs.md#)|查询一对或者多对SSH密钥对。|

## 网络相关接口 {#section_network_t2h_vdb .section}

|接口|描述|
|:-|:-|
|[AllocatePublicIpAddress](cn.zh-CN/API参考/网络/AllocatePublicIpAddress.md#)|为一台实例分配一个公网IP地址。|
|[ConvertNatPublicIpToEip](cn.zh-CN/API参考/网络/ConvertNatPublicIpToEip.md#)|将一台网络类型为VPC类型的实例的公网IP（NatPublicIp）转化为弹性公网 IP（EIP）。|
|[AttachClassicLinkVpc](cn.zh-CN/API参考/网络/AttachClassicLinkVpc.md#)|将一台经典网络类型实例连接到VPC中，使经典网络类型实例可以和VPC中的云资源私网互通。|
|[DetachClassicLinkVpc](cn.zh-CN/API参考/网络/DetachClassicLinkVpc.md#)|取消经典网络类型实例与VPC的连接（ClassicLink）。|
|[DescribeBandwidthLimitation](cn.zh-CN/API参考/网络/DescribeBandwidthLimitation.md#)|查询带宽资源列表。|
|[DescribeClassicLinkInstances](cn.zh-CN/API参考/网络/DescribeClassicLinkInstances.md#)|查询一台或者多台与VPC建立了连接的经典网络类型实例。|
|[ModifyInstanceNetworkSpec](cn.zh-CN/API参考/网络/ModifyInstanceNetworkSpec.md#)|修改实例的带宽配置。|

## 弹性网卡相关接口 {#section_networkinterface_t2h_vdb .section}

|接口|描述|
|:-|:-|
|[CreateNetworkInterface](cn.zh-CN/API参考/弹性网卡/CreateNetworkInterface.md#)|创建一张弹性网卡（ENI）。|
|[AttachNetworkInterface](cn.zh-CN/API参考/弹性网卡/AttachNetworkInterface.md#)|附加弹性网卡（ENI）到VPC类型实例上。|
|[DetachNetworkInterface](cn.zh-CN/API参考/弹性网卡/DetachNetworkInterface.md#)|从实例上分离弹性网卡（ENI）。|
|[DeleteNetworkInterface](cn.zh-CN/API参考/弹性网卡/DeleteNetworkInterface.md#)|删除一张弹性网卡（ENI）。|
|[DescribeNetworkInterfaces](cn.zh-CN/API参考/弹性网卡/DescribeNetworkInterfaces.md#)|查看弹性网卡（ENI）列表。|
|[ModifyNetworkInterfaceAttribute](cn.zh-CN/API参考/弹性网卡/ModifyNetworkInterfaceAttribute.md#)|修改一张弹性网卡（ENI）的属性。|
|[AssignIpv6Addresses](cn.zh-CN/API参考/弹性网卡/AssignIpv6Addresses.md#)|为弹性网卡分配一个或多个IPv6地址。|
|[UnassignIpv6Addresses](cn.zh-CN/API参考/弹性网卡/UnassignIpv6Addresses.md#)|若弹性网卡已被分配了IPv6地址，UnassignIpv6Addresses可以回收一个或多个 IPv6 地址。|
|[AssignPrivateIpAddresses](cn.zh-CN/API参考/弹性网卡/AssignPrivateIpAddresses.md#)|为一块弹性网卡分配一个或多个辅助私有IPv4地址。可以为网卡指定在所属虚拟交换机（VSwitch）的CIDR私有IP地址，或者通过指定私有网络地址数量自动创建私有IP地址。|
|[UnassignPrivateIpAddresses](cn.zh-CN/API参考/弹性网卡/UnassignPrivateIpAddresses.md#)|从一块弹性网卡删除一个或多个辅助私有IPv4地址。|

## 系统事件相关接口 {#section_eqs_vyd_kgb .section}

|接口|描述|
|:-|:-|
|[DescribeDisksFullStatus](cn.zh-CN/API参考/系统事件/DescribeDisksFullStatus.md#)|查询磁盘的全部状态信息。|
|[CreateSimulatedSystemEvents](cn.zh-CN/API参考/系统事件/CreateSimulatedSystemEvents.md#)|为一台或多台ECS实例预约模拟系统事件。模拟系统事件相当于事件演习，不会真正执行事件，也不会对ECS实例产生影响。|
|[CancelSimulatedSystemEvents](cn.zh-CN/API参考/系统事件/CancelSimulatedSystemEvents.md#)|取消一件或多件处于`Scheduled`或`Executing`状态的模拟系统事件。取消系统事件后，模拟事件变为`Canceled`状态。|
|[DescribeInstancesFullStatus](cn.zh-CN/API参考/系统事件/DescribeInstancesFullStatus.md#)|查询实例的全状态信息。|
|[DescribeInstanceHistoryEvents](cn.zh-CN/API参考/系统事件/DescribeInstanceHistoryEvents.md#)|查询指定实例的已经处于非活跃状态的历史事件，指定查询事件的最大时长必须小于等于两个月。|

## 运维与监控相关接口 {#section_monitor_t2h_vdb .section}

|接口|描述|
|:-|:-|
|[DescribeDiskMonitorData](cn.zh-CN/API参考/运维与监控/DescribeDiskMonitorData.md#)|查询一块磁盘指定时间内的使用信息。|
|[DescribeInstanceMonitorData](cn.zh-CN/API参考/运维与监控/DescribeInstanceMonitorData.md#)|查询您某一台实例所有相关的监控信息，查询结果可以分页显示。|
|[GetInstanceScreenshot](cn.zh-CN/API参考/运维与监控/GetInstanceScreenshot.md#)|获取实例的截屏信息。|
|[GetInstanceConsoleOutput](cn.zh-CN/API参考/运维与监控/GetInstanceConsoleOutput.md#)|获取一台实例的系统命令行输出，数据以Base64编码后返回。|
|[DescribeEniMonitorData](cn.zh-CN/API参考/运维与监控/DescribeEniMonitorData.md#)|查询一块辅助网卡在指定时间段内使用的流量信息。|

## 云助手相关接口 {#section_cloudassistant_t2h_vdb .section}

|接口|描述|
|:-|:-|
|[CreateCommand](cn.zh-CN/API参考/云助手/CreateCommand.md#)|新建[云助手](../../../../cn.zh-CN/部署与运维/云助手/云助手概述.md#)命令。|
|[InvokeCommand](cn.zh-CN/API参考/云助手/InvokeCommand.md#)|为目标实例触发指定的命令。|
|[StopInvocation](cn.zh-CN/API参考/云助手/StopInvocation.md#)|停止实例中正在进行中（`Running`）的云助手命令进程。|
|[DeleteCommand](cn.zh-CN/API参考/云助手/DeleteCommand.md#)|删除已创建的云助手命令。|
|[DescribeCommands](cn.zh-CN/API参考/云助手/DescribeCommands.md#)|查询您已经创建的云助手命令。|
|[DescribeInvocations](cn.zh-CN/API参考/云助手/DescribeInvocations.md#)|查询您的实例中的云助手命令执行列表及状态。|
|[DescribeInvocationResults](cn.zh-CN/API参考/云助手/DescribeInvocationResults.md#)|查看云助手命令的执行结果，即在指定实例中的实际输出信息（Output）。|

## 标签相关接口 {#section_tag_t2h_vdb .section}

|接口|描述|
|:-|:-|
|[AddTags](cn.zh-CN/API参考/标签/AddTags.md#)|添加或者覆盖一个或者多个标签到云服务器ECS的各项资源上。|
|[RemoveTags](cn.zh-CN/API参考/标签/RemoveTags.md#)|从云服务器ECS资源上解绑一个或多个标签，例如，实例、磁盘、快照、镜像和安全组等。|
|[DescribeTags](cn.zh-CN/API参考/标签/DescribeTags.md#)|查询可以供您使用的标签。|
|[TagResources](cn.zh-CN/API参考/标签/TagResources.md#)|为指定的ECS资源列表统一创建并绑定标签。|
|[UntagResources](cn.zh-CN/API参考/标签/UntagResources.md#)|为指定的ECS资源列表统一解绑并删除标签。|
|[ListTagResources](cn.zh-CN/API参考/标签/ListTagResources.md#)|查询一个或多个ECS资源已经绑定的标签列表。|

## 地域相关接口 {#section_region_t2h_vdb .section}

|接口|描述|
|:-|:-|
|[DescribeRegions](cn.zh-CN/API参考/地域/DescribeRegions.md#)|查询您可以使用的阿里云地域。|
|[DescribeZones](cn.zh-CN/API参考/地域/DescribeZones.md#)|查询某一阿里云地域下的可用区。|
|[DescribeAvailableResource](cn.zh-CN/API参考/地域/DescribeAvailableResource.md#)|查询某一可用区的资源列表。|
|[DescribeResourcesModification](cn.zh-CN/API参考/地域/DescribeResourcesModification.md#)|查询升级和降配实例规格或者系统盘时，某一可用区的可用资源信息。|

## 其他接口 {#section_other_t2h_vdb .section}

|接口|描述|
|:-|:-|
|[CancelTask](cn.zh-CN/API参考/其他接口/CancelTask.md#)|取消一件正在运行的任务。|
|[DescribeTasks](cn.zh-CN/API参考/其他接口/DescribeTasks.md#)|查询指定的异步请求的进度。|
|[DescribeTaskAttribute](cn.zh-CN/API参考/其他接口/DescribeTaskAttribute.md#)|查询异步任务的详细信息。目前，可以查询的异步任务有导入镜像（[ImportImage](cn.zh-CN/API参考/镜像/ImportImage.md#)）和导出镜像（[ExportImage](cn.zh-CN/API参考/镜像/ExportImage.md#)）两种。|
|[DescribeAccountAttributes](cn.zh-CN/API参考/其他接口/DescribeAccountAttributes.md#)|查询您在一个阿里云地域下能创建的ECS资源上限。包括您能创建的安全组数量、弹性网卡数量、按量付费vCPU核数、抢占式实例vCPU核数、专用宿主机数量、地域网络类型以及账号是否已完成实名认证。|

