# CreateInstance {#doc_api_1161576 .reference}

Creates an ECS instance.

## Description {#description .section}

**Note:** Before creating an instance, you can call the [DescribeAvailableResource](~~66186~~) action to view the available resources in the specified region or zone. If you want to create multiple instances that automatically enter the running state, we recommend that you call the [RunInstances](~~63440~~) action.

You must fully understand the ECS billing methods before you create an instance, because resource billing is involved when creating instances. For more information, see [Billing overview](~~25398~~). If the billing method is set to `PrePaid`, coupons available under your account will be used.

When you call this action, note that:

For **instance types**:

-   You can use the `IoOptimized` parameter to indicate whether to create an optimized instance.
-   For an `ephemeral_ssd` instance, the instance type cannot be changed after it is created.

For **images**:

When creating an instance, you must select an image to determine the system disk configuration of the new instance. After an instance is created, its system disk is a clone of that image.

-   If the instance memory is 512 MiB, you can only use the Windows Server 1709 image.
-   If the instance memory is 4 GiB or more, the 32-bit OS image cannot be used.

For **network configuration**:

-   To create a VPC-type instance, you must specify the VPC network and a VSwitch. One instance can only belong to one VSwitch.
-   When you specify `VSwitchId`, `SecurityGroupId` must be in the same VPC as `VSwitchId`.
-   ``If you specify both and `PrivateIpAddress`, `PrivateIpAddress` must be in the same CIDR block as the VSwitch.
-   `` depends on `VSwitchId`, so you cannot specify only `PrivateIpAddress`.
-   When you call this action to create an instance, no public IP address is allocated to the instance. You can call the [AllocatePublicIpAddress](~~25544~~) action to allocate a public IP address to the instance.
-   You can use the `InternetChargeType` and `InternetMaxBandwidthOut` parameters to limit the bandwidth fees.`InternetMaxBandwidthIn` is not related to bandwidth billing, because the inbound data traffic for the instance is free.
-   The relationship between `InternetChargeType` and `InternetMaxBandwidthOut` is as follows:
    -   `` indicates that the instance is charged based on a fixed bandwidth, so `InternetMaxBandwidthOut` is the selected bandwidth value.
    -   `` indicates that the instance is charged based on actual traffic, so `InternetMaxBandwidthOut` is the upper limit of the specified bandwidth. The Pay-As-You-Go billing method is used.

For **security groups**:

-   You can call the [CreateSecurityGroup](~~25553~~) action to create a security group in advance.
-   You can also specify a security group when creating an instance or call the [ModifyInstanceAttribute](~~25503~~) action to change the security group of the instance.
-   Instances that belong to the same security group can access each other, but not instances that belong to different security groups. However, you can configure firewall permissions by using the security group authorization to allow instances in different security groups to access each other. For more information, see [AuthorizeSecurityGroup](~~25554~~) and [AuthorizeSecurityGroupEgress](~~25560~~).
-   One security group can contain a maximum of 1,000 instances.

For **storage**:

-   The maximum capacity of data disks varies based on disk categories:
    -   The maximum capacity of a single basic disk \(`cloud`\) is 2,000 GiB.
    -   The maximum capacity of a single ultra disk \(`cloud_efficiency`\) is 32 TiB \(32,768 GiB\).
    -   The maximum capacity of a single SSD \(`cloud_ssd`\) is 32 TiB \(32,768 GiB\).
    -   The maximum capacity of a single ESSD \(`cloud_essd`\) is 32 TiB \(32,768 GiB\).
    -   The maximum capacity of a single local SSD \(`ephemeral_ssd`\) is 800 GiB.
-   ECS allocates a system disk of an appropriate size for the instance that you create. The system disk capacity must be equal to or greater than max \{20, ImageSize \}. The system disk can be a basic disk \(`cloud`\), ultra disk \(`cloud_efficiency`\), SSD \(`cloud_ssd`\), or local SSD \(`ephemeral_ssd`\).
-   When the system disk is a basic disk \(`cloud`\), ultra disk \(`cloud_efficiency`\), or SSD \(`cloud_ssd`\), the data disk cannot be a local SSD \(`ephemeral_ssd`\).
-   When you select an optimized instance, the system disk can only be an ultra disk \(`cloud_efficiency`\) or SSD \(`cloud_ssd`\).
-   A maximum of 16 data disks can be attached to an instance. The mount points of data disks are allocated by the system in the default order, from /dev/xvdb to /dev/xvdz. If a local SSD \(`ephemeral_ssd`\) is used as the data disk, the system disk must be a local SSD. The total capacity of local SSDs for an instance cannot exceed 1 TiB \(1,024 GiB, excluding the system disk\).
-   The local SSD `ephemeral_ssd` must be specified when you create an instance. It cannot be added after the instance is created. For more information, see [Instance type families](~~25378~~).

For **user data**:

If the instance meets the requirements for [user data](~~49121~~), you can import UserData information. User data is encoded in Base64. We recommend that you do not import confidential information, such as passwords and keys, because user data is imported in plain-text mode. If you need to transfer confidential information, we recommend that you encrypt it and encode it in Base64 before importing it and decrypt it in the instance.

For **others**:

When you call this action in the Alibaba Cloud CLI and SDK, first delete the period \(.\) from the following parameters: `SystemDisk.Category`, `SystemDisk.Size`, `SystemDisk.Description`, `DataDisk.N.Size`, `DataDisk.N.Category`, `DataDisk.N.SnapshotId`, `DataDisk.N.DiskName`, `DataDisk.N.Description`, `DataDisk.N.DeleteWithInstance`, and `DataDisk.N.PerformanceLevel`.

For example, in the [Alibaba Cloud CLI](~~66653~~) and [SDK](https://github.com/aliyun), `Systemdiskcategory` is used to represent `SystemDisk.Category`.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=CreateInstance) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|ImageId|String|Yes|win2008r2\_64\_ent\_sp1\_en-us\_40G\_alibase\_20170915.vhd| The ID of the image file that you specified when you create the instance. For more information about marketplace images, see `ImageId` on the Product Details page at Alibaba Cloud Marketplace.

 |
|InstanceType|String|Yes|ecs.g5.large| The type of the instance. For more information, see [Instance type families](~~25378~~), or call the [DescribeInstanceTypes](~~25620~~) action to obtain the latest instance type list.

 |
|RegionId|String|Yes|cn-hangzhou| The region ID of the instance. You can call the [DescribeRegions](~~25609~~) action to view the latest region list.

 |
|Action|String|No|CreateInstance| The operation that you want to perform. Set the value to CreateInstance.

 |
|AutoRenew|Boolean|No|true| Indicates whether to enable automatic renewal. The parameter is valid only when `InstanceChargeType` is set to `PrePaid`. Valid values:

 -   true
-   false

 |
|AutoRenewPeriod|Integer|No|2| The automatic renewal period of the instance. This parameter is required when AutoRenew is set to true. Valid values:

 \{“1”, “2”, “3”, “6”, “12”\} if PeriodUnit is set to Month.

 |
|ClientToken|String|No|123e4567-e89b-12d3-a456-426655440000| The token used to ensure idempotence. You can generate the token in your client, but you must ensure that it is globally unique.**ClientToken** can contain only ASCII characters. It must be no more than 64 characters in length. For more information, see [How to ensure idempotence](~~25693~~).

 |
|ClusterId|String|No|c-clusterid1| The ID of the cluster to which the instance belongs.

 **Note:** This parameter will be removed in the future. We recommend that you use other parameters to ensure compatibility.

 |
|CreditSpecification|String|No|Standard| The running mode of the burstable performance instance \(t5\). Valid values:

 -   Standard: the standard mode. For more information, see [Standard t5 instances](~~90635~~).
-   Unlimited: the unlimited performance mode. For more information, see [Unlimited-performance t5 instances](~~90581~~).

 Default value: null.

 |
|DataDisk.N.Category|String|No|cloud-ssd| The category of the nth data disk. Default value: cloud. Valid values:

 -   cloud: basic disk.
-   cloud\_efficiency: ultra disk.
-   cloud\_ssd: SSD.
-   ephemeral\_ssd: local SSD.
-   cloud\_essd: ESSD. ESSDs are still in the public beta test phase and only available in some regions. For more information, see [ESSD FAQ](~~64950#AvailableRegion~~).

 |
|DataDisk.N.DeleteWithInstance|Boolean|No|true| Indicates whether the data disk is released along with the instance. Default value: true.

 |
|DataDisk.N.Description|String|No|DataDiskFinance| The description of the data disk. It must be 2 to 256 characters in length. It cannot start with http:// or https://. Default value: null.

 |
|DataDisk.N.Device|String|No|/dev/xvda| The mount point of the nth data disk.

 |
|DataDisk.N.DiskName|String|No|DataDisk| The name of the nth data disk. It must be 2 to 128 characters in length and can contain uppercase and lowercase letters, digits, colons \(:\), underscores \(\_\), and hyphens \(-\). It must start with a letter. It cannot start with http:// or https://. Default value: null.

 |
|DataDisk.N.Encrypted|Boolean|No|false| Indicates whether the nth data disk is encrypted. Default value: false.

 |
|DataDisk.N.Size|Integer|No|2,000| The size of the nth data disk. n ranges from 1 to 16. Unit: GiB. Valid values:

 -   cloud: 5 to 2,000.
-   cloud\_efficiency: 20 to 32,768.
-   cloud\_ssd: 20 to 32,768.
-   cloud\_essd: 20 to 32,768.
-   ephemeral\_ssd: 5 to 800.

 This value must be equal to or greater than the size of `SnapshotId`.

 |
|DataDisk.N.SnapshotId|String|No|s-bp17441ohwka0yuhx3h0| The ID of the snapshot used to create the nth data disk. n ranges from 1 to 16. When `DataDisk.N.SnapshotId` is specified, the value of `DataDisk.N.Size` is ignored. The size of the new data disk is equal to that of the specified snapshot. Snapshots created on or before July 15, 2013 cannot be used here. Otherwise, an error will be returned and your request will be rejected.

 |
|DedicatedHostId|String|No|dh-dedicatedhost1| Indicates whether to create an ECS instance on the specified Dedicated Host \(DDH\). You can call the [DescribeDedicatedHosts](~~94572~~) action to view the DDH list.

 No preemptible instances can be created on the DDH. Therefore, if you specify `DedicatedHostId`, the values of `SpotStrategy` and `SpotPriceLimit` will be ignored.

 |
|DeletionProtection|Boolean|No|false| The release protection attribute of the instance. It indicates whether you can use the ECS console or call the [DeleteInstance](~~25507~~) action to release the instance. Default value: false. Valid values:

 -   true: enables release protection.
-   false: disables release protection.

 **Note:** This attribute is applicable to Pay-As-You-Go instances. It can only be used to block manual release operations, but not automatic release operations by the system.

 |
|SystemDisk.PerformanceLevel|String|No|PL1| The performance level you select for an ESSD cloud disk that is used as a system disk. Valid values:

 -   PL1 \(default value\): The maximum random read/write IOPS of a single disk is 50,000.
-   PL2: The maximum random read/write IOPS of a single disk is 100,000.
-   PL3: The maximum random read/write IOPS of a single disk is 1,000,000.

 For information about how to select a performance level for an ESSD cloud disk, see [ESSD cloud disk](~~122389~~).

 |
|DataDisk.N.PerformanceLevel|String|No|PL2| The performance level you select for an ESSD cloud disk that is used as a data disk. The value of N must be the same as that in `DataDisk.N.Category=cloud_essd`. Valid values:

 -   PL1 \(default value\): The maximum random read/write IOPS of a single disk is 50,000.
-   PL2: The maximum random read/write IOPS of a single disk is 100,000.
-   PL3: The maximum random read/write IOPS of a single disk is 1,000,000.

 For information about how to select a performance level for an ESSD cloud disk, see [ESSD cloud disk](~~122389~~).

 |
|Affinity|String|No|default| Indicates whether to associate an ECS instance with the DDH on which the instance is created. Valid values:

 -   default: The instance is not associated with the DDH on which the instance is created. For an instance that is enabled with the **No fees for stopped instances \(VPC-Connected\)** feature, if the original DDH does not have sufficient resources after the instance is restarted, the instance will be hosted on another DDH in the automatic DDH resource pool.
-   host: The instance is associated with the DDH on which the instance is created. An instance that is enabled with the **No fees for stopped instances \(VPC-Connected\)** feature is still hosted on the original DDH after it is restarted. If the original DDH does not have sufficient resources, the instance restart fails

 Default value: default

 |
|Tenancy|String|No|default| Indicates whether to create an ECS instance on a DDH. Valid values:

 -   default: The ECS instance is not created on a DDH.
-   host: The ECS instance is created on a DDH. If you do not specify `DedicatedHostId`, Alibaba Cloud will automatically select a DDH for your instance.

 Default value: default

 |
|DeploymentSetId|String|No|ds-bp1brhwhoqinyjd6tn3x| The ID of the deployment set.

 |
|Description|String|No|InstanceFinance| The description of the instance. It must be 2 to 256 characters in length. It cannot start with http:// or https://. Default value: null.

 |
|DryRun|Boolean|No|false| Indicates whether to send a check request only. Default value: false.

 -   true: Only a check request is sent and no instance is created. The system checks whether the required parameters are set, and verifies the request format, service limits, and available ECS instances. If the check fails, the corresponding error code is returned. If the check succeeds, the `DryRunOperation` error code is returned.
-   false: A request is sent and then the instance is created.

 |
|HostName|String|No|LocalHost| The hostname of the instance.

 -   It cannot start or end with a period \(.\) or a hyphen \(-\) It cannot contain consecutive periods \(.\) or hyphens \(-\).
-   For Windows: The hostname must be 2 to 15 characters in length and can contain uppercase and lowercase letters, digits, and hyphens \(-\). It cannot contain periods \(.\) or contain only digits.
-   For other operating systems: The hostname must be 2 to 64 characters in length and can contain uppercase and lowercase letters, digits, and hyphens \(-\). It can be separated by periods \(.\).

 |
|HpcClusterId|String|No|hpc-hpcclusterid| The ID of the HPC cluster to which the instance belongs.

 |
|InnerIpAddress|String|No|XX.XXX.XX.XXX| The private IP address of the instance.

 |
|InstanceChargeType|String|No|PrePaid| The billing method of the instance. Default value: PostPaid. Valid values:

 -   PrePaid: subscription. If it is set to PrePaid, you must confirm that your payment account has sufficient balance or credit. Otherwise, the `InvalidPayMethod` error code is returned.
-   PostPaid: Pay-As-You-Go.

 |
|InstanceName|String|No|yk201812061032| The name of the instance. It must be 2 to 128 characters in length and can contain uppercase and lowercase letters, digits, colons \(:\), underscores \(\_\), and hyphens \(-\). It must start with a letter. It cannot start with http:// or https://. If this parameter is not specified, InstanceId is used by default.

 |
|InternetChargeType|String|No|PayByTraffic| The billing method of the instance. Default value: PayByTraffic. Valid values:

 -   PayByTraffic: charged based on actual traffic.

 |
|InternetMaxBandwidthIn|Integer|No|200| The maximum inbound bandwidth for the public network. Unit: Mbit/s. Valid values: 1 to 200.

 Default value: 200

 |
|InternetMaxBandwidthOut|Integer|No|5| The maximum outbound bandwidth for the public network. Unit: Mbit/s. Valid values: 0 to 100.

 Default value: 0

 |
|IoOptimized|String|No|optimized| Specifies whether the instance is an I/O optimized instance. The default value for [phased-out instance types](~~55263~~) is none, but that for other instances is optimized. Valid values:

 -   none.
-   optimized.

 |
|KeyPairName|String|No|Instancetest| The name of the key pair.

 -   For Windows instances, ignore this parameter. Default value: null. Even if this parameter is specified, the `Password` value is used.
-   For Linux instances, the password logon method is forbidden during initialization. To improve instance security, we recommend that you use the key pair connection method.

 |
|NodeControllerId|String|No|nc-nodecontroller| This parameter has been discarded.

 |
|OwnerAccount|String|No|ECSforCloud@Alibaba.com| The logon name of the RAM user.

 |
|Password|String|No|EcsV587!| The password of the instance. It must be 8 to 30 characters in length and can contain uppercase and lowercase letters, digits, and special characters. The following special characters can be used:

 ``` {#codeblock_i6a_wkf_qdo}

Parentheses (()), grave accents (`), tildes (~), exclamation points (!), at signs (@), number signs (#), dollar signs ($), percent signs (%), carets (^), ampersands (&), asterisks (*), hyphens (-), underscores (_), plus signs (+), equal signs (=), vertical bars (|), braces ({}), brackets ([]), colons (:), semicolons (;), acute accents (′), angle brackets (<>), commas (,), periods (.), question marks (?), and forward slashes (/).

```

 For Windows, the password cannot start with a forward slash \(/\).

 **Note:** If `Password` is specified, we recommend that you send requests over the HTTPS protocol to keep the password confidential. To improve instance security, we recommend that you use the key pair connection method.

 |
|PasswordInherit|Boolean|No|false| Indicates whether to use the password predefined in the image. If PasswordInherit is specified, Password must be null. Make sure that the selected image has a password configured.

 |
|Period|Integer|No|1| The subscription period of the instance. Unit: month. The parameter is valid and required only when `InstanceChargeType` is set to `PrePaid`. If DedicatedHostId is specified, the value range of the Period parameter must be within the subscription period of the DDH. Valid values:

 \{ “1”, “2”, “3”, “4”, “5”, “6”, “7”, “8”, “9”, “12”, “24”, “36”,”48”,”60”\} if PeriodUnit is set to Month.

 |
|PeriodUnit|String|No|Month| The unit of the subscription period. Default value: Month. Valid values: Week and Month.

 |
|PrivateIpAddress|String|No|172.16.236.14X| The private IP address of the instance. PrivateIpAddress depends on VSwitchId and cannot be specified separately.

 |
|RamRoleName|String|No|FinanceDept| The RAM role name of the instance. You can call the [ListRoles](~~28713~~) action to view RAM roles for the specified instance.

 |
|ResourceGroupId|String|No|rg-resourcegroupid| The ID of the resource group to which the instance belongs.

 |
|SecurityEnhancementStrategy|String|No|Active| Indicates whether to enable security hardening. Valid values:

 -   Active: enables security hardening. It is applicable only to the system image.
-   Deactive: disables security hardening. It is applicable to all images.

 |
|SecurityGroupId|String|No|sg-bp15ed6xe1yxeycg7ov3| The ID of the security group to which the instance belongs. Instances in the same security group can access each other.

 |
|SpotInterruptionBehavior|String|No|Terminate| The interruption mode of the preemptible instance. Only the Terminate mode is supported, in which the instance is released.

 |
|SpotPriceLimit|Float|No|0.98| The maximum hourly price for the instance. It is precise up to three decimal places. It is valid only when `SpotStrategy` is set to `SpotWithPriceLimit`.

 |
|SpotStrategy|String|No|NoSpot| The preemption policy of the Pay-As-You-Go instance. The parameter is valid only when `InstanceChargeType` is set to `PostPaid`. Default value: NoSpot. Valid values:

 -   NoSpot: a standard Pay-As-You-Go instance.
-   SpotWithPriceLimit: a preemptible instance with the upper price limit defined.
-   SpotAsPriceGo: a Pay-As-You-Go instance with its price based on the current market price.

 |
|SystemDisk.Category|String|No|cloud-ssd| The category of the system disk. The default value of the non-optimized instance for [phased-out instance types](~~55263~~) is cloud. The default value for other instances is cloud\_efficiency. Valid values:

 -   cloud: basic disk.
-   cloud\_efficiency: ultra disk.
-   cloud\_ssd: SSD.
-   ephemeral\_ssd: local SSD.
-   cloud\_essd: ESSD. ESSD cloud disks are still in the public beta test phase and only available in some regions. For more information, see [ESSD FAQ](~~64950#AvailableRegion~~).

 |
|SystemDisk.Description|String|No|SystemDiskFinance| The description of the system disk. It must be 2 to 256 characters in length. It cannot start with http:// or https://. Default value: null.

 |
|SystemDisk.DiskName|String|No|SystemDisk| The name of the system disk. It must be 2 to 128 characters in length and can contain uppercase and lowercase letters, digits, colons \(:\), underscores \(\_\), and hyphens \(-\). It must start with a letter. It cannot start with http:// or https://. Default value: null.

 |
|SystemDisk.Size|Integer|No|40| The size of the system disk. Unit: GiB. Valid values: 20 to 500. This value must be equal to or greater than max \{20, ImageSize\}. Default value: max \{40, ImageSize\}.

 |
|Tag.N.Key|String|No|FinanceDept| The tag key of the instance, disk, and primary NIC. n ranges from 1 to 20. If you specify this parameter, it cannot be left empty. It must be no more than 64 characters in length. It cannot start with aliyun, acs:, http://, or https://.

 |
|Tag.N.Value|String|No|FinanceDeptJoshua| The tag value of the instance, disk, and primary NIC. n ranges from 1 to 20. If you specify this parameter, it can be left empty. It must be no more than 128 characters in length. It cannot start with aliyun, acs:, http://, or https://.

 |
|Tag.N.key|String|No|FinanceDept| The tag key of the instance, disk, and primary NIC.

 **Note:** This parameter will be removed in the future. We recommend that you use Tag.N.Key to ensure compatibility.

 |
|Tag.N.value|String|No|FinanceDeptJoshua| The tag value of the instance, disk, and primary NIC.

 **Note:** This parameter will be removed in the future. We recommend that you use Tag.N.Value to ensure compatibility.

 |
|UseAdditionalService|Boolean|No|true| Indicates whether to use the virtual machine system configuration provided by Alibaba Cloud \(Windows: NTP and KMS. Linux: NTP and YUM\).

 |
|UserData|String|No|ZWNobyBoZWxsbyBlY3Mh| The user data of the instance. It must be encoded in Base64. The maximum size of the user data is 16 KB.

 |
|VSwitchId|String|No|vsw-bp1s5fnvk4gn2tws03ziX| The ID of the VSwitch. It must be specified when you create VPC-type instances.

 |
|VlanId|String|No|10| The VLAN ID of the instance.

 |
|ZoneId|String|No|cn-hangzhou-b| The zone ID of the instance. For more information, see [DescribeZones](~~25610~~).

 Default value: null. If you do not specify a zone, the system randomly selects a zone.

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|InstanceId|String|i-instance1| The ID of the instance. It is a unique identifier of the instance.

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The request ID. The system returns a unique RequestId for each API request, regardless of whether the API action is successful.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

https://ecs.aliyuncs.com/?Action=CreateInstance
&RegionId=cn-hangzhou 
&ImageId=_32_23c472_20120822172155_aliguest.vhd 
&SecurityGroupId=sg-c0003e8b9 
&HostName=Bctest01 
&InstanceType=ecs.t1.small
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<CreateInstanceResponse> 
  <RequestId>04F0F334-1335-436C-A1D7-6C044FE73368</RequestId> 
  <InstanceId>i-instance1</InstanceId>
</CreateInstanceResponse> 

```

`JSON` format

``` {#json_return_success_demo}
{
	"InstanceId":"i-instance1",
	"RequestId":"04F0F334-1335-436C-A1D7-6C044FE73368"
}
```

## Errors {#section_hz0_mmq_l2u .section}

|HTTP status code|Error code|Error message|Meaning|
|----------------|----------|-------------|-------|
|400|InvalidInternetChargeType.ValueNotSupported|The specified InternetChargeType is not valid.|The error message returned when the specified instance type does not exist.|
|400|InvalidSystemDiskCategory.ValueNotSupported|The specified parameter " SystemDisk.Category" is not valid.|The error message returned when the specified disk type is invalid.|
|400|InvalidDataDiskSize.ValueNotSupported|The specified DataDisk.N.Size beyond the permitted range, or the capacity of snapshot exceeds the size limit of the specified disk category.|The error message returned when the maximum size of the specified data disk is reached.|
|403|InvalidDiskCategory.NotSupported|The specified disk category is not support the specified instance type.|The error message returned when the specified disk type is not supported in the instance type.|
|400|InvalidInstanceType.ValueNotSupported|The specified InstanceType does not exist or beyond the permitted range.|The error message returned when the specified instance type is not supported.|
|404|InvalidSecurityGroupId.NotFound|The specified SecurityGroupId does not exist.|The error message returned when the specified SecurityGroupId does not exist under this account. Check whether the SecurityGroupId is correct.|
|400|InvalidHostName.Malformed|The specified parameter "HostName" is not valid.|The error message returned when the format of the specified HostName is invalid.|
|400|InvalidPasswordParam.Mismatch|The input password should be null when passwdInherit is true.|The error message returned when no password can be configured if PasswordInherit is set to true.|
|400|InvalidSystemDiskCategory.ValueNotSupported|The specified parameter "SystemDisk.Category" is not valid.|The error message returned when the specified SystemDisk.Category is invalid.|
|400|InvalidDiskDescription.Malformed|The specified parameter "SystemDisk.DiskDescription" or "DataDisk.N.Description" is not valid.|The error message returned when the specified SyatemDisk.DiskDescription or DataDisk.N.Description is invalid.|
|400|InvalidDataDiskCategory.ValueNotSupported|The specified parameter "DataDisk.N.Category" is not valid.|The error message returned when the specified DataDisk.N.Category is invalid.|
|400|OperationDenied|The specified parameter "VlanId" is not valid or vlan has not enough IP address.|The error message returned when the specified VLAN ID is invalid or no more IP addresses are available in this VLAN.|
|400|InvalidSnapshotId.BasedSnapshotTooOld|The specified snapshot is created before 2013-07-15.|The error message returned when the specified snapshot was created on or before July 15, 2013.|
|400|InvalidMarketImageChargeType.NotSupport|The specified chargeType of marketImage is unsupported.|The error message returned when the billing method for marketplace images is invalid.|
|403|OperationDenied|The specified Image is disabled or is deleted.|The error message returned when the specified image is disabled or deleted.|
|403|InvalidSnapshotId.NotReady|The specified snapshot has not completed yet.|The error message returned when the specified snapshot has not been completed.|
|403|OperationDenied|The specified snapshot is not allowed to create disk.|The error message returned when no disk can be created for the specified snapshot.|
|403|InvalidDevice.InUse|The specified device has been occupied.|The error message returned when the specified device has been attached to a disk.|
|403|ImageRemovedInMarket|The specified market image is not available, or the specified user defined image includes product code because it is based on an image subscribed from marketplace, and that image in marketplace including exact the same product code has been removed.|The error message returned when the specified marketplace image is unavailable.|
|404|InvalidClusterId.NotFound|The ClusterId provided does not exist in our records.|The error message returned when the specified ClusterId does not exist.|
|403|OperationDenied|The creation of Instance to the specified Zone is not allowed.|The error message returned when no instance can be created in the specified zone.|
|403|OperationDenied|The specified Zone or cluster does not offer the specified disk category or the specified zone and cluster do not match.|The error message returned when the specified disk category is unavailable in the specified zone or cluster, or when the specified zone and cluster do not match.|
|400|InvalidDiskDescription.Malformed|The specified parameter "SystemDisk.DiskDescription or DataDisk.N.Description" is not valid.|The error message returned when the specified SyatemDisk.DiskDescription or DataDisk.N.Description is invalid.|
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
|404|InvalidImageId.NotFound|The specified ImageId does not exist.|The error message returned when the specified image does not exist under this account. Check whether the image ID is correct.|
|404|OperationDenied|Another Instance has been creating|The error message returned when no new instances can be created.|
|403|InvalidDiskSize.TooSmall|Specified disk size is less than the size of snapshot|The error message returned when the specified disk has insufficient space for the snapshot.|
|403|OperationDenied|The type of the disk does not support the operation|The error message returned when the current disk category does not support the specified operation.|
|404|InvalidInstanceChargeType.NotFound|The InstanceChargeType does not exist in our records|The error message returned when the specified instance type does not exist.|
|400|InvalidPeriod|The specified period is not valid.|The error message returned when the specified parameter is invalid.|
|400|InvalidDataDiskCategory.ValueNotSupported|The specified parameter " DataDisk.N.Category " is not valid.|The error message returned when the specified disk type is invalid.|
|400|InstanceDiskCategoryLimitExceed|The specified DataDisk.N.Size beyond the permitted range, or the capacity of snapshot exceeds the size limit of the specified disk category.|The error message returned when the maximum size of the specified data disk is reached.|
|403|OperationDenied|The resource is out of usage.|The error message returned when the instance is not in the running state. Enable the instance or check whether a proper operation is performed.|
|404|InvalidSystemDiskSize.LessThanImageSize|The specified parameter SystemDisk.Size is less than the image size.|The error message returned when the specified SystemDisk.Size is less than the image size.|
|400|InvalidSystemDiskCategory.ValueNotSupported|The specified parameter SystemDisk.Category is not valid.|The error message returned when the specified SystemDisk.Category is invalid.|
|403|InvalidParameter.ResourceOwnerAccount|ResourceOwnerAccount is Invalid.|The error message returned when the specified ResourceOwnerAccount is invalid.|
|403|InvalidUserData.Forbidden|User not authorized to input the parameter "UserData", please apply for permission "UserData"|The error message returned when you are not authorized to configure UserData.|
|400|InvalidUserData.NotSupported|The specified parameter "UserData" only support the vpc and IoOptimized Instance.|The error message returned when the specified UserData is only supported in VPC-type or optimized instances.|
|403|InvalidResourceType.NotSupported|This resource type is not supported; please try other resource types.|The error message returned when the specified resource type is out of stock.|
|403|InvalidInstanceType.ZoneNotSupported|The specified zone does not support this instancetype.|The error message returned when the specified instance type is not supported in the specified zone.|
|400|InstanceDiskNumber.LimitExceed|The total number of specified disk in an instance exceeds.|The error message returned when the maximum number of the specified disks in the instance is reached.|
|400|Account.Arrearage|Your account has an outstanding payment.|The error message returned when you have unpaid orders under your account.|
|400|InvalidDiskCategory.ValueNotSupported|The specified parameter "DiskCategory" is not valid.|The error message returned when the specified DiskCategory is invalid.|
|400|InvalidAutoRenewPeriod.ValueNotSupported|The specified autoRenewPeriod is not valid.|The error message returned when the specified AutoRenewPeriod is invalid.|
|400|InvalidParameter.Bandwidth|%s|The error message returned when the parameter is invalid.|
|400|InvalidDataDiskCategory.ValueNotSupported|%s|The error message returned when the parameter is invalid.|
|400|InvalidSystemDiskCategory.ValueNotSupported|%s|The error message returned when the parameter is invalid.|
|400|InvalidParameter.Conflict|%s|The error message returned when the parameter is in conflict with another parameter.|
|400|InvalidInternetChargeType.ValueNotSupported|%s|The error message returned when the parameter is invalid.|
|400|InvalidInstanceType.ValueNotSupported|%s|The error message returned when the specified instance type is invalid.|
|403|InstanceType.Offline|%s|The error message returned when the specified instance type is unavailable.|
|500|InternalError|%s|The error message returned when an unknown internal error occurs.|
|400|InvalidSystemDiskSize.ValueNotSupported|%s|The error message returned when the parameter is invalid.|
|400|InvalidDataDiskSize.ValueNotSupported|%s|The error message returned when the parameter is invalid.|
|404|InvalidKeyPairName.NotFound|The specified parameter "KeyPairName" does not exist in our records.|The error message returned when the specified KeyPairName does not exist.|
|403|DependencyViolation.WindowsInstance|The instance creating is window, cannot use ssh key pair to login.|The error message returned when SSH key pairs are not supported in Windows.|
|400|InvalidInstanceType.ValueNotSupported|The specified parameter "KeyPairName" only support IoOptimized Instance.|The error message returned when SSH key pairs are not supported in optimized instances.|
|403|RealNameAuthenticationError|Your account has not passed the real-name authentication yet.|The error message returned when you failed the real-name authentication.|
|400|OperationDenied|The specified instance type or Zone is not available or not authorized.|The error message returned when the specified instance type or zone is unavailable or unauthorized.|
|403|InvalidAccountStatus.NotEnoughBalance|Your account does not have enough balance.|The error message returned when your account has insufficient balance.|
|400|InvalidParameter.EncryptedIllegal|%s|The error message returned when the parameter is invalid.|
|400|InvalidParameter.EncryptedNotSupported|%s|The error message returned when the parameter is invalid.|
|400|EncryptedOption.Conflict|%s|The error message returned when the parameter is invalid.|
|400|InvalidParameter.Encrypted.KmsNotEnabled|The encrypted disk need enable KMS|The error message returned when KMS is not enabled for encrypted disks|
|500|InternalError|The request processing has failed due to some unknown error, exception or failure.|The error message returned when an unknown error occurs.|
|400|InvalidSpotPriceLimit.LowerThanPublicPrice|The specified parameter "soptPriceLimit" can't be lower than current public price.|The error message returned when the specified SpotPriceLimit is lower than the current price.|
|400|InvalidHpcClusterId.Unnecessary|The specified HpcClusterId is unnecessary.|The error message returned when the specified HpcClusterId is invalid.|
|400|InvalidVSwitchId.Necessary|The VSwitchId is necessary.|The error message returned when VSwitchId is not specified.|
|400|InvalidHpcClusterId.Necessary|The HpcClusterId is necessary.|The error message returned when HpcClusterId is not specified.|
|400|InvalidHpcClusterId.NotFound|The specified HpcClusterId is not found.|The error message returned when the specified HPC cluster ID does not exist.|
|400|InvalidHpcClusterId.Creating|The specified HpcClusterId is creating.|The error message returned when the specified HPC cluster is being created.|
|400|InvalidPeriodUnit.ValueNotSupported|The specified parameter PeriodUnit is not valid.|The error message returned when the specified PeriodUnit is invalid.|
|400|IncorrectImageStatus|Encrypted snapshots do not support this operation.|The error message returned when the operation is not supported on encrypted snapshots.|
|400|InvalidTagValue.Malformed|The specified Tag.N.Value is not valid.|The error message returned when the specified Tag.N.Value is invalid.|
|400|InvalidSecurityGroup.NotInDefaultVpc|%s|The error message returned when the specified security group is not in the default VPC.|
|403|InvalidParameter.NotMatch|%s|The error message returned when the parameter is in conflict with another parameter.|
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
|400|ChargeTypeViolation.PostPaidDedicatedHost|Prepaid instance onto postpaid dedicated host is not allowed.|The error message returned when the billing method is changed for DDHs.|
|403|InvalidVSwitch.DefaultVSwitchNotSupport|The specified zone in vpc can't support create default vSwitch.|The error message returned when the default VSwitch is not supported in VPCs of the specified zone.|
|400|InvalidParameter.CreditSpecification|The specified CreditSpecification is not supported in this region.|The error message returned when the specified CreditSpecification is not supported in this region.|
|400|IncorrectImageStatus|The specified Image is not available.|The error message returned when the status of the specified source image is incorrect.|
|404|InvalidMarketImage.NotFound|The specified marketplace image does not exist, please change the imageId and try again.|The error message returned when the specified marketplace image does not exist.|
|400|InvalidInstanceType.NotSupported|The specified instanceType is not supported by the deployment set.|The error message returned when the instance type is not supported in the specified deployment set.|
|400|InvalidVpcZone.NotSupported|Zone of the specified VSwitch is not available for creating, please try in other zones.|The error message returned when the default VSwitch is not supported in VPCs of the specified zone.|
|400|IncorrectDefaultVpcStatus|The status of the default VPC is invalid.|The error message returned when the status of the default VPC is incorrect.|
|404|DeploymentSet.NotFound|The specified deployment set does not exist.|The error message returned when the specified deployment set does not exist.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

