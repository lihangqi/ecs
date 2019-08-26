# CreateLaunchTemplateVersion {#doc_api_1131116 .reference}

Creates a new version for a specified instance launch template.

## Description {#description .section}

You can create up to 30 versions of each instance launch template. The `CreateLaunchTemplateVersion` operation allows you to create new versions of templates instead of modifying existing template versions. To modify the parameters of a specific version, you can create a new template version. For more information, see [CreateLaunchTemplate](~~74686~~).

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=CreateLaunchTemplateVersion) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|RegionId|String|Yes|cn-hangzhou| The ID of the region. You can call [DescribeRegions](~~25609~~) to view the latest regions of Alibaba Cloud.

 |
|Action|String|No|CreateLaunchTemplateVersion| The operation that you want to perform. Set the value to CreateLaunchTemplateVersion.

 |
|AutoReleaseTime|String|No|2018-01-01T12:05:00Z| The time when the instance is automatically released. The time follows the [ISO 8601](~~25696~~) standard and uses UTC time. The format is yyyy-MM-ddTHH:mm:ssZ.

 -   If the value of the seconds place \(`ss`\) is not `00`, the time will automatically be set to the start of the specified minute \(`mm`\).
-   It must be at least half an hour past the current time.
-   It must be less than three years from the current time.

 |
|DataDisk.N.Category|String|No|cloud\_ssd| The category of data disk N. Valid values:

 -   cloud: basic disk
-   cloud\_efficiency: ultra disk
-   cloud\_ssd: SSD
-   ephemeral\_ssd: local SSD
-   cloud\_essd: ESSD

 |
|DataDisk.N.DeleteWithInstance|Boolean|No|true| Indicates whether the data disk is released together with the instance.

 |
|DataDisk.N.Description|String|No|FinanceDept| The description of the instance. The description must be 2 to 256 characters in length and cannot start with http:// or https://.

 |
|DataDisk.N.DiskName|String|No|cloud\_ssdData| The name of a data disk. The name must be 2 to 128 characters in length. It must start with a letter and cannot start with http:// or https://. It can contain letters, digits, colons \(:\), underscores \(\_\), and hyphens \(-\).

 |
|DataDisk.N.Encrypted|String|No|false| Indicates whether data disk N is encrypted.

 |
|DataDisk.N.Size|Integer|No|2000| The size of data disk N. Valid values of N: 1 to 16. Unit: GiB. Valid values:

 -   cloud: 5 to 2000
-   cloud\_efficiency: 20 to 32768
-   cloud\_ssd: 20 to 32768
-   cloud\_essd: 20 to 32768
-   ephemeral\_ssd: 5 to 800

 The value of this parameter must be greater than or equal to that of the snapshot specified by the `SnapshotId` parameter.

 |
|DataDisk.N.SnapshotId|String|No|s-bp17441ohwka0yuhx3h0| The ID of the snapshot used to create data disk n. Valid values of n: 1 to 16. If the `DataDisk.n.SnapshotId` parameter is specified, the `DataDisk.n.Size` parameter will be ignored, and the size of the created disk will be the size of the specified snapshot. The specified snapshot cannot be created on or before July 15, 2013. Otherwise, an error will be returned.

 |
|Description|String|No|FinaceDept| The description of the instance. The description must be 2 to 256 characters in length and cannot start with http:// or https://.

 |
|EnableVmOsConfig|Boolean|No|false| Indicates whether to enable the operating system configuration of the instance.

 |
|HostName|String|No|JoshuaHost| The name of the host where the created ECS instances reside.

 -   It cannot start or end with a period \(.\) or a hyphen \(-\). It cannot contain consecutive periods \(.\) or hyphens \(-\).
-   On Windows, the hostname must be 2 to 15 characters in length. The hostname cannot contain periods \(.\) or contain only digits. It can contain letters, digits, and hyphens \(-\).
-   On other OSs such as Linux, the hostname must be 2 to 64 characters in length. It can be segments separated with periods \(.\). Each segment can contain letters, digits, and hyphens \(-\).

 |
|ImageId|String|No|win2008r2\_64\_ent\_sp1\_en-us\_40G\_alibase\_20170915.vhd| The ID of the image to be used to create instances. You can call [DescribeImages](~~25534~~) to query available images.

 |
|ImageOwnerAlias|String|No|system| The source of the image.

 **Note:** This parameter will be removed in the future. We recommend that you use other parameters to ensure compatibility.

 |
|InstanceChargeType|String|No|PrePaid| The billing method of the instance. Valid values:

 -   PostPaid: Pay-As-You-Go

 |
|InstanceName|String|No|JoshuaHost| The name of the instance. The name must be 2 to 128 characters in length. It must start with a letter and cannot start with http:// or https://. It can contain letters, digits, colons \(:\), underscores \(\_\), and hyphens \(-\).

 |
|InstanceType|String|No|ecs.g5.large| The instance type. For more information, see [Instance type families](~~25378~~) or call [DescribeInstanceTypes](~~25620~~) to query latest instance types.

 |
|InternetChargeType|String|No|PayByTraffic| The billing method of the network bandwidth. Valid values:

 -   PayByTraffic: You are billed based on the actual traffic usage.

 |
|InternetMaxBandwidthIn|Integer|No|200| The maximum inbound bandwidth for Internet traffic. Unit: Mbit/s. Valid values: 1 to 200.

 |
|InternetMaxBandwidthOut|Integer|No|5| The maximum outbound bandwidth for Internet traffic. Unit: Mbit/s. Valid values: 0 to 100.

 |
|IoOptimized|String|No|optimized| Indicates whether the instance is I/O optimized. Valid values:

 -   none: The instance is not I/O optimized.
-   optimized: The instance is I/O optimized.

 |
|KeyPairName|String|No|Instancetest| The name of the key pair.

 -   For Windows ECS instances, this parameter is ignored. The `Password` parameter is still effective even when the KeyPairName parameter is specified.
-   By default, the username and password authentication method is disabled for Linux ECS instances.

 |
|LaunchTemplateId|String|No|lt-m5eiaupmvm2op9dxxxxx| The ID of the instance launch template. For more information, call [DescribeLaunchTemplates](~~73759~~). You must specify either the `LaunchTemplateId` parameter or the `LaunchTemplateName` parameter to determine a launch template.

 |
|LaunchTemplateName|String|No|JoshuaWinPrePaid| The name of the instance launch template. The name must be 2 to 128 characters in length. It must start with a letter and cannot start with http:// or https://. It can contain letters, digits, colons \(:\), underscores \(\_\), and hyphens \(-\).

 |
|NetworkInterface.N.Description|String|No|FinnanceDept| The description of the ENI . The description must be 2 to 256 characters in length and cannot start with http:// or https://.

 **Note:** The value of N in the `NetworkInterface.N` parameter cannot be greater than 1.

 |
|NetworkInterface.N.NetworkInterfaceName|String|No|FinnanceJoshua| The name of the ENI.

 **Note:** The value of N in the `NetworkInterface.N` parameter cannot be greater than 1.

 |
|NetworkInterface.N.PrimaryIpAddress|String|No|192.168.2.XXX| The primary private IP address of the ENI.

 **Note:** The value of N in the `NetworkInterface.N` parameter cannot be greater than 1.

 |
|NetworkInterface.N.SecurityGroupId|String|No|sg-bp15ed6xe1yxeycg7ov3| The ID of the security group to which the ENI belongs. The security group of the ENI must belong to the same VPC as the instance.

 **Note:** The value of N in the `NetworkInterface.N` parameter cannot be greater than 1.

 |
|NetworkInterface.N.VSwitchId|String|No|vsw-bp1s5fnvk4gn2tws03ziX| The ID of the VSwitch to which the ENI belongs. The instance must be in the same zone of the same VPC network as the ENI, but they can belong to different VSwitches.

 **Note:** The value of N in the `NetworkInterface.N` parameter cannot be greater than 1.

 |
|NetworkType|String|No|vpc| The network type of the instance. Valid values:

 -   classic
-   vpc

 |
|Period|Integer|No|1| The subscription duration. Unit: month. This parameter takes effect and is required only when the value of the `InstanceChargeType` parameter is set to `PrePaid`. If the DedicatedHostId parameter is specified, the value range of the Period parameter must be within the subscription period of the dedicated host. Valid values:

 -   When the PeriodUnit parameter is set to Week,the valid values of the Period parameter are \{"1", "2", "3", "4"\}.
-   When the PeriodUnit parameter is set to Month,the valid values of the Period parameter are \{ "1", "2", "3", "4", "5", "6", "7", "8", "9", "12", "24", "36", "48", "60"\}.

 |
|RamRoleName|String|No|FinanceDept| The RAM role name of the instance. You can call the RAM operation [ListRoles](~~28713~~) to query the RAM roles that you have created.

 |
|ResourceGroupId|String|No|rg-resourcegroupid| The ID of the resource group.

 **Note:** This parameter will be removed in the future. We recommend that you use other parameters to ensure compatibility.

 |
|SecurityEnhancementStrategy|String|No|Active| Indicates whether to enable security hardening for the operating system. Valid values:

 -   Active: enables security hardening for public images.
-   Deactive: disables security hardening for all images.

 |
|SecurityGroupId|String|No|sg-bp15ed6xe1yxeycg7ov3| The ID of the security group to which the created instances belong. Instances within the same security group can access one another.

 |
|SpotDuration|Integer|No|1| The protection period of the instance.

 **Note:** This parameter will be removed in the future. We recommend that you use other parameters to ensure compatibility.

 |
|SpotPriceLimit|Float|No|0.97| The maximum hourly price of the instance. This parameter supports up to three decimal places.

 |
|SpotStrategy|String|No|NoSpot| The preemption policy of a Pay-As-You-Go instance. This parameter takes effect when the value of the `InstanceChargeType` parameter is `PostPaid`. Valid values:

 -   NoSpot: a normal Pay-As-You-Go instance
-   SpotWithPriceLimit: a preemptible instance with a maximum hourly price
-   SpotAsPriceGo: an instance that is billed based on the actual market price

 |
|SystemDisk.Category|String|No|cloud\_ssd| The category of the system disk. Valid values:

 -   cloud: basic disk
-   cloud\_efficiency: ultra disk
-   cloud\_ssd: SSD
-   ephemeral\_ssd: local SSD
-   cloud\_essd: ESSD

 |
|SystemDisk.Description|String|No|FinanceDept| The description of the system disk. The description must be 2 to 256 characters in length and cannot start with http:// or https://.

 |
|SystemDisk.DiskName|String|No|cloud\_ssdSystem| The name of the system disk. The name must be 2 to 128 characters in length. It must start with a letter and cannot start with http:// or https://. It can contain letters, digits, colons \(:\), underscores \(\_\), and hyphens \(-\).

 |
|SystemDisk.Iops|Integer|No|30000| The number of I/O operations per second for the system disk.

 **Note:** This parameter will be removed in the future. We recommend that you use other parameters to ensure compatibility.

 |
|SystemDisk.Size|Integer|No|40| The size of the system disk. Unit: GiB. Valid values: 20 to 500.

 The value of this parameter must be at least 20 GiB, or greater than or equal to the value of ImageSize.

 |
|Tag.N.Key|String|No|FinanceDept| The tag key of an instance, disk, or NIC. Valid values of N: 1 to 5. It cannot be a null string. It can be a maximum of 64 characters in length. It cannot start with aliyun or acs:. It cannot contain http:// or https://.

 |
|Tag.N.Value|String|No|FinanceDept.Joshua| The tag value of an instance, disk, or NIC. Valid values of N: 1 to 5. It can be a null string. It can be a maximum of 128 characters in length. It cannot start with aliyun or acs:. It cannot contain http:// or https://.

 |
|UserData|String|No|ZWNobyBoZWxsbyBlY3Mh| The custom data of the instance. It is encoded by using Base64. The maximum size of the raw data is 16 KB.

 |
|VSwitchId|String|No|vsw-bp1s5fnvk4gn2tws03ziX| The ID of the VSwitch. If you are creating VPC-type instances, you must specify this parameter.

 |
|VersionDescription|String|No|LTFinanceJoshua| The description of instance launch template. The description must be 2 to 256 characters in length and cannot start with http:// or https://.

 |
|VpcId|String|No|vpc-bp12433upq1y5sceni07X| The ID of the VPC.

 |
|ZoneId|String|No|cn-hangzhou-g| The ID of the zone to which the instance belongs.

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|LaunchTemplateVersionNumber|Long|2| The version number of the instance launch template.

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=CreateLaunchTemplateVersion
&RegionId=cn-hangzhou 
&LaunchTemplateId=lt-m5eiaupmvm2op9dxxxxx
&LaunchTemplateName=JoshuaWinPrePaid
&VersionDescription=LTFinanceJoshua
&ImageId=win2008r2_64_ent_sp1_en-us_40G_alibase_20170915.vhd
&InstanceType=ecs.g5.large
&SecurityGroupId=sg-bp15ed6xe1yxeycg7ov3
&VpcId=vpc-bp12433upq1y5sceni07X
&VSwitchId=vsw-bp1s5fnvk4gn2tws03ziX
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
&DataDisk. 1. Size=2000
&DataDisk. 1. SnapshotId=s-bp17441ohwka0yuhx3h0
&DataDisk. 1. Category=cloud_ssd
&DataDisk. 1. Encrypted=false
&DataDisk. 1. DiskName=cloud_ssdData
&DataDisk. 1. Description=FinanceDept
&DataDisk. 1. DeleteWithInstance=true
&IoOptimized=optimized
&NetworkInterface. 1. PrimaryIpAddress=192.168.2. XXX
&NetworkInterface. 1. VSwitchId=vsw-bp1s5fnvk4gn2tws03ziX
&NetworkInterface. 1. SecurityGroupId=sg-bp15ed6xe1yxeycg7ov3
&NetworkInterface. 1.1etworkInterfaceName=FinnanceJoshua
&NetworkInterface. 1. Description=FinnanceDept
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
&Tag. 1. Key=FinanceDept
&Tag. 1. Value=FinanceDept.Joshua
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<CreateLaunchTemplateVersionResponse>
  <RequestId>04F0F334-1335-436C-A1D7-6C044FExxxxx</RequestId>
  <LaunchTemplateVersionNumber>2</LaunchTemplateVersionNumber>
</CreateLaunchTemplateVersionResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"04F0F334-1335-436C-A1D7-6C044FExxxxx",
	"LaunchTemplateVersionNumber":2
}
```

## Error codes { .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|400|InvalidRegion.NotExist|%s|The error message returned when the specified region does not exist.|
|403|LaunchTemplateVersionLimitExceed|%s|The error message returned when the number of launch template versions has reached the upper limit.|
|404|InvalidLaunchTemplate.NotFound|%s|The error message returned when the specified launch template name does not exist.|
|400|MissingParameter|%s|The error message returned when a required parameter is not specified.|
|400|InvalidParameter|%s|The error message returned when the parameter format is invalid.|
|403|InnerServiceFailed|%s|The error message returned when an internal service failed to be called.|
|400|InvalidUserData.SizeExceeded|%s|The error message returned when the size of the specified custom data exceeds the limit.|
|400|InvalidUserData.Base64FormatInvalid|%s|The error message returned when the specified template version description is not formatted correctly.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

