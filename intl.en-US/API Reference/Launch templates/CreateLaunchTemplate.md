# CreateLaunchTemplate {#doc_api_1130759 .reference}

Creates an instance launch template, or template for short. An instance launch template removes the need to configure a large number of parameters every time you create an instance.

## Description {#description .section}

Instance launch templates contain preset configurations used to create instances, such as the instance region, image ID, instance type, security group ID, and public bandwidth settings. If the configuration of a certain parameter is not included in the template, that parameter must be specified manually during instance creation. After you create a template \(`CreateLaunchTemplate`\), its version number is set to 1 by default. You can create multiple versions \(`CreateLaunchTemplateVersion`\) based on this template. Version numbers start from 1 and increase sequentially. If you do not specify a template version number when creating an instance \([RunInstances](~~63440~~)\), the default version will be used.

When you call this operation, note that:

-   You can create up to 30 instance launch templates in each region. Each template can have up to 30 versions.
-   Most instance launch template parameters are optional. When you create a template, ECS does not verify the existence or validity of its parameter values. The validity of specified parameter values cannot be verified until you create instances with the template.
-   If you configure a certain parameter in an instance launch template, you cannot filter out this parameter when creating an instance \([RunInstances](~~63440~~)\). For example, if `HostName=LocalHost` is configured in the template, and the value of the `HostName` parameter is not specified in the `RunInstances` operation, the host name of the instance is still `LocalHost`. If you want to overwrite the `HostName=LocalHost` configuration, you can configure `RunInstances` or other parameters in the `HostName=MyHost` operation.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=CreateLaunchTemplate) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|LaunchTemplateName|String|Yes|JoshuaWinPrePaid| The name of the instance launch template. The name must be 2 to 128 characters in length. It must start with a letter and cannot start with http:// or https://. It can contain letters, digits, colons \(:\), underscores \(\_\), and hyphens \(-\).

 |
|RegionId|String|Yes|cn-hangzhou| The ID of the region. You can call [DescribeRegions](~~25609~~) to view the latest regions of Alibaba Cloud.

 |
|Action|String|No|CreateLaunchTemplate| The operation that you want to perform. Set the value to CreateLaunchTemplate.

 |
|AutoReleaseTime|String|No|2018-01-01T12:05:00Z| The time when the instance is automatically released. The time follows the [ISO 8601](~~25696~~) standard and uses UTC time. The format is yyyy-MM-ddTHH:mm:ssZ.

 -   If the value of the seconds place \(`ss`\) is not `00`, the time will automatically be set to the start of the specified minute \(`mm`\).
-   The specified release time must be at least half an hour later than the current time.
-   The specified release time cannot be more than three years later than the current time.

 |
|DataDisk.N.Category|String|No|cloud\_ssd| The category of data disk N. Valid values:

 -   cloud: basic disk
-   cloud\_efficiency: ultra disk
-   cloud\_ssd: SSD
-   ephemeral\_ssd: local SSD
-   cloud\_essd: ESSD disk

 |
|DataDisk.N.DeleteWithInstance|Boolean|No|true| Indicates whether data disk N is released together with the instance.

 |
|DataDisk.N.Description|String|No|FinanceDept| The description of data disk N. The description must be 2 to 256 characters in length and cannot start with http:// or https://.

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
|DataDisk.N.SnapshotId|String|No|s-bp17441ohwka0yuhx3h0| The ID of the snapshot used to create the data disk. Valid values of n: 1 to 16. If the `DataDisk.n.SnapshotId` parameter is specified, the `DataDisk.n.Size` parameter will be ignored, and the size of the created disk will be the size of the specified snapshot. The specified snapshot cannot be created on or before July 15, 2013. Otherwise, an error will be returned.

 |
|Description|String|No|FinaceDept| The description for the instance. The description must be 2 to 256 characters in length and cannot start with http:// or https://.

 |
|EnableVmOsConfig|Boolean|No|false| Indicates whether to enable the operating system configuration of the instance.

 **Note:** This parameter will be removed in the future. We recommend that you use other parameters to ensure compatibility.

 |
|HostName|String|No|JoshuaHost| The name of the host that will contain the created ECS instances.

 -   It cannot start or end with a period \(.\) or a hyphen \(-\). It cannot contain consecutive periods \(.\) or hyphens \(-\).
-   On Windows, the hostname must be 2 to 15 characters in length. The hostname cannot contain periods \(.\) or contain only digits. It can contain letters, digits, and hyphens \(-\).
-   On other OSs such as Linux, the hostname must be 2 to 64 characters in length. It can be segments separated with periods \(.\). Each segment can contain letters, digits, and hyphens \(-\).

 |
|ImageId|String|No|win2008r2\_64\_ent\_sp1\_en-us\_40G\_alibase\_20170915.vhd| The ID of the image file to be used to create the instances. You can call [DescribeImages](~~25534~~) to query available images.

 |
|ImageOwnerAlias|String|No|system| The source of the image. Valid values:

 -   system: public images provided by Alibaba Cloud.
-   self: your custom images.
-   others: shared images from other Alibaba Cloud users.

 Default value: null, indicating that the results matching system, self, and others are returned.

 |
|InstanceChargeType|String|No|PrePaid| The billing method of the instance. Valid values:

 -   PrePaid: Subscription If you select this billing method, ensure that you have activated credit card payment for your account. Otherwise, the error message `InvalidPayMethod` will be returned.
-   Postpaid: Pay-As-You-Go.

 |
|InstanceName|String|No|JoshuaHost| The name of the instance. The name must be 2 to 128 characters in length. It must start with a letter and cannot start with http:// or https://. It can contain letters, digits, colons \(:\), underscores \(\_\), and hyphens \(-\).

 |
|InstanceType|String|No|ecs.g5.large| The instance type. For more information, see [Instance type families](~~25378~~) or call [DescribeInstanceTypes](~~25620~~) to query latest instance types.

 |
|InternetChargeType|String|No|PayByTraffic| The billing method of network bandwidth. Valid values:

 -   PayByTraffic: You are billed based on the actual amount of bandwidth used by traffic.

 |
|InternetMaxBandwidthIn|Integer|No|200| The maximum inbound bandwidth from the Internet. Unit: Mbit/s. Valid values: 1 to 200.

 |
|InternetMaxBandwidthOut|Integer|No|5| The maximum outbound bandwidth to the Internet. Unit: Mbit/s. Valid values: 0 to 100.

 |
|IoOptimized|String|No|optimized| Indicates whether the instance is I/O optimized. Valid values:

 -   none: The instance is not I/O optimized.
-   optimized: The instance is I/O optimized.

 |
|KeyPairName|String|No|Instancetest| The name of the key pair.

 -   For a Windows ECS instance, this parameter is ignored. The `Password` parameter is still effective even when the KeyPairName parameter is specified.
-   For a Linux ECS instance, the username and password authentication method is disabled by default.

 |
|NetworkInterface.N.Description|String|No|FinnanceDept| The description of an ENI. The description must be 2 to 256 characters in length and cannot start with http:// or https://.

 **Note:** The value of N in the `NetworkInterface.N` parameter must be either 0 or 1.

 |
|NetworkInterface.N.NetworkInterfaceName|String|No|FinnanceJoshua| The name of the ENI.

 **Note:** The value of N in the `NetworkInterface.N` parameter must be either 0 or 1.

 |
|NetworkInterface.N.PrimaryIpAddress|String|No|192.168.2.XXX| The primary private IP address of the ENI.

 **Note:** The value of N in the `NetworkInterface.N` parameter must be either 0 or 1.

 |
|NetworkInterface.N.SecurityGroupId|String|No|sg-bp15ed6xe1yxeycg7ov3| The ID of the security group to which the ENI belongs. The security group of the ENI must belong to the same VPC as that of the instance.

 **Note:** The value of N in the `NetworkInterface.N` parameter must be either 0 or 1.

 |
|NetworkInterface.N.VSwitchId|String|No|vsw-bp1s5fnvk4gn2tws03ziX| The ID of the VSwitch to which the ENI belongs. The instance must be in the same zone of the same VPC network as the ENI, but they can belong to different VSwitches.

 **Note:** The value of N in the `NetworkInterface.N` parameter must be either 0 or 1.

 |
|NetworkType|String|No|vpc| The network type of the instance. Valid values:

 -   classic
-   vpc

 |
|Period|Integer|No|1| The duration of the subscription. Unit: month. This parameter is required when the value of the `InstanceChargeType` parameter is set to `PrePaid` and only takes effect when this condition is met. If the DedicatedHostId parameter is specified, the value range of the Period parameter must be within the subscription period of the dedicated host. Valid values:

 -   When the PeriodUnit parameter is set to Week,the valid values of the Period parameter are \{"1", "2", "3", "4"\}.
-   When the PeriodUnit parameter is set to Month,the valid values of the Period parameter are \{ "1", "2", "3", "4", "5", "6", "7", "8", "9", "12", "24", "36", "48", "60"\}.

 |
|RamRoleName|String|No|FinanceDept| The RAM role name of the instance. You can call the RAM operation [ListRoles](~~28713~~) to query the RAM roles that you have created.

 |
|ResourceGroupId|String|No|rg-resourcegroupid1| The ID of the resource group to which the instance, disk, and ENI belong.

 |
|SecurityEnhancementStrategy|String|No|Deactive| Indicates whether to enable security hardening for the operating system. Valid values:

 -   Active: enables security hardening for public images.
-   Deactive: disables security hardening for all images.

 |
|SecurityGroupId|String|No|sg-bp15ed6xe1yxeycg7ov3| The ID of the security group that the created instance will belong to. Instances within the same security group can access one another. A security group can contain up to 1,000 instances.

 |
|SpotDuration|Integer|No|1| The protection period of the instance.

 **Note:** This parameter will be removed in the future. We recommend that you use other parameters to ensure compatibility.

 |
|SpotPriceLimit|Float|No|0.97| The maximum hourly price of the instance. This parameter supports up to three decimal places and takes effect when the value of the `SpotStrategy` parameter is `SpotWithPriceLimit`.

 |
|SpotStrategy|String|No|NoSpot| The preemption policy of a Pay-As-You-Go instance. This parameter takes effect only when the value of the `InstanceChargeType` parameter is `PostPaid`. Valid values:

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
|SystemDisk.Size|Integer|No|40| The size of the system disk. Unit: GiB. Valid values: 20 to 500.

 The value of this parameter must be at least 20 GiB, or greater than or equal to the value of ImageSize.

 |
|Tag.N.Key|String|No|FinanceDept| The tag key of an instance, disk, or NIC. Valid values of N: 1 to 5. It cannot be a null string. It can be a maximum of 64 characters in length. It cannot start with aliyun or acs:. It cannot contain http:// or https://.

 |
|Tag.N.Value|String|No|FinanceDept.Joshua| The tag value of an instance, disk, or NIC. Valid values of N: 1 to 5. It can be a null string. It can be a maximum of 128 characters in length. It cannot start with aliyun or acs:. It cannot contain http:// or https://.

 |
|TemplateResourceGroupId|String|No|rg-resourcegroupid2| The ID of the resource group to which the launch template belongs.

 |
|TemplateTag.N.Key|String|No|LTFinance| The tag key of the launch template. Valid values of N: 1 to 20. It cannot be a null string. It can be a maximum of 64 characters in length. It cannot start with aliyun or acs:. It cannot contain http:// or https://.

 |
|TemplateTag.N.Value|String|No|LTFinanceJoshua| The tag value of the launch template. Valid values of N: 1 to 20. It can be a null string. It can be a maximum of 128 characters in length. It cannot start with aliyun, acs:, http://, or https://.

 |
|UserData|String|No|ZWNobyBoZWxsbyBlY3Mh| The custom data of the instance. It is encoded by using Base64. The maximum size of the raw data is 16 KB.

 |
|VSwitchId|String|No|vsw-bp1s5fnvk4gn2tws03ziX| The ID of the VSwitch. If you are creating VPC-type instances, you must specify this parameter.

 |
|VersionDescription|String|No|LTFinanceJoshua| The description of instance launch template version 1. The description must be 2 to 256 characters in length and cannot start with http:// or https://.

 |
|VpcId|String|No|vpc-bp12433upq1y5sceni07X| The ID of the VPC.

 |
|ZoneId|String|No|cn-hangzhou-g| The ID of the zone to which the instance belongs.

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|LaunchTemplateId|String|lt-m5eiaupmvm2op9dxxxxx| The ID of the instance launch template.

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=CreateLaunchTemplate
&LaunchTemplateName=JoshuaWinPrePaid 
&RegionId=cn-hangzhou
&TemplateTag. 1. Key=LTFinance
&TemplateTag. 1. Value=LTFinanceJoshua
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
&SecurityEnhancementStrategy=Deactive
&Tag. 1. Key=FinanceDept
&Tag. 1. Value=FinanceDept.Joshua
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<CreateLaunchTemplateResponse>
  <RequestId>04F0F334-1335-436C-A1D7-6C044FExxxxx</RequestId>
  <LaunchTemplateId>lt-m5eiaupmvm2op9dxxxxx</LaunchTemplateId>
</CreateLaunchTemplateResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"LaunchTemplateId":"lt-m5eiaupmvm2op9dxxxxx",
	"RequestId":"04F0F334-1335-436C-A1D7-6C044FExxxxx"
}
```

## Error codes {#section_r0e_mhh_p31 .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|400|InvalidRegion.NotExist|%s|The error message returned when the specified region does not exist.|
|403|LaunchTemplateLimitExceed|%s|The error message returned when the number of launch templates has reached the upper limit.|
|403|LaunchTemplateName.Duplicated|%s|The error message returned when the specified template name is already in use.|
|400|MissingParameter|%s|The error message returned when a required parameter is not specified.|
|400|InvalidParameter|%s|The error message returned when the parameter format is invalid.|
|400|InvalidLaunchTemplateName.Malformed|The specified parameter LaunchTemplateName is not valid.|The error message returned when the specified value of the LaunchTemplateName parameter is invalid.|
|400|InvalidDescription.Malformed|The specified parameter VersionDescription is not valid.|The error message returned when the format of the specified template version description is invalid.|
|403|InnerServiceFailed|%s|The error message returned when an internal service failed to be called.|
|400|InvalidUserData.SizeExceeded|%s|The error message returned when the size of the specified custom data exceeds the limit.|
|400|InvalidUserData.Base64FormatInvalid|%s|The error message returned when the format of the specified template version description is invalid.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

