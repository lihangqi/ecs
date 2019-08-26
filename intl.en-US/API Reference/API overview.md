# API overview {#doc_9844 .concept}

The following tables list API operations available for use in ECS.

## Instances {#section_qgi_2ia_agq .section}

|Operation|Description|
|---------|-----------|
|[RunInstances](reseller.en-US/API Reference/Instances/RunInstances.md)|Creates one or more Pay-As-You-Go or subscription ECS instances.|
|[CreateInstance](reseller.en-US/API Reference/Instances/CreateInstance.md)|Creates an ECS instance.|
|[DescribeInstances](reseller.en-US/API Reference/Instances/DescribeInstances.md)|Queries the details of one or more ECS instances.|
|[StartInstance](reseller.en-US/API Reference/Instances/StartInstance.md)|Starts an ECS instance.|
|[RebootInstance](reseller.en-US/API Reference/Instances/RebootInstance.md)|Restarts an ECS instance.|
|[StopInstance](reseller.en-US/API Reference/Instances/StopInstance.md)|Stops an ECS instance.|
|[DeleteInstance](reseller.en-US/API Reference/Instances/DeleteInstance.md)|Releases a Pay-As-You-Go instance or a subscription ECS instance that expires.|
|[AttachInstanceRamRole](reseller.en-US/API Reference/Instances/AttachInstanceRamRole.md)|Attaches a RAM role to one or more ECS instances. You can only attach one RAM role to an ECS instance at any time. If the instance already has a RAM role, an error code is returned because another RAM role cannot be attached to the same instance.|
|[DetachInstanceRamRole](reseller.en-US/API Reference/Instances/DetachInstanceRamRole.md)|Detaches a RAM role from one or more ECS instances.|
|[DescribeInstanceStatus](reseller.en-US/API Reference/Instances/DescribeInstanceStatus.md)|Obtains the states of multiple ECS instances.|
|[RenewInstance](reseller.en-US/API Reference/Instances/RenewInstance.md)|Renews a subscription ECS instance.|
|[ReactivateInstances](reseller.en-US/API Reference/Instances/ReactivateInstances.md)|Restarts a Pay-As-You-Go ECS instance that is suspended because of overdue payments or has expired.|
|[RedeployInstance](reseller.en-US/API Reference/Instances/RedeployInstance.md)|Redeploys an ECS instance when the instance receives an event notification.|
|[DescribeInstanceVncUrl](reseller.en-US/API Reference/Instances/DescribeInstanceVncUrl.md)|Queries the Web management terminal URL of an ECS instance.|
|[DescribeUserData](reseller.en-US/API Reference/Instances/DescribeUserData.md)|Queries the user data of an ECS instance.|
|[DescribeInstanceAutoRenewAttribute](reseller.en-US/API Reference/Instances/DescribeInstanceAutoRenewAttribute.md)|Queries the auto renewal status of one or more subscription ECS instances.|
|[DescribeInstanceRamRole](reseller.en-US/API Reference/Instances/DescribeInstanceRamRole.md)|Queries RAM roles attached to one or more ECS instances.|
|[DescribeSpotPriceHistory](reseller.en-US/API Reference/Instances/DescribeSpotPriceHistory.md)|Queries the price history of the last 30 days for a preemptible instance.|
|[DescribeInstanceTypeFamilies](reseller.en-US/API Reference/Instances/DescribeInstanceTypeFamilies.md)|Queries the instance type families provided by ECS.|
|[DescribeInstanceTypes](reseller.en-US/API Reference/Instances/DescribeInstanceTypes.md)|Queries the instance type list provided by ECS.|
|[ModifyInstanceVpcAttribute](reseller.en-US/API Reference/Instances/ModifyInstanceVpcAttribute.md)|Modifies the VPC attributes of an ECS instance.|
|[ModifyInstanceAttribute](reseller.en-US/API Reference/Instances/ModifyInstanceAttribute.md)|Modifies the information of an ECS instance, such as the password, name, description, hostname, and user data. For a burstable performance instance \(t5\), you can also change its running mode.|
|[ModifyInstanceVncPasswd](reseller.en-US/API Reference/Instances/ModifyInstanceVncPasswd.md)|Modifies the Web management terminal password of an ECS instance.|
|[ModifyInstanceAutoReleaseTime](reseller.en-US/API Reference/Instances/ModifyInstanceAutoReleaseTime.md)|Sets or cancels the automatic release time for a Pay-As-You-Go ECS instance. Use caution when you set the automatic release time, because the instance is automatically released upon expiration.|
|[ModifyInstanceAutoRenewAttribute](reseller.en-US/API Reference/Instances/ModifyInstanceAutoRenewAttribute.md)|Sets one or more subscription ECS instances to the auto renewal status. To reduce the maintenance workload when an instance expires, you can set auto renewal for subscription ECS instances.|
|[ModifyInstanceChargeType](reseller.en-US/API Reference/Instances/ModifyInstanceChargeType.md)|Modifies the billing method for one or more ECS instances. You can change the billing method between Pay-As-You-Go and subscription, or change all Pay-As-You-Go data disks attached to an instance to subscription disks.|
|[ModifyInstanceSpec](reseller.en-US/API Reference/Instances/ModifyInstanceSpec.md)|Modifies the instance type or public bandwidth of a Pay-As-You-Go ECS instance.|
|[ModifyPrepayInstanceSpec](reseller.en-US/API Reference/Instances/ModifyPrepayInstanceSpec.md)|Modifies the type of your subscription ECS instance. The new instance type takes effect for the entire lifecycle of the instance.|

## Launch templates {#section_jxn_j1p_nw6 .section}

|Operation|Description|
|---------|-----------|
|[CreateLaunchTemplate](reseller.en-US/API Reference/Launch templates/CreateLaunchTemplate.md)|Creates an ECS instance launch template \(launch template for short\). An instance launch template removes the need to configure a large number of parameters every time you create an instance.|
|[CreateLaunchTemplateVersion](reseller.en-US/API Reference/Launch templates/CreateLaunchTemplateVersion.md)|Creates a new version for a specified ECS instance launch template.|
|[DeleteLaunchTemplate](reseller.en-US/API Reference/Launch templates/DeleteLaunchTemplate.md)|Deletes an ECS instance launch template.|
|[DeleteLaunchTemplateVersion](reseller.en-US/API Reference/Launch templates/DeleteLaunchTemplateVersion.md)|Deletes an ECS instance launch template version. This operation does not delete the default version of an ECS instance launch template. To delete the default version, you must call the DeleteLaunchTemplate operation.|
|[DescribeLaunchTemplates](reseller.en-US/API Reference/Launch templates/DescribeLaunchTemplates.md)|Queries one or more ECS instance launch templates.|
|[DescribeLaunchTemplateVersions](reseller.en-US/API Reference/Launch templates/DescribeLaunchTemplateVersions.md)|Queries one or more ECS instance launch template versions.|
|[ModifyLaunchTemplateDefaultVersion](reseller.en-US/API Reference/Launch templates/ModifyLaunchTemplateDefaultVersion.md)|Modifies the default version of an ECS instance launch template. If you do not specify a template version number when creating an ECS instance \(RunInstances\), the default version is used.|

## Auto provisioning groups {#section_xzj_fvi_g6o .section}

|Operation|Description|
|---------|-----------|
|[CreateAutoProvisioningGroup](reseller.en-US/API Reference/Auto provisioning group/CreateAutoProvisioningGroup.md)|Creates an auto provisioning group.|
|[ModifyAutoProvisioningGroup](reseller.en-US/API Reference/Auto provisioning group/ModifyAutoProvisioningGroup.md)|Modifies the configurations of an auto provisioning group.|
|[DeleteAutoProvisioningGroup](reseller.en-US/API Reference/Auto provisioning group/DeleteAutoProvisioningGroup.md)|Deletes an auto provisioning group.|
|[DescribeAutoProvisioningGroups](reseller.en-US/API Reference/Auto provisioning group/DescribeAutoProvisioningGroups.md)|Queries auto provisioning groups.|
|[DescribeAutoProvisioningGroupInstances](reseller.en-US/API Reference/Auto provisioning group/DescribeAutoProvisioningGroupInstances.md)|Queries ECS instances in an auto provisioning group.|
|[DescribeAutoProvisioningGroupHistory](reseller.en-US/API Reference/Auto provisioning group/DescribeAutoProvisioningGroupHistory.md)|Queries the scheduling tasks of an auto provisioning group.|

## Disks {#section_agf_aec_xie .section}

|Operation|Description|
|---------|-----------|
|[CreateDisk](reseller.en-US/API Reference/Disk/CreateDisk.md)|Creates a Pay-As-You-Go or subscription data disk. You can create a basic disk, an ultra disk, an SSD disk, or an ESSD disk.|
|[DeleteDisk](reseller.en-US/API Reference/Disk/DeleteDisk.md)|Releases a Pay-As-You-Go data disk. You can release a basic disk, an ultra disk, or an SSD disk.|
|[DescribeDisks](reseller.en-US/API Reference/Disk/DescribeDisks.md)|Queries the disks that you have created.|
|[AttachDisk](reseller.en-US/API Reference/Disk/AttachDisk.md)|Attaches a data disk to an ECS instance.|
|[DetachDisk](reseller.en-US/API Reference/Disk/DetachDisk.md)|Detaches a Pay-As-You-Go disk from an ECS instance. You can detach a basic disk, an ultra disk, or an SSD disk.|
|[ModifyDiskChargeType](reseller.en-US/API Reference/Disk/ModifyDiskChargeType.md)|Modifies the billing method for up to 16 disks that are attached to an ECS instance.|
|[ModifyDiskAttribute](reseller.en-US/API Reference/Disk/ModifyDiskAttribute.md)|Modifies the attributes of a disk.|
|[ReplaceSystemDisk](reseller.en-US/API Reference/Disk/ReplaceSystemDisk.md)|Replaces the system disk or the operating system of an ECS instance.|
|[ReInitDisk](reseller.en-US/API Reference/Disk/ReInitDisk.md)|Resets a disk to its initial state.|
|[ResetDisk](reseller.en-US/API Reference/Disk/ResetDisk.md)|Rolls back a disk to a specified disk state by using one of its historic disk snapshots.|
|[ResizeDisk](reseller.en-US/API Reference/Disk/ResizeDisk.md)|Resizes a cloud disk. You can resize both system disks and data disks.|
|[ModifyDiskSpec](reseller.en-US/API Reference/Disk/ModifyDiskSpec.md)|Upgrades the performance level of an ESSD disk.|

## Reserved instances {#section_cat_cse_92c .section}

|Operation|Description|
|---------|-----------|
|[PurchaseReservedInstancesOffering](reseller.en-US/API Reference/Reserved Instances/PurchaseReservedInstancesOffering.md)|Purchases reserved instances to pay for the CPU and memory usage fees of Pay-As-You-Go ECS instances.|
|[DescribeReservedInstances](reseller.en-US/API Reference/Reserved Instances/DescribeReservedInstances.md)|Queries the reserved instances that you have purchased.|
|[ModifyReservedInstances](reseller.en-US/API Reference/Reserved Instances/ModifyReservedInstances.md)|Modifies reserved instances.|

## Images {#section_3q0_tyv_7ka .section}

|Operation|Description|
|---------|-----------|
|[ExportImage](reseller.en-US/API Reference/Images/ExportImage.md)|Exports a custom image to an OSS bucket in the same region as the custom image.|
|[CreateImage](reseller.en-US/API Reference/Images/CreateImage.md)|Creates a custom image. You can use the created image to create ECS instances \(RunInstances\) and replace system disks \(ReplaceSystemDisk\).|
|[ImportImage](reseller.en-US/API Reference/Images/ImportImage.md)|Imports your locally saved image files to Alibaba Cloud ECS. Such images appears in the corresponding regions as custom images.|
|[CopyImage](reseller.en-US/API Reference/Images/CopyImage.md)|Copies a custom image from one region to another. You can use the copied image to create ECS instances \(RunInstances\) and replace system disks \(ReplaceSystemDisk\) in another region.|
|[CancelCopyImage](reseller.en-US/API Reference/Images/CancelCopyImage.md)|Cancels an ongoing CopyImage operation.|
|[DescribeImages](reseller.en-US/API Reference/Images/DescribeImages.md)|Queries available image resources.|
|[DeleteImage](reseller.en-US/API Reference/Images/DeleteImage.md)|Deletes a specified custom image.|
|[DescribeImageSharePermission](reseller.en-US/API Reference/Images/DescribeImageSharePermission.md)|Queries the accounts to which a custom image is shared. The response can be displayed over several pages. Ten entries are displayed on each page by default.|
|[ModifyImageAttribute](reseller.en-US/API Reference/Images/ModifyImageAttribute.md)|Modifies the name and description of a custom image.|
|[ModifyImageSharePermission](reseller.en-US/API Reference/Images/ModifyImageSharePermission.md)|Manages which accounts a custom image is shared to. After you share a custom image to other Alibaba Cloud accounts, these accounts can use the shared image to create ECS instances \(RunInstances\) and replace system disks \(ReplaceSystemDisk\).|
|[DescribeImageSupportInstanceTypes](reseller.en-US/API Reference/Images/DescribeImageSupportInstanceTypes.md)|Queries the instance types supported by the specified image.|

## Snapshots {#section_vay_o96_urw .section}

|Operation|Description|
|---------|-----------|
|[CreateSnapshot](reseller.en-US/API Reference/Snapshots/CreateSnapshot.md)|Creates a snapshot for a specified disk.|
|[CreateAutoSnapshotPolicy](reseller.en-US/API Reference/Snapshots/CreateAutoSnapshotPolicy.md)|Creates an automatic snapshot policy. After you create an automatic snapshot policy, you can call the ApplyAutoSnapshotPolicy operation to apply it to any disks. You can call the ModifyAutoSnapshotPolicyEx operation to modify an existing automatic snapshot policy as required.|
|[ApplyAutoSnapshotPolicy](reseller.en-US/API Reference/Snapshots/ApplyAutoSnapshotPolicy.md)|Applies an automatic snapshot policy to one or more disks. If you apply an automatic snapshot policy to a disk that already has an automatic snapshot policy, the new policy takes effect on the disk and replace the original policy.|
|[DeleteSnapshot](reseller.en-US/API Reference/Snapshots/DeleteSnapshot.md)|Deletes a snapshot. Snapshots that are currently being created can also be deleted by calling this operation.|
|[CancelAutoSnapshotPolicy](reseller.en-US/API Reference/Snapshots/CancelAutoSnapshotPolicy.md)|Cancels the automatic snapshot policies of one or more disks.|
|[DeleteAutoSnapshotPolicy](reseller.en-US/API Reference/Snapshots/DeleteAutoSnapshotPolicy.md)|Deletes an automatic snapshot policy. After you delete an automatic snapshot policy, the policy is no longer applied to the disks that it previously took effect on.|
|[DescribeAutoSnapshotPolicyEX](reseller.en-US/API Reference/Snapshots/DescribeAutoSnapshotPolicyEX.md)|Queries the automatic snapshot policies that you have created.|
|[DescribeSnapshots](reseller.en-US/API Reference/Snapshots/DescribeSnapshots.md)|Queries all the snapshots of an ECS instance or a disk. Request parameters such as InstanceId, DiskId, and SnapshotIds act as filtering conditions and are in a logical AND relationship.|
|[DescribeSnapshotLinks](reseller.en-US/API Reference/Snapshots/DescribeSnapshotLinks.md)|Queries the snapshot links of one or more disks. A snapshot chain is a chain of all the snapshots of a disk and a disk corresponds to a chain of snapshots. The snapshot chain ID is the same as the disk ID.|
|[ModifyAutoSnapshotPolicyEx](reseller.en-US/API Reference/Snapshots/ModifyAutoSnapshotPolicyEx.md)|Modifies an automatic snapshot policy. After you modify an automatic snapshot policy, the new policy takes effect immediately on the disks that have the policy applied.|
|[DescribeSnapshotsUsage](reseller.en-US/API Reference/Snapshots/DescribeSnapshotsUsage.md)|Queries the number of snapshots stored in a region and the total size of the snapshots. If you want to view the snapshot usage information on each disk in the current region, we recommend that you call the DescribeSnapshotLinks operation to query the snapshot chain information.|
|[DescribeSnapshotPackage](reseller.en-US/API Reference/Snapshots/DescribeSnapshotPackage.md)|Queries the storage plans that you have purchased within an Alibaba Cloud region. These storage plans can be used to store snapshots.|

## Security groups {#section_jf8_l64_log .section}

|Operation|Description|
|---------|-----------|
|[ModifySecurityGroupEgressRule](reseller.en-US/API Reference/Security groups/ModifySecurityGroupEgressRule.md)|Modifies the outbound rules of a security group. You can call the AuthorizeSecurityGroup operation to add a security group rule.|
|[CreateSecurityGroup](reseller.en-US/API Reference/Security groups/CreateSecurityGroup.md)|Creates a security group. Only instances within the security group are granted access permissions by default. If you want to allow requests from the Internet or requests from instances in other security groups, you can call the AuthorizeSecurityGroup operation to grant access permissions to these instances or groups.|
|[AuthorizeSecurityGroup](reseller.en-US/API Reference/Security groups/AuthorizeSecurityGroup.md)|Adds an inbound rule for a security group. This operation allows or blocks the inbound traffic from other devices to ECS instances in the security group.|
|[AuthorizeSecurityGroupEgress](reseller.en-US/API Reference/Security groups/AuthorizeSecurityGroupEgress.md)|Adds an outbound rule for a security group. This operation allows or blocks the outbound traffic from the ECS instances in the security group to other devices.|
|[RevokeSecurityGroup](reseller.en-US/API Reference/Security groups/RevokeSecurityGroup.md)|Deletes an inbound rule from a security group.|
|[RevokeSecurityGroupEgress](reseller.en-US/API Reference/Security groups/RevokeSecurityGroupEgress.md)|Deletes an outbound rule from a security group.|
|[JoinSecurityGroup](reseller.en-US/API Reference/Security groups/JoinSecurityGroup.md)|Adds an ECS instance to a specified security group.|
|[LeaveSecurityGroup](reseller.en-US/API Reference/Security groups/LeaveSecurityGroup.md)|Removes an ECS instance from a specified security group.|
|[DeleteSecurityGroup](reseller.en-US/API Reference/Security groups/DeleteSecurityGroup.md)|Deletes a security group. Before deleting a security group, make sure that no ECS instance exists in the security group and that the security group is not referenced by other security groups. Otherwise, the DeleteSecurityGroup request fails.|
|[DescribeSecurityGroupAttribute](reseller.en-US/API Reference/Security groups/DescribeSecurityGroupAttribute.md)|Queries the details of a security group.|
|[DescribeSecurityGroups](reseller.en-US/API Reference/Security groups/DescribeSecurityGroups.md)|Queries the basic information of your security groups, such as security group IDs and descriptions. Security groups are displayed in descending order of their IDs.|
|[DescribeSecurityGroupReferences](reseller.en-US/API Reference/Security groups/DescribeSecurityGroupReferences.md)|Queries whether a specified security group has been authorized by other security groups.|
|[ModifySecurityGroupAttribute](reseller.en-US/API Reference/Security groups/ModifySecurityGroupAttribute.md)|Modifies the attributes of a security group, including its name and description.|
|[ModifySecurityGroupPolicy](reseller.en-US/API Reference/Security groups/ModifySecurityGroupPolicy.md)|Modifies the access control policy of a security group.|
|[ModifySecurityGroupRule](reseller.en-US/API Reference/Security groups/ModifySecurityGroupRule.md)|Modifies the inbound rules of a security group. You can call the AuthorizeSecurityGroup operation to add a security group rule.|

## Deployment sets {#section_cpi_uva_ga4 .section}

|Operation|Description|
|---------|-----------|
|[CreateDeploymentSet](reseller.en-US/API Reference/Deployment sets/CreateDeploymentSet.md)|Creates a deployment set in the specified region.|
|[ModifyInstanceDeployment](reseller.en-US/API Reference/Deployment sets/ModifyInstanceDeployment.md)|Migrates an ECS instance to a DDH in the same region.|
|[ModifyDeploymentSetAttribute](reseller.en-US/API Reference/Deployment sets/ModifyDeploymentSetAttribute.md)|Modifies the name and description of a deployment set.|
|[DeleteDeploymentSet](reseller.en-US/API Reference/Deployment sets/DeleteDeploymentSet.md)|Deletes a deployment set.|
|[DescribeDeploymentSets](reseller.en-US/API Reference/Deployment sets/DescribeDeploymentSets.md)|Queries attributes of one or more deployment sets.|

## SSH key pairs {#section_2x5_hp3_lk2 .section}

|Operation|Description|
|---------|-----------|
|[CreateKeyPair](reseller.en-US/API Reference/SSH key pairs/CreateKeyPair.md)|Creates an SSH key pair. The system stores the public key and returns the unencrypted private key. The private key is encoded by using PEM and is in the PKCS\#8 format. You must store the private key on your own and guarantee its confidentiality.|
|[ImportKeyPair](reseller.en-US/API Reference/SSH key pairs/ImportKeyPair.md)|Imports the public key of an RSA-encrypted key pair that was created by other key pair generators. After the public key is imported, you must store the private key on your own and its guarantee confidentiality.|
|[AttachKeyPair](reseller.en-US/API Reference/SSH key pairs/AttachKeyPair.md)|Attaches an SSH key pair to one or more Linux instances.|
|[DetachKeyPair](reseller.en-US/API Reference/SSH key pairs/DetachKeyPair.md)|Detaches an SSH key pair from one or more Linux instances.|
|[DeleteKeyPairs](reseller.en-US/API Reference/SSH key pairs/DeleteKeyPairs.md)|Deletes one or more SSH key pairs. The entry of a deleted SSH key pair is removed from the database. However, the instances to which the SSH key pair is attached can still use the SSH key pair.|
|[DescribeKeyPairs](reseller.en-US/API Reference/SSH key pairs/DescribeKeyPairs.md)|Queries one or more SSH key pairs.|

## Network configurations {#section_uxh_hxh_lyb .section}

|Operation|Description|
|---------|-----------|
|[AllocatePublicIpAddress](reseller.en-US/API Reference/Networks/AllocatePublicIpAddress.md)|Assigns a public IP address to an ECS instance.|
|[ConvertNatPublicIpToEip](reseller.en-US/API Reference/Networks/ConvertNatPublicIpToEip.md)|Converts the public IP address of a VPC-type ECS instance to an EIP.|
|[AttachClassicLinkVpc](reseller.en-US/API Reference/Networks/AttachClassicLinkVpc.md)|Establishes a ClassicLink between a classic network-type instance and a VPC to allow the instance to communicate with resources in the VPC over the internal network. For more information, see ClassicLink overview in VPC User Guide.|
|[DetachClassicLinkVpc](reseller.en-US/API Reference/Networks/DetachClassicLinkVpc.md)|Removes the ClassicLink between a classic network-type instance and a VPC. For more information, see ClassicLink overview in VPC User Guide. After the ClassicLink is removed, the classic network-type instance cannot communicate with the VPC.|
|[DescribeBandwidthLimitation](reseller.en-US/API Reference/Networks/DescribeBandwidthLimitation.md)|Queries available bandwidth resources.|
|[DescribeClassicLinkInstances](reseller.en-US/API Reference/Networks/DescribeClassicLinkInstances.md)|Queries one or more classic network-type instances that have established ClassicLink with VPCs.|
|[ModifyInstanceNetworkSpec](reseller.en-US/API Reference/Networks/ModifyInstanceNetworkSpec.md)|Modifies the bandwidth configurations of an ECS instance. When the network specifications of an ECS instance cannot meet your needs, you can modify its bandwidth configurations to improve network performance.|

## ENIs {#section_vx8_gtz_yjf .section}

|Operation|Description|
|---------|-----------|
|[CreateNetworkInterface](reseller.en-US/API Reference/Elastic network interfaces/CreateNetworkInterface.md)|Creates an ENI.|
|[AttachNetworkInterface](reseller.en-US/API Reference/Elastic network interfaces/AttachNetworkInterface.md)|Attaches an ENI to a VPC-type instance.|
|[AssignPrivateIpAddresses](reseller.en-US/API Reference/Elastic network interfaces/AssignPrivateIpAddresses.md)|Assigns one or more secondary private IP addresses to an ENI. Specifically, you can specify private IP addresses within the CIDR block of the VSwitch to which an ENI belongs, or the number of private IP addresses for ECS to assign them automatically.|
|[UnassignPrivateIpAddresses](reseller.en-US/API Reference/Elastic network interfaces/UnassignPrivateIpAddresses.md)|Deletes one or more secondary private IP addresses from an ENI.|
|[DetachNetworkInterface](reseller.en-US/API Reference/Elastic network interfaces/DetachNetworkInterface.md)|Detaches an ENI from an ECS instance.|
|[DeleteNetworkInterface](reseller.en-US/API Reference/Elastic network interfaces/DeleteNetworkInterface.md)|Deletes an ENI.|
|[DescribeNetworkInterfaces](reseller.en-US/API Reference/Elastic network interfaces/DescribeNetworkInterfaces.md)|Queries available ENIs.|
|[ModifyNetworkInterfaceAttribute](reseller.en-US/API Reference/Elastic network interfaces/ModifyNetworkInterfaceAttribute.md)|Modifies the attributes of an ENI. You can modify the name, description, and security group of the ENI.|

## System events {#section_era_0mo_yvs .section}

|Operation|Description|
|---------|-----------|
|[DescribeInstancesFullStatus](reseller.en-US/API Reference/System event/DescribeInstancesFullStatus.md)|Queries the full status information of one or more ECS instances. The full status information is made up of the instance status and the instance event status. The instance status is the lifecycle status of the instance. The instance event status is the health status of the maintenance event. For more information, see ECS instance lifecycle and System events.|
|[DescribeInstanceHistoryEvents](reseller.en-US/API Reference/System event/DescribeInstanceHistoryEvents.md)|Queries the system events of the specified ECS instance. You can query system events within the last week. You can specify the InstanceEventCycleStatus parameter to query system events that are in the Scheduled or Executing state.|
|[DescribeDisksFullStatus](reseller.en-US/API Reference/System event/DescribeDisksFullStatus.md)|Queries the full status information of one or more disks.|
|[CancelSimulatedSystemEvents](reseller.en-US/API Reference/System event/CancelSimulatedSystemEvents.md)|Cancels one or more simulated system events that are in the Scheduled or Executing state. After you cancel a simulated system event, the simulated event is in the Canceled state.|
|[CreateSimulatedSystemEvents](reseller.en-US/API Reference/System event/CreateSimulatedSystemEvents.md)|Schedules simulated system events for one or more ECS instances. The simulated system events do not occur in the actual system and the simulation does not affect ECS instances.|

## O&M and monitoring {#section_qha_80y_png .section}

|Operation|Description|
|---------|-----------|
|[DescribeEniMonitorData](reseller.en-US/API Reference/Operations and monitoring/DescribeEniMonitorData.md)|Queries traffic information of a secondary ENI over a specific period.|
|[DescribeDiskMonitorData](reseller.en-US/API Reference/Operations and monitoring/DescribeDiskMonitorData.md)|Queries the usage information of a specified disk over a specific period. You can query the read IOPS, write IOPS, read bandwidth \(Byte/s\), write bandwidth \(Byte/s\), read latency \(ms\), and write latency \(ms\) of the disk. A portion of the information may be missing. This is because the system cannot obtain the relevant information, such as when the disk is not in the In Use state.|
|[DescribeInstanceMonitorData](reseller.en-US/API Reference/Operations and monitoring/DescribeInstanceMonitorData.md)|Queries all the monitoring data of an ECS instance. You can query the CPU usage, inbound data traffic, outbound data traffic, network traffic, and average bandwidth of the ECS instance. A portion of the information may be missing. This is because the system cannot obtain the relevant information, such as when the instance is in the Stopped state.|
|[GetInstanceScreenshot](reseller.en-US/API Reference/Operations and monitoring/GetInstanceScreenshot.md)|Obtains the screenshot information of an ECS instance.|
|[GetInstanceConsoleOutput](reseller.en-US/API Reference/Operations and monitoring/GetInstanceConsoleOutput.md)|Obtains the command line output of an ECS instance. The returned output is encoded in Base64.|

## Cloud assistant {#section_nds_h39_z6y .section}

|Operation|Description|
|---------|-----------|
|[CreateCommand](reseller.en-US/API Reference/Cloud assistant/CreateCommand.md)|Creates a cloud assistant command.|
|[InstallCloudAssistant](reseller.en-US/API Reference/Cloud assistant/InstallCloudAssistant.md)|Installs the cloud assistant client on one or more ECS instances.|
|[InvokeCommand](reseller.en-US/API Reference/Cloud assistant/InvokeCommand.md)|Triggers a cloud assistant command on one or more ECS instances.|
|[StopInvocation](reseller.en-US/API Reference/Cloud assistant/StopInvocation.md)|Stops the process of a running cloud assistant command on one or more ECS instances.|
|[DeleteCommand](reseller.en-US/API Reference/Cloud assistant/DeleteCommand.md)|Deletes a cloud assistant command.|
|[DescribeCloudAssistantStatus](reseller.en-US/API Reference/Cloud assistant/DescribeCloudAssistantStatus.md)|Checks whether the cloud assistant client is installed on one or more instances.|
|[DescribeCommands](reseller.en-US/API Reference/Cloud assistant/DescribeCommands.md)|Queries the cloud assistant commands that you have created. If you only specify the Action and RegionId parameters, all available commands are displayed.|
|[DescribeInvocations](reseller.en-US/API Reference/Cloud assistant/DescribeInvocations.md)|Queries the invocation information and status of cloud assistant commands.|
|[DescribeInvocationResults](reseller.en-US/API Reference/Cloud assistant/DescribeInvocationResults.md)|Queries the invocation result of a cloud assistant command, or the actual output on a specified ECS instance.|

## Tags {#section_79i_o7d_zum .section}

|Operation|Description|
|---------|-----------|
|[TagResources](reseller.en-US/API Reference/Tags/TagResources.md)|Creates and attaches tags to the specified ECS resources.|
|[ListTagResources](reseller.en-US/API Reference/Tags/ListTagResources.md)|Queries tags that are attached to one or more ECS resources.|
|[UntagResources](reseller.en-US/API Reference/Tags/UntagResources.md)|Detaches and deletes tags from the specified ECS resources.|

## Regions {#section_ykr_fmw_kcg .section}

|Operation|Description|
|---------|-----------|
|[DescribeRegions](reseller.en-US/API Reference/Regions/DescribeRegions.md)|Queries the Alibaba Cloud regions available to you.|
|[DescribeZones](reseller.en-US/API Reference/Regions/DescribeZones.md)|Queries zones available in a specified region.|
|[DescribeResourcesModification](reseller.en-US/API Reference/Regions/DescribeResourcesModification.md)|Queries resources available in a certain zone upon upgrading or downgrading an ECS instance type or system disk.|
|[DescribeAvailableResource](reseller.en-US/API Reference/Regions/DescribeAvailableResource.md)|Queries resources available in a certain zone. For example, you can view resources available in a certain zone before creating an ECS instance \(RunInstances\) or modify the instance type \(ModifyInstanceSpec\).|

## Other operations {#section_lip_cie_w96 .section}

|Operation|Description|
|---------|-----------|
|[CancelTask](reseller.en-US/API Reference/Others/CancelTask.md)|Cancels an ongoing task. You can cancel the following asynchronous tasks: importing images \(ImportImage\) and exporting images \(ExportImage\).|
|[DescribeTasks](reseller.en-US/API Reference/Others/DescribeTasks.md)|Queries the progress of one or more asynchronous tasks.|
|[DescribeTaskAttribute](reseller.en-US/API Reference/Others/DescribeTaskAttribute.md)|Queries the details of a specified asynchronous task. You can query the following asynchronous tasks: importing images \(ImportImage\) and exporting images \(ExportImage\).|
|[DescribeAccountAttributes](reseller.en-US/API Reference/Others/DescribeAccountAttributes.md)|Queries the maximum number of ECS resources that you can create in a region. Specifically, you can query the maximum number of security groups, ENIs, Pay-As-You-Go instance vCPUs, preemptible instance vCPUs, and Dedicated Hosts \(DDHs\), local network type, and whether your account has been authenticated with real-name credentials.|

