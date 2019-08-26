# RunInstances {#doc_api_1161594 .reference}

Creates one or more Pay-As-You-Go or Subscription ECS instances.

## Description {#description .section}

Before creating an instance, you can call the [DescribeAvailableResource](~~66186~~) action to view the available resources in the specified region or zone.

You must fully understand the ECS billing methods before you create an instance, because resource billing is involved when creating instances. For more information, see [Billing overview](~~25398~~).

When you call this action, note that:

-   You can create a maximum of 100 instances at a time.
-   You can use the `AutoReleaseTime` parameter to set the automatic release time of the instance.
-   After the instance is created, you can call the [DescribeInstances](~~25506~~) action to check the status of the new instance.
-   Before creating an instance, make sure you have created a security group. For more information, see [CreateSecurityGroup](~~25553~~).
-   An instance is enabled automatically after it is created. It is ready to use when it is in the `Running` state.
-   Before creating a VPC-based instance, you must [create a VPC](~~65430~~) in the same region.
-   Unlike [CreateInstance](~~25499~~), when you call `RunInstances` to create an instance, a public IP address is configured for it if the value of `InternetMaxBandwidthOut` is greater than 0.
-   After you submit the instance creation task, an error is returned if the parameters are invalid or no resources are available. For more information, see Error codes.

**Best practice**

`RunInstances` can be called to create multiple instances at a time. For the sake of future management and retrieval, we recommend that you specify the `Tag.N.Key` and `Tag.N.Value` tags for instances created in each batch creation task. For their `HostName` and `InstanceName` values, we recommend that you add `UniqueSuffix`.

An instance launch template allows you to automatically set configuration parameters that are used each time you create a new instance. You can all the [CreateLaunchTemplate](~~74686~~) action to create an instance launch template. After that, you can specify `RunInstances` and `LaunchTemplateId` in `LaunchTemplateVersion` to enable this template.

You can use the [ECS console](https://ecs.console.aliyun.com/) to obtain `RunInstances` best practices when creating an ECS instance. When you confirm the order, in the **API Workflow** pane at the left side, the APIs and request parameters that can be associated with `RunInstances` are listed. At the right side, the programming language-specific examples are provided. **Java** and **Python** examples are available.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=RunInstances) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required?|Example|Description|
|----|----|---------|-------|-----------|
|RegionId|String|Yes|cn-hangzhou| The region ID of the instance. You can call the [DescribeRegions](~~25609~~) action to view the latest region list.

 |
|Action|String|No|RunInstances| The operation that you want to perform. Set the value to RunInstances.

 |
|ZoneId|String|No|cn-hangzhou-b| The zone ID that is available in the specified region. You can call the [DescribeZones](~~25610~~) action to obtain the latest zone list. It is allocated randomly by the system by default.

 |
|ImageId|String|No|win2008r2\_64\_ent\_sp1\_en-us\_40G\_alibase\_20170915.vhd| The ID of the image resource that you specify when you create the instance. You can call the [DescribeImages](~~25534~~) action to view the image resources available. If you do not use `LaunchTemplateId` or `LaunchTemplateName` to specify an instance launch template, `ImageId` is required.

 |
|SecurityGroupId|String|No|sg-bp15ed6xe1yxeycg7ov3| The ID of the security group to which the instance belongs. Instances in the same security group can access each other. One security group can contain a maximum of 1,000 instances.

 **Note:** SecurityGroupId determines the network type of its instances. For example, if a security group is of the VPC type, its instances must be of the VPC type. You must also specify VSwitchId for them.

 If you do not use `LaunchTemplateId` or `LaunchTemplateName` to specify an instance launch template, `SecurityGroupId` is required.

 |
|VSwitchId|String|No|vsw-bp1s5fnvk4gn2tws03ziX| The ID of the VSwitch. It must be specified when you create VPC-based instances.

 |
|InstanceType|String|No|ecs.g5.large| The type of the instance. For more information, see [Instance type families](~~25378~~), or call the [DescribeInstanceTypes](~~25620~~) action to obtain the latest instance type list. If you do not use LaunchTemplateId or LaunchTemplateName to specify an instance launch template, InstanceType is required.

 |
|InternetMaxBandwidthIn|Integer|No|200| The maximum inbound bandwidth for the public network. Unit: Mbit/s. Valid values: 1 to 200.

 Default value: 200.

 |
|InternetMaxBandwidthOut|Integer|No|5| The maximum outbound bandwidth for the public network. Unit: Mbit/s. Valid values: 0 to 100.

 Default value: 0.

 |
|InstanceName|String|No|JoshuaHost| The name of the instance. It must be 2 to 128 characters in length and can contain uppercase and lowercase letters, digits, colons \(:\), underscores \(\_\), and hyphens \(-\). It must start with a letter. It cannot start with http:// or https://. `InstanceId` is used by default.

 **Note:** When batch creating instances, you can use `UniqueSuffix` to set different `InstanceName` values for the instances.

 |
|HostName|String|No|JoshuaHost| The hostname of the instance.

 -   It cannot start or end with a period \(.\) or a hyphen \(-\). It cannot contain consecutive periods \(.\) or hyphens \(-\).
-   For Windows: The hostname must be 2 to 15 characters in length and can contain uppercase and lowercase letters, digits, periods \(.\), and hyphens \(-\). It cannot only contain digits.
-   For other operating systems: The hostname must be 2 to 64 characters in length and can contain uppercase and lowercase letters, digits, and hyphens \(-\). It can be segments separated by periods \(.\).

 **Note:** When batch creating instances, you can use `UniqueSuffix` to set different `HostName` values for the instances.

 |
|UniqueSuffix|Boolean|No|true| Indicates whether to add sequential suffixes to `HostName` and `InstanceName` values. The sequential suffix ranges from 001 to 999. Example: `LocalHost001`, `LocalHost002`, `MyInstance001`, and `MyInstance002`. Default value: false.

 |
|Description|String|No|FinanceDept| The description of the instance. It must be 2 to 256 characters in length. It cannot start with http:// or https://.

 |
|PasswordInherit|Boolean|No|false| Indicates whether to use the password predefined in the image. If PasswordInherit is specified, the Password must be null. Make sure that the selected image has a password configured.

 |
|Password|String|No|EcsV587!| The password of the instance. It must be 8 to 30 characters in length, and must be a combination of uppercase and lowercase letters, digits, and special characters. The following special characters can be used:

 ``` {#codeblock_m6d_1gw_mc1}
()`~!@#$%^&*-_+=|{}[]:;'<>,.?/
```

 For Windows, the password cannot start with a forward slash \(/\).

 **Note:** If `Password` is specified, we recommend that you send requests over the HTTPS protocol to keep the password confidential.

 |
|KeyPairName|String|No|Instancetest| The name of the key pair.

 -   For Windows instances, ignore this parameter. Default value: null. Even if this parameter is specified, the `Password` value is used.
-   For Linux instances, the password logon method is forbidden during initialization.

 |
|SystemDisk.Size|String|No|40| The size of the system disk. Unit: GiB. Valid values: 20 to 500.

 This value must be equal to or greater than max \{20, ImageSize\}. Default value: max \{40, ImageSize\}.

 |
|SystemDisk.Category|String|No|cloud\_ssd| The category of the system disk. The default value of the non-optimized instance for [phased-out instance types](~~55263~~) for which I/O optimization is not performed is cloud. The default value for other instances is cloud\_efficiency. Valid values:

 -   cloud: basic disk.
-   cloud\_efficiency: ultra disk.
-   cloud\_ssd: SSD.
-   ephemeral\_ssd: local SSD.
-   cloud\_essd: ESSD. ESSDs are still in the public beta test phase and only available in some regions. For more information, see [ESSD FAQ](~~64950#AvailableRegion~~).

 |
|SystemDisk.DiskName|String|No|cloud\_ssdSystem| The name of the system disk. It must be 2 to 128 characters in length and can contain uppercase and lowercase letters, digits, colons \(:\), underscores \(\_\), and hyphens \(-\). It must start with a letter. It cannot start with http:// or https://. Default value: null.

 |
|SystemDisk.Description|String|No|FinanceDept| The description of the system disk. It must be 2 to 256 characters in length. It cannot start with http:// or https://.

 |
|DataDisk.N.Size|Integer|No|2,000| The size of the nth data disk. n ranges from 1 to 16. Unit: GiB. Valid values:

 -   cloud: 5 to 2,000.
-   cloud\_efficiency: 20 to 32,768.
-   cloud\_ssd: 20 to 32,768.
-   cloud\_essd: 20 to 32,768.
-   ephemeral\_ssd: 5 to 800.

 This value must be equal to or greater than the size of `SnapshotId`.

 |
|DataDisk.N.SnapshotId|String|No|s-bp17441ohwka0yuhx3h0| The ID of the snapshot used to create the nth data disk. n ranges from 1 to 16. When `DataDisk.N.SnapshotId` is specified, the value of `DataDisk.N.Size` is ignored. The size of the new data disk is equal to that of the specified snapshot. Those snapshots created on or before July 15, 2013 cannot be used here. Otherwise, an error will be returned and your request will be rejected.

 |
|DataDisk.N.Category|String|No|cloud\_ssd| The category of the nth data disk. Default value: cloud. Valid values:

 -   cloud: basic disk.
-   cloud\_efficiency: ultra disk.
-   cloud\_ssd: SSD.
-   ephemeral\_ssd: local SSD.
-   cloud\_essd: ESSD. ESSDs are still in the public beta test phase and only available in some regions. For more information, see [ESSD FAQ](~~64950#AvailableRegion~~).

 |
|DataDisk.N.Encrypted|String|No|false| Indicates whether the nth data disk is encrypted. Default value: false.

 |
|DataDisk.N.KMSKeyId|String|No|0e478b7a-4262-4802-b8cb-00d3fb40826X| The KMS ID for the nth data disk.

 |
|DataDisk.N.DiskName|String|No|cloud\_ssdData| The name of the nth data disk. It must be 2 to 128 characters in length and can contain uppercase and lowercase letters, digits, colons \(:\), underscores \(\_\), and hyphens \(-\). It must start with a letter. It cannot start with http:// or https://. Default value: null.

 |
|DataDisk.N.Description|String|No|FinanceDept| The description of the nth data disk. It must be 2 to 256 characters in length. It cannot start with http:// or https://.

 |
|DataDisk.N.Device|String|No|/dev/vda| The mount point of the nth data disk.

 **Note:** This parameter will be removed in the future. We recommend that you use other parameters to ensure compatibility.

 |
|DataDisk.N.DeleteWithInstance|Boolean|No|true| Indicates whether the data disk is released along with the instance. Default value: true.

 |
|IoOptimized|String|No|optimized| Specifies whether the instance is an I/O optimized instance. The default value for [phased-out instance types](~~55263~~) is none, while that for other instances is optimized. Valid values:

 -   none.
-   optimized.

 |
|NetworkInterface.N.PrimaryIpAddress|String|No|172.16.236.14X| The primary IP address of the nth ENI.

 |
|NetworkInterface.N.VSwitchId|String|No|vsw-vswitchid2| The ID of the VSwitch for the nth ENI.

 |
|NetworkInterface.N.SecurityGroupId|String|No|sg-securitygroupid2| The ID of security group for the nth ENI.

 |
|NetworkInterface.N.NetworkInterfaceName|String|No|FinanceJoshua| The name of the nth ENI.

 |
|NetworkInterface.N.Description|String|No|FinanceDept| The description of the nth ENI. It must be 2 to 256 characters in length. It cannot start with http:// or https://.

 |
|RamRoleName|String|No|FinanceDept| The RAM role name for the instance. You can call the [ListRoles](~~28713~~) action to view RAM roles for the specified instance.

 |
|UserData|String|No|ZWNobyBoZWxsbyBlY3Mh| The user data of the instance. It must be encoded in Base64. The maximum size of the user data is 16 KB.

 |
|MinAmount|Integer|No|2| The minimum number of the specified instances to purchase. Valid values: 1 to 100.

 -   If the number of ECS instances in stock is lower than the MinAmount value, the instance creation operation fails.
-   If the number of ECS instances in stock is equal to or greater than the MinAmount value, the instance creation operation succeeds.

 |
|Amount|Integer|No|3| The specified number of instances you want to create. Valid values: 1 to 100.

 Default value: 1.

 |
|SpotPriceLimit|Float|No|0.97| The maximum hourly price for the instance. It is precise up to three decimal places. It is valid only when `SpotStrategy` is set to `SpotWithPriceLimit`.

 |
|SpotStrategy|String|No|NoSpot| The preemption policy of the Pay-As-You-Go instance. The parameter is valid only when `InstanceChargeType` is set to `PostPaid`. Valid values:

 -   NoSpot: a standard Pay-As-You-Go instance.
-   SpotWithPriceLimit: a preemptible instance with the upper price limit defined.
-   SpotAsPriceGo: a Pay-As-You-Go instance with its price based on the current market price.

 |
|SpotInterruptionBehavior|String|No|Terminate| The interruption mode of the preemptible instance. Only the Terminate mode is supported, in which the instance is released.

 |
|CreditSpecification|String|No|Standard| The running mode of the burstable performance instance \(t5\). Valid values:

 -   Standard: standard mode. For more information, see [Standard mode](Standard mode../DNECS19100341/EN-US_TP_9554.dita#concept_n52_3v2_5db).
-   Unlimited: unlimited mode. For more information, see [Unlimited mode](Unlimited mode../DNECS19100341/EN-US_TP_9554.dita#concept_n52_3v2_5db).

 Default value: null

 |
|SecurityEnhancementStrategy|String|No|Active| Indicates whether to enable security hardening. Valid values:

 -   Active: enables security hardening. It is applicable only to Alibaba Cloud public images.
-   Deactive: disables security hardening. It is applicable to all images.

 |
|DeploymentSetId|String|No|ds-bp1brhwhoqinyjd6tnXX| The ID of the deployment set.

 |
|DedicatedHostId|String|No|dh-dedicatedhost1| Indicates whether to create an ECS instance on the specified Dedicated Host \(DDH\). You can call the [DescribeDedicatedHosts](~~94572~~) action to view the DDH list.

 No preemptible instances can be created on the DDH. Therefore, if you specify `DedicatedHostId`, the values of `SpotStrategy` and `Spotpricelimit` will be ignored.

 |
|Tag.N.Key|String|No|FinanceDept| The tag key of the instance, disk, and primary NIC. n ranges from 1 to 20. This parameter cannot be left empty. It must be no more than 64 characters in length. It cannot start with `aliyun` or `acs:`, and cannot contain `http://` or `https://`.

 |
|Tag.N.Value|String|No|FinanceDept.Joshua| The tag value of the instance, disk, and primary NIC. n ranges from 1 to 20. This parameter can be left empty. It must be no more than 128 characters in length. It cannot start with `aliyun` or `acs:`, and cannot contain `http://` or `https://`.

 |
|HpcClusterId|String|No|hpc-clusterid| The ID of the EHPC cluster to which the instance belongs.

 |
|ResourceGroupId|String|No|rg-resourcegroupid1| The ID of the resource group to which the instance belongs.

 |
|LaunchTemplateId|String|No|lt-bp1apo0bbbkuy0rj3b9X| The ID of the instance launch template. For more information, call [DescribeLaunchTemplates](~~73759~~). You must use `LaunchTemplateId` or `LaunchTemplateName` to specify the instance launch template.

 |
|LaunchTemplateName|String|No|JoshuaWinPostPaid| The name of the instance launch template. You must use `LaunchTemplateId` or `LaunchTemplateName` to specify the instance launch template.

 |
|LaunchTemplateVersion|Long|No|3| The version of the instance launch template. If you specify `LaunchTemplateId` or `LaunchTemplateName`, but skip LaunchTemplateVersion, the default template version is used.

 |
|DeletionProtection|Boolean|No|false| The release protection attribute of the instance. It indicates whether you can use the ECS console or call the [DeleteInstance](~~25507~~) action to release the instance. Default value: false. Valid values:

 -   true: enables release protection.
-   false: disables release protection.

 **Note:** This attribute is applicable only to Pay-As-You-Go instances. It can only be used to block manual release operations, but not automatic release operations by the system.

 |
|AutoReleaseTime|String|No|2018-01-01T12:05:00Z| The automatic release time of the instance. The time follows the [ISO 8601](~~25696~~) standard and is in UTC time. Format: yyyy-MM-ddTHH:mm:ssZ.

 -   If `ss` is set to a value other than `00`, only the value of `mm` is used, with ss changed to 00.
-   The automatic release time must be at least half an hour later than the current time.
-   The automatic release time must be less than 3 years from the current time.

 |
|InternetChargeType|String|No|PayByTraffic| The billing method of the instance. Default value: PayByTraffic. Valid values:

 -   PayByTraffic: charged based on actual traffic.

 |
|Period|Integer|No|1| The subscription period of the instance. Unit: month. The parameter is valid and required only when `InstanceChargeType` is set to `PrePaid`. If DedicatedHostId is specified, the value range of the Period parameter must be within the subscription period of the DDH. Valid values:

 -   ``\{“1”, “2”, “3”, “4”\} if PeriodUnit is set to Week.
-   ``\{ “1”, “2”, “3”, “4”, “5”, “6”, “7”, “8”, “9”, “12”, “24”, “36”,”48”,”60”\} if PeriodUnit is set to Month.

 |
|AutoRenew|Boolean|No|true| Indicates whether to enable automatic renewal. The parameter is valid only when `InstanceChargeType` is set to `PrePaid`. Default value: false. Valid values:

 -   true.
-   false.

 |
|PeriodUnit|String|No|Month| The unit of the subscription period. Default value: Month. Valid values:

 -   Week
-   Month

 |
|AutoRenewPeriod|Integer|No|1| The automatic renewal period of the instance. Valid values:

 -   ``\{“1”, “2”, “3”\} if PeriodUnit is set to Week.
-   ``\{"1", "2", "3", "12", "24", "36","48", "60"\} if PeriodUnit is set to Month.

 Default value: 1.

 |
|InstanceChargeType|String|No|PrePaid| The billing method of the instance. Default value: PostPaid. Valid values:

 -   PrePaid: subscription.
-   PostPaid: Pay-As-You-Go.

 If it is set to PrePaid, you must confirm that your payment account has sufficient credit. Otherwise, the `InvalidPayMethod` error code is returned.

 |
|Ipv6AddressCount|Integer|No|1| The number of randomly generated IPv6 addresses which are allocated to the ENI.

 **Note:** You cannot specify both `Ipv6Addresses.N` and `Ipv6AddressCount`.

 |
|PrivateIpAddress|String|No|172.16.236.14X| The private IP address of the instance. PrivateIpAddress depends on VSwitchId and cannot be specified separately.

 **Note:** When `PrivateIpAddress` is specified, `Amount` can only be set to 1.

 |
|Ipv6Address.N|RepeatList|No|Ipv6Address. 1=2001:db8:1234:1a00::XXX| Allocates one or more IPv6 addresses to the ENI. N can only be 1.

 Sample:``

 **Note:** You cannot specify both `Ipv6Addresses.N` and `Ipv6AddressCount`.

 |
|DryRun|Boolean|No|false| Indicates whether to send a check request only. Default value: false.

 -   true: Only a check request is sent and no instance is created. The system checks whether the required parameters are set, and verifies the request format, service limits, and available ECS instances. If the check fails, the corresponding error code is returned. If the check succeeds, the `DryRunOperation` error code is returned.
-   false: A request is sent and then the instance is created.

 |
|ClientToken|String|No|123e4567-e89b-12d3-a456-426655440000| The token used to ensure idempotence. You can generate the token in your client, but you must ensure that it is globally unique.**ClientToken** can contain only ASCII characters. It must be no more than 64 characters in length. For more information, see [How to ensure idempotence](~~25693~~).

 |
|Affinity|String|No|default| Indicates whether to associate an ECS instance with the DDH on which the instance is created. Valid values:

 -   default: The instance is not associated with the DDH on which the instance is created. For an instance that is enabled with the **No fees for stopped instances \(VPC-Connected\)** feature, if the original DDH does not have sufficient resources after the instance is restarted, the instance will be hosted on another DDH in the automatic DDH resource pool.
-   host: The instance is associated with the DDH on which the instance is created. An instance that is enabled with the **No fees for stopped instances \(VPC-Connected\)** feature is still hosted on the original DDH after it is restarted. If the original DDH does not have sufficient resources, the instance restart fails.

 Default value: default

 |
|DataDisk.N.PerformanceLevel|String|No|PL2| The performance level you select for an ESSD cloud disk that is used as a data disk. The value of N must be the same as that in `DataDisk.N.Category=cloud_essd`. Valid values:

 -   PL1 \(default value\): The maximum random read/write IOPS of a single disk is 50,000.
-   PL2: The maximum random read/write IOPS of a single disk is 100,000.
-   PL3: The maximum random read/write IOPS of a single disk is 1,000,000.

 For information about how to select a performance level for an ESSD cloud disk, see [ESSD cloud disk](~~122389~~).

 |
|SecurityGroupIds.N|RepeatList|No|sg-bp15ed6xe1yxeycg7o\*\*\*| The IDs of security groups to which an ECS instance belongs. You can add one ECS instance to multiple security groups. The value range of N depends on the maximum number of security groups that an ECS instance can be added to. For more information, see [Security group limits](../../../../intl.en-US/Product Introduction/Limits.md#section_mzr_52x_wdb).

 |
|SystemDisk.PerformanceLevel|String|No|PL1| The performance level you select for an ESSD cloud disk that is used as a system disk. Valid values:

 -   PL1 \(default value\): The maximum random read/write IOPS of a single disk is 50,000.
-   PL2: The maximum random read/write IOPS of a single disk is 100,000.
-   PL3: The maximum random read/write IOPS of a single disk is 1,000,000.

 For information about how to select a performance level for an ESSD cloud disk, see [ESSD cloud disk](~~122389~~).

 |
|Tenancy|String|No|default| Indicates whether to create an ECS instance on a DDH. Valid values:

 -   default: The ECS instance is not created on a DDH.
-   host: The ECS instance is created on a DDH. If you do not specify `DedicatedHostId`, Alibaba Cloud will automatically select a DDH for your instance.

 Default value: default

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|InstanceIdSets| |\["i-instanceid1", "i-instanceid2", "i-instanceid3"\]| The list of instance IDs \(`InstanceId`.

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The request ID.

 |

## Examples {#demo .section}

Sample request

``` {#request_demo}

https://ecs.aliyuncs.com/?Action=RunInstances
&RegionId=cn-hangzhou
&InstanceType=ecs.cm4.6xlarge
&SecurityGroupId=sg-securitygroupid
&Amount=3
&<Common request parameters>

```

Successful response examples

`XML` format

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

`JSON` format

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

## Errors {#section_pnx_d3f_kbh .section}

|HTTP status code|Error code|Error message|Meaning|
|----------------|----------|-------------|-------|
|404|InvalidSecurityGroupId|The specified SecurityGroupId is invalid or does not exist.|The error message returned when the specified security group ID does not exist.|
|400|InvalidInternetChargeType.ValueNotSupported|The specified InternetChargeType is not valid.|The error message returned when the specified instance configuration change type does not exist.|
|400|InvalidHostName.Malformed|The specified parameter "HostName" is not valid.|The error message returned when the format of the specified HostName is invalid.|
|403|InvalidParams.InstanceNameExceed|The uniqueSuffix takes three naming places, please shorten your InstanceName.|The error message returned when the instance name needs to be shortened, because uniqueSuffix occupies three namespaces.|
|403|InvalidParams.HostnameExceed|The uniqueSuffix takes three naming places, please shorten your Hostname.|The error message returned when the hostname needs to be shortened, because uniqueSuffix occupies three namespaces.|
|400|InvalidPasswordParam.Mismatch|The input password should be null when PasswdInherit is true.|The error message returned when no password can be configured if PasswdInherit is set to true.|
|400|InvalidSystemDiskCategory.ValueNotSupported|The specified parameter "SystemDisk.Category" is not valid.|The specified SystemDisk.Category is invalid.|
|400|InvalidDataDiskSize.ValueNotSupported|The specified DataDisk.N.Size beyond the permitted range, or the capacity of snapshot exceeds the size limit of the specified disk category.|The error message returned when the maximum size of the specified data disk is reached.|
|400|InvalidDataDiskCategory.ValueNotSupported|The specified parameter "DataDisk.N.Category" is not valid.|The error message returned when the specified DataDisk.N.Category is invalid.|
|400|InvalidSnapshotId.BasedSnapshotTooOld|The specified snapshot is created before 2013-07-15.|The error message returned when the specified snapshot was created on or before July 15, 2013.|
|403|InvalidSnapshotId.NotReady|The specified snapshot has not completed yet.|The error message returned when the specified snapshot has not been completed.|
|403|InvalidDevice.InUse|The specified device has been occupied.|The error message returned when the specified device has been attached to a disk.|
|403|ImageRemovedInMarket|The specified market image is not available, or the specified user defined image includes product code because it is based on an image subscribed from marketplace, and that image in marketplace including exact the same product code has been removed.|The error message returned when the specified marketplace image is unavailable.|
|404|InvalidClusterId.NotFound|The ClusterId provided does not exist in our records.|The error message returned when the specified ClusterId does not exist.|
|400|InvalidDiskDescription.Malformed|The specified parameter "SyatemDisk.DiskDescription or DataDisk.N.Description" is not valid.|The error message returned when the specified SyatemDisk.DiskDescription or DataDisk.N.Description is invalid.|
|403|RegionUnauthorized|There is no authority to create instance in the specified region.|The error message returned when you are not authorized to create instances in the specified region.|
|403|CategoryNotSupported|The specified Zone or cluster does not offer the specified disk category.|The error message returned when the specified disk category is unavailable in the specified zone or cluster.|
|403|CategoryNotSupported|The specified cluster does not offer the specified disk category.|The error message returned when the specified disk category is unavailable in the specified cluster.|
|404|InvalidVSwitchId.NotFound|Specified virtual switch does not exist.|The error message returned when the specified VSwitch does not exist.|
|400|InvalidParameter.Mismatch|Specified security group and virtual switch are not in the same VPC.|The error message returned when the specified security group is not in the same VPC as the VSwitch.|
|400|InvalidPrivateIpAddress|Specified private IP address is not in the CIDR block of virtual switch.|The error message returned when the specified private IP address is not in the same CIDR block as the VSwitch.|
|400|InvalidPrivateIpAddress.Malformed|Specified private IP address is malformed.|The error message returned when the specified private IP address is invalid.|
|400|IncorrectVSwitchStatus|The current status of virtual switch does not support this operation.|The error message returned when the specified VSwitch in the pending state and cannot be deleted.|
|400|InvalidParameter.Mismatch|Specified virtual switch is not in the specified zone.|The error message returned when the specified VSwitch does not exist in the specified zone.|
|400|MissingParameter|The input parameter "VSwitchId" that is mandatory for processing this request is not supplied.|The error message returned when the VSwitchId parameter is empty.|
|400|InvalidDiskCategory.Mismatch|The specified disk categories' combination is not supported.|The error message returned when the specified disk types are used together.|
|403|Forbbiden|User not authorized to operate on the specified resource.|The error message returned when you are not authorized to perform operations on the specified resource.|
|404|InvalidImageId.NotFound|The specified ImageId does not exist.|The error message returned when the specified image does not exist under this account. Check whether the image ID is correct.|
|403|InvalidDiskSize.TooSmall|Specified disk size is less than the size of snapshot|The error message returned when the specified disk has insufficient space for the snapshot.|
|404|InvalidInstanceChargeType.NotFound|The InstanceChargeType does not exist in our records|The error message returned when the specified instance configuration change type does not exist.|
|400|InvalidPeriod|The specified period is not valid.|The error message returned when the specified period is invalid.|
|400|InvalidDataDiskCategory.ValueNotSupported|The specified parameter " DataDisk.N.Category " is not valid.|The error message returned when the specified disk type is invalid.|
|400|InvalidSystemDiskCategory.ValueNotSupported|The specified parameter " SystemDisk.Category " is not valid.|The error message returned when the specified disk type is invalid.|
|403|InvalidDiskCategory.NotSupported|The specified disk category does not support the specified instance type.|The error message returned when the specified disk type is not supported in the instance type.|
|400|InstanceDiskCategoryLimitExceed|The specified DataDisk.N.Size beyond the permitted range, or the capacity of snapshot exceeds the size limit of the specified disk category.|The error message returned when the maximum size of the specified data disk is reached.|
|403|QuotaExceed.BuyImage|The specified image is from the image market? You have not bought it or your quota has been exceeded.|The error message returned when the specified image has not been purchased or its maximum quota is reached.|
|400|InvalidClientToken.ValueNotSupported|clienttoken is not valid.|The error message returned when the specified ClientToken is invalid.|
|400|InvalidHostName.Malformed|The specified parameter HostName is not valid.|The error message returned when the specified HostName is invalid.|
|400|InvalidInternetMaxBandwidthOut.Malformed|The specified parameter internetMaxBandwidthOut is not valid.|The error message returned when the specified InternetMaxBandwidthOut is invalid.|
|400|InvalidTagValue.Malformed|The specified Tag.N.Value is not valid.|The error message returned when the specified Tag.n.Value is invalid.|
|400|InvalidMinAmount.Malformed|The specified parameter MinAmount is not valid.|The error message returned when the specified MinAmount is invalid. Check whether it is correct.|
|400|InvalidMaxAmount.Malformed|The specified parameter MaxAmount is not valid.|The error message returned when the specified MaxAmount is invalid.|
|400|InvalidAutoReleaseTime.Malformed|The specified parameter AutoReleaseTime is not valid.|The error message returned when the specified AutoReleaseTime is invalid. The time follows the ISO 8601 standard and is in UTC time. The format is yyyy-MM-ddTHH:mm:ssZ.|
|400|InvalidPrivateIpAddress.Malformed|The specified parameter PrivateIpAddress is not valid.|The error message returned when the specified PrivateIpAddress is invalid.|
|404|InvalidSystemDiskSize.LessThanImageSize|The specified parameter SystemDisk.Size is less than the image size.|The error message returned when the specified SystemDisk.Size is less than the image size.|
|403|OperationDenied|The specified RegionId does not support the creation of the network type ECS instance.|The error message returned when the ECS instance of this network type cannot be created in the specified region. Check whether this network type is still available in the specified region.|
|400|OperationDenied.NoVlan|The specified parameter "VlanId" is not valid or vlan has not enough IP address.|The error message returned when the specified VLAN ID is invalid or no IP address is available in this VLAN.|
|403|OperationDenied.SnapshotNotValid|The specified snapshot is not allowed to create disk.|The error message returned when no disk can be created for the specified snapshot.|
|403|OperationDenied.NoStock|The resource is out of usage.|The error message returned when the instance is not in the running status. Enable the instance or check whether a proper operation is performed.|
|403|OperationDenied.SnapshotParamsNotValid|The capacity of snapshot exceeds the size limit of the specified disk category or the specified category is not authorized.|The error message returned when the maximum snapshot size is reached or you are not authorized to use the specified disk type.|
|403|OperationDenied.DiskTypeNotSupport|The type of the disk does not support the operation|The error message returned when the specified operation is invalid.|
|400|Account.Arrearage|Your account has been in arrears.|The error message returned when your account has insufficient balance. Charge your account and try it again.|
|403|InvalidUserData.Forbidden|User not authorized to input the parameter "UserData", please apply for permission "UserData"|The error message returned when you are not authorized to configure UserData.|
|400|InvalidUserData.NotSupported|The specified parameter "UserData" only support the vpc and IoOptimized Instance.|The error message returned when the specified UserData is only supported in VPC or optimized instances.|
|400|InvalidUserData.NotSupported|The specified parameter "UserData" only support the vpc and IoOptimized Instance.|The error message returned when the specified UserData is only supported in VPC or optimized instances.|
|404|InvalidZoneId.NotFound|The specified zoneId does not exist.|The error message returned when the specified zone ID does not exist.|
|403|Zone.NotOnSale|The resource in the specified zone is no longer available for sale. Please try other regions and zones.|The error message returned when no resources are available in the specified zone.|
|403|InvalidResourceType.NotSupported|This resource type is not supported. Please try other resource types.|The error message returned when the specified resource type is not supported.|
|403|InvalidInstanceType.ZoneNotSupported|The specified zone does not support this instancetype.|The error message returned when the specified instance type is not supported in the specified zone.|
|400|InstanceDiskNumber.LimitExceed|The total number of specified disk in an instance exceeds.|The error message returned when the maximum number of the specified disks in the instance is reached.|
|400|InvalidDiskCategory.ValueNotSupported|The specified parameter "DiskCategory" is not valid.|The error message returned when the specified DiskCategory is invalid.|
|400|InvalidParameter.Bandwidth|%s|The error message returned when the parameter is invalid.|
|400|InvalidDataDiskCategory.ValueNotSupported|%s|The error message returned when the parameter is invalid.|
|400|InvalidSystemDiskCategory.ValueNotSupported|%s|The error message returned when the parameter is invalid.|
|400|InvalidParameter.Conflict|%s|The error message returned when the parameter is in conflict with another parameter.|
|400|InvalidInternetChargeType.ValueNotSupported|%s|The error message returned when the parameter is invalid.|
|400|InvalidInstanceType.ValueNotSupported|%s|The error message returned when the specified instance type is invalid.|
|403|InstanceType.Offline|%s|The error message returned when the specified instance type is unavailable.|
|400|InvalidSystemDiskSize.ValueNotSupported|%s|The error message returned when the parameter is invalid.|
|400|InvalidDataDiskSize.ValueNotSupported|%s|The error message returned when the parameter is invalid.|
|404|InvalidKeyPairName.NotFound|The specified parameter "KeyPairName" does not exist in our records.|The error message returned when the specified KeyPairName does not exist.|
|403|DependencyViolation.WindowsInstance|The instance creating is window, cannot use ssh key pair to login.|The error message returned when SSH key pairs are not supported in Windows.|
|400|InvalidInstanceType.ValueNotSupported|The specified parameter "KeyPairName" only support IoOptimized Instance.|The error message returned when SSH key pairs are not supported in optimized instances.|
|403|InvalidNetworkType.MismatchRamRole|A RAM role can't be used for classic instance.|The error message returned when RAM roles are not supported in classic instances.|
|404|InvalidRamRole.NotFound|The specified parameter "RAMRoleName" does not exist.|The error message returned when the specified RAMRoleName does not exist.|
|404|InvalidLaunchTemplate.NotFound|%s|The error message returned when the specified template name is not found.|
|404|InvalidLaunchTemplateVersion.NotFound|%s|The error message returned when the specified template version is not found.|
|400|InvalidInstanceType.ElasticNetworkInterfaceNotSupported|The specified instance type does not support Elastic Network Interface, you cannot attach Elastic Network Interface to generation I instances.|The error message returned when ENIs are not supported in the specified instance type.|
|400|InvalidParameter.EncryptedIllegal|%s|The error message returned when the parameter is invalid.|
|400|InvalidParameter.EncryptedNotSupported|%s|The error message returned when the parameter is invalid.|
|400|InvalidParameter.Encrypted.KmsNotEnabled|The encrypted disk need enable KMS|The error message returned when the KMS is not enabled for encrypted disks.|
|500|InternalError|The request processing has failed due to some unknown error, exception or failure.|The error message returned when an unknown error occurs.|
|403|Forbidden.RiskControl|This operation is forbidden by Aliyun RiskControl system.|The error message returned when the operation is forbidden by the risk control system.|
|403|InvalidInstance.UnPaidOrder|The specified Instance has unpaid order.|The error message returned when you have unpaid orders under the specified instance.|
|403|RealNameAuthenticationError|Your account has not passed the real-name authentication yet.|The error message returned when you failed the real-name authentication.|
|403|InvalidAccountStatus.NotEnoughBalance|Your account does not have enough balance.|The error message returned when your account has insufficient balance.|
|400|InvalidSpotPriceLimit.LowerThanPublicPrice|The specified parameter "spotPriceLimit" can't be lower than current public price.|The error message returned when the specified spotPriceLimit is lower than the current open market price.|
|400|InvalidRelationResource.NotFound|The relation resource has been deleted.|The error message returned when the related resource is deleted.|
|400|IncorrectRecycleBinStatus|The operation is not permitted due to resource status.|The error message returned when the operation is not supported while the resource is in the current state.|
|400|InvalidHpcClusterId.Unnecessary|The specified HpcClusterId is unnecessary|The error message returned when the specified HpcClusterId is not required.|
|400|InvalidVSwitchId.Necessary|The VSwitchId is necessary|The error message returned when a required parameter is not specified.|
|400|InvalidHpcClusterId.Necessary|The HpcClusterId is necessary|The error message returned when a required parameter is not specified.|
|400|InvalidHpcClusterId.NotFound|The specified HpcClusterId is not found|The error message returned when the specified HPC cluster does not exist.|
|400|InvalidHpcClusterId.Creating|The specified HpcClusterId is creating|The error message returned when the specified HPC cluster is being created.|
|404|InvalidVSwitchId.NotExist|%s|The error message returned when the specified VSwitch does not exist.|
|403|ImageNotSupportInstanceType|The specified image does not support the specified InstanceType.|The error message returned when the specified instance type is not supported in the specified image.|
|400|InvalidSecurityGroup.NotInDefaultVpc|%s|The error message returned when the specified security group is not in the default VPC.|
|400|InvalidSpotInterruptionBehavior|%s|The error message returned when SpotInterruptionBehavior is not supported.|
|403|InvalidSpotInterruptionBehavior.ClassicNetworkNotSupport|The specified SpotInterruptionBehavior does not support Classic network Instance.|The error message returned when the preemptible instance is a classic instance.|
|403|InvalidSpotInterruptionBehavior.LocalDiskNotSupport|The specified SpotInterruptionBehavior does not support local disk instance.|The error message returned when you try to use preemptible instances with local disks.|
|400|InvalidDeploymentOnHost|%s|The error message returned when DDHs are not supported in the specified deployment set.|
|400|InvalidInstanceChargeType.NotSupport|The Dedicated host not support the specified Instance charge type.|The error message returned when the billing method is not supported in DDHs.|
|400|InvalidNetworkType.NotSupported|The classic networkType not support create ECS on dedicatedHost|The error message returned when you try to use classic network with DDHs.|
|400|InvalidDedicatedHostId.NotFound|The specified DedicatedHostId does not exist.|The error message returned when the specified DDH ID does not exist.|
|400|InvalidDedicatedHostStatus.NotSupport|Operation denied due to dedicated host status.|The error message returned when the operation is not supported while the resource is in the current state.|
|400|IncorrectDedicatedHostStatus|The current status of the resource does not support this operation.|The error message returned when the operation is not supported while the resource is in the current state.|
|400|ChargeTypeViolation.PostPaidDedicatedHost|Prepaid instance onto postpaid dedicated host is not allowed|The error message returned when the billing method is changed for DDHs.|
|400|InvalidPeriod.ExceededDedicatedHost|Instance expired date can't exceed dedicated host expired date.|The error message returned when the expiration date of the instance is later than that of the DDH.|
|400|InvalidInstanceType.ValueUnauthorized|The specified InstanceType is not authorize.|The error message returned when you are not authorized to use this instance type.|
|400|DedicatedHostType.Unmatched|The specified DedicatedHostType doesn't match the instance type.|The error message returned when preemptible instances do not support the instance type.|
|400|LackResource|There's no enough resource on the specified dedicated host.|The error message returned when the DDH has insufficient resources.|
|400|MissingParameter|The input parameter ImageId that is mandatory for processing this request is not supplied.|The error message returned when a required parameter is not specified.|
|400|MissingParameter|The input parameter InstanceType that is mandatory for processing this request is not supplied.|The error message returned when a required parameter is not specified.|
|400|ChargeTypeViolation.PostPaidDedicatedHost|Prepaid instance onto postpaid dedicated host is not allowed.|The error message returned when the billing method is changed for DDHs.|
|400|InvalidParam.NetworkInterface|%s|The error message returned when the specified parameter is invalid.|
|401|InvalidRamRole.NotEcsRole|The specified ram role is not authorized for ecs, please check your role policy.|The error message returned when the specified RAM role is not authorized to access ECS.|
|403|InvalidParameter.NotMatch|%s|The error message returned when the parameter is in conflict with another parameter.|
|403|InvalidVSwitch.DefaultVSwitchNotSupport|The specified zone in vpc can't support create default vSwitch.|The error message returned when the default VSwitch is not supported in VPCs of the specified zone.|
|400|InvalidParameter.CreditSpecification|The specified CreditSpecification is not supported in this region.|The error message returned when the specified CreditSpecification is not supported in this region.|
|404|InvalidMarketImage.NotFound|The specified marketplace image does not exist, please change the imageId and try again.|The error message returned when the specified image is not available on the Alibaba Cloud market.|
|400|InvalidInstanceType.NotSupported|The specified instanceType is not supported by the deployment set.|The error message returned when the instance type is not supported in the specified deployment set.|
|400|InvalidVpcZone.NotSupported|The specified operation is not allowed in the zone to which your VPC belongs, please try in other zones.|The error message returned when the operation is not supported in the specified zone.|
|400|IncorrectDefaultVpcStatus|The status of the default VPC is invalid.|The error message returned when the status of the default VPC is incorrect.|
|404|DeploymentSet.NotFound|The specified deployment set does not exist.|The error message returned when the specified deployment set does not exist.|
|400|InvalidAutoRenewPeriod.ValueNotSupported|The specified autoRenewPeriod is invalid.|The error message returned when the specified autoRenewPeriod is invalid.|
|403|DefaultVswitch.Existed|The default vswitch for VPC already exists.|The error message returned when the default VSwtich has been created for the VPC.|
|400|InvalidMarketImageChargeType.NotSupport|The specified chargeType of marketImage is unsupported.|The error message returned when the billing method for marketplace images is invalid.|
|403|IncorrectInstanceStatus|The current status of the resource does not support this operation.|The error message returned when the operation is not supported while the resource is in the current state.|
|403|CategoryViolation|The specified instance does not support this operation because of its disk category.|The error message returned when configurations are changed for instances with local disks attached.|
|400|InvalidPeriodType.ValueNotSupported|The specified parameter PeriodType is invalid.|The error message returned when the specified PeriodType is invalid.|
|403|InvalidDisk.SystemDiskSize|The specified SystemDiskSize beyond the permitted range.|The error message returned when the maximum size of the specified system disk is reached.|
|400|IncorrectImageStatus|The specified marketplace image is not available.|The error message returned when the specified marketplace image is unavailable.|
|403|MaxEniIpv6IpsCountExceeded|%s|The error message returned when the maximum number of IPv6 addresses that can be allocated to the ENI is reached.|
|403|InvalidIp.IpRepeated|%s|The error message returned when the IP address is specified repeatedly.|
|403|InvalidIp.IpAssigned|%s|The error message returned when the specified IP address has been allocated.|
|403|InvalidIp.Address|%s|The error message returned when the specified IP address is invalid.|
|403|InvalidOperation.Ipv4CountExceeded|%s|The error message returned when the maximum number of IPv4 addresses is reached.|
|403|InvalidOperation.Ipv6CountExceeded|%s|The error message returned when the maximum number of IPv6 addresses is reached.|
|403|InvalidOperation.Ipv6NotSupport|%s|The error message returned when IPv6 addresses are not supported by the instance type.|
|403|InvalidVSwitch.Ipv6NotTurnOn|%s|The error message returned when the IPv6 feature is not enabled on the VSwitch.|
|403|InvalidParam.Amount|%s|The error message returned when the specified Amount is invalid.|
|403|InvalidVSwitchId.IpInvalid|%s|The error message returned when the specified private IP address is invalid.|
|403|Forbidden.RegionId|%s|The error message returned when the feature is not supported in the specified region.|
|400|IncorrectVpcStatus|The current status of vpc does not support this operation.|The error message returned when the operation is not supported while the VPC is in the current state.|
|403|InvalidChargeType.ValueNotSupported|The operation is not permitted due to deletion protection only support postPaid instance|The error message returned when release protection is not supported.|
|403|InvalidRegion.NotSupport|The specified region does not support byok.|The error message returned when BYOK is not supported in the specified region.|
|403|UserNotInTheWhiteList|The user is not in byok white list.|The error message returned when you use BYOK.|
|400|InvalidParameter.EncryptedIllegal|The specified parameter Encrypted must be true when kmsKeyId is not empty.|The error message returned when the Encrypted feature is not enabled after you set KmsKeyId.|
|400|IoOptimized.NotSupported|The specified instance must be IoOptimized instance when kmsKeyId is not empty.|The error message returned when optimized instances are not used after you set KmsKeyId.|
|404|InvalidParameter.KMSKeyId.NotFound|The specified KMSKeyId does not exist.|The error message returned when the specified KMSKeyId is invalid.|
|403|InvalidParameter.KMSKeyId.KMSUnauthorized|ECS service have no right to access your KMS.|The error message returned when ECS is not authorized to access your KMS.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

