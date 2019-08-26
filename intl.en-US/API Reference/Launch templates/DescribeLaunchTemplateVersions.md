# DescribeLaunchTemplateVersions {#doc_api_1090646 .reference}

Queries one or more instance launch template versions.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=DescribeLaunchTemplateVersions) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|RegionId|String|Yes|cn-hangzhou| The ID of the region to which the instance launch template belongs. You can call [DescribeRegions](~~25609~~) to view the latest regions of Alibaba Cloud.

 |
|Action|String|No|DescribeLaunchTemplateVersions| The operation that you want to perform. Set the value to DescribeLaunchTemplateVersions.

 |
|DefaultVersion|Boolean|No|true| Indicates whether to query the default version.

 |
|DetailFlag|Boolean|No|true| Indicates whether the details tag is supported.

 **Note:** This parameter will be removed in the future. We recommend that you use other parameters to ensure compatibility.

 |
|LaunchTemplateId|String|No|lt-launchtemplateid1| The ID of the instance launch template. You must specify either the LaunchTemplateId parameter or the LaunchTemplateName parameter to determine a launch template.

 |
|LaunchTemplateName|String|No|FinanceJoshua| The name of the instance launch template.

 |
|LaunchTemplateVersion.N|RepeatList|No|1| One or more instance launch template versions.

 |
|MaxVersion|Long|No|10| The maximum version number when a range is used to specify the template.

 |
|MinVersion|Long|No|1| The minimum version number when a range is used to specify the template.

 |
|OwnerAccount|String|No|EcsforCloud@Alibaba.com| The logon name of a RAM user.

 |
|PageNumber|Integer|No|1| The page number that you query in the instance launch template list. Starting value: 1.

 Default value: 1.

 |
|PageSize|Integer|No|10| The number of entries per page. Maximum value: 50.

 Default value: 10.

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|LaunchTemplateVersionSets| | | A set of template versions.

 |
|└CreateTime|String|2018-05-14T14:18:00Z| The creation time of the template.

 |
|└CreatedBy|String|1942111349714xxx| The creator of the template.

 |
|└DefaultVersion|Boolean|true| The default version of the template.

 |
|└LaunchTemplateData| | | The specific configurations of the template.

 |
|└AutoReleaseTime|String|2018-05-14T14:18:00Z| The automatic release time of the template.

 |
|└DataDisks| | | A set of data disks.

 |
|└Category|String|cloud\_ssd| The category of the data disk.

 |
|└DeleteWithInstance|Boolean|true| Indicates whether the data disk is released together with the instance.

 |
|└Description|String|FinanceDept| The description of the data disk.

 |
|└Device|String|/dev/xvda| The device name of the data disk.

 |
|└DiskName|String|FinanceJoshua| The name of the data disk.

 |
|└Encrypted|String|false| Indicates whether the data disk is encrypted.

 |
|└Size|Integer|2000| The size of the data disk.

 |
|└SnapshotId|String|s-snapshotid1| The ID of the snapshot used to create the data disk.

 |
|└Description|String|FinanceDept| The description of the instance.

 |
|└EnableVmOsConfig|Boolean|false| Indicates whether the operating system configuration of the instance is enabled.

 **Note:** This parameter will be removed in the future. We recommend that you use other parameters to ensure compatibility.

 |
|└HostName|String|JoshuaHost| The hostname of the instance.

 |
|└ImageId|String|m-imagid1| The ID of the image used by the instance.

 |
|└ImageOwnerAlias|String|system| The source of the image.

 |
|└InstanceChargeType|String|Postpaid| The billing method of the instance.

 |
|└InstanceName|String|FinanceJoshua| The name of the instance.

 |
|└InstanceType|String|ecs.g5.large| The instance type.

 |
|└InternetChargeType|String|PayByTraffic| The billing method of Internet bandwidth.

 |
|└InternetMaxBandwidthIn|Integer|5| The maximum inbound Internet bandwidth.

 |
|└InternetMaxBandwidthOut|Integer|200| The maximum outbound Internet bandwidth.

 |
|└IoOptimized|String|none| Indicates whether the instance is I/O optimized.

 |
|└KeyPairName|String|FinanceJoshuaV25| The name of the key pair.

 |
|└NetworkInterfaces| | | The attributes of the ENI.

 |
|└Description|String|FinanceDept| The description of the ENI.

 |
|└NetworkInterfaceName|String|FinanceJoshua| The name of the ENI.

 |
|└PrimaryIpAddress|String|203.0.113.2| The primary private IP address.

 |
|└SecurityGroupId|String|sg-securitygroupid1| The ID of the security group to which the ENI belongs.

 |
|└VSwitchId|String|vsw-vswitchid1| The ID of the VSwitch to which the ENI belongs.

 |
|└NetworkType|String|vpc| The network type.

 |
|└PasswordInherit|Boolean|true| Indicates whether the username and password pair of the original image is used.

 |
|└Period|Integer|1| The duration of the subscription.

 |
|└RamRoleName|String|FinanceDeptTest| The RAM role name of the instance.

 |
|└ResourceGroupId|String|rg-resourcegroupid1| The ID of the resource group to which the launch template belongs.

 |
|└SecurityEnhancementStrategy|String|active| Indicates whether to enable security hardening.

 |
|└SecurityGroupId|String|sg-securitygroupid1| The ID of the security group.

 |
|└SpotDuration|Integer|1| The protection period of the instance.

 |
|└SpotPriceLimit|Float|0.98| The maximum hourly price of the instance.

 |
|└SpotStrategy|String|NoSpot| The bidding policy of a Pay-As-You-Go instance.

 |
|└SystemDisk.Category|String|cloud\_ssd| The category of the system disk.

 |
|└SystemDisk.Description|String|FinanceDept| The description of the system disk.

 |
|└SystemDisk.DiskName|String|FinanceJoshua| The name of the system disk.

 |
|SystemDisk.Iops|Integer|30000| The number of I/O operations per second for the system disk.

 **Note:** This parameter will be removed in the future. We recommend that you use other parameters to ensure compatibility.

 |
|└SystemDisk.Size|Integer|80| The size of the system disk. Unit: GiB.

 |
|└Tags| | | The tag of the instance.

 |
|└Key|String|FinanceDept| The tag key of the instance.

 |
|└Value|String|FinanceDeptJoshua| The tag value of the instance.

 |
|└UserData|String|SGVsbG9FQ1M=| The custom data of the instance. It is encoded by using Base64.

 |
|└VSwitchId|String|vsw-vswitchid2| The ID of the VSwitch to which the instance belongs.

 |
|└VpcId|String|v-vpcid2| The ID of the VPC.

 |
|└ZoneId|String|cn-hangzhou-g| The ID of the zone.

 |
|└LaunchTemplateId|String|lt-launchtemplateid| The ID of the template.

 |
|└LaunchTemplateName|String|FinanceJoshua| The name of the template.

 |
|└ModifiedTime|String|2018-05-14T14:18:00Z| The time when the template was last modified.

 |
|└VersionDescription|String|InitialVersion| The description of the template version.

 |
|└VersionNumber|Long|1| The version number of the template.

 |
|RequestId|String|04F0F334-1335-436C-A1D7-6C044FExxxxx| The ID of the request.

 |
|PageSize|Integer|10| The number of entries per page.

 |
|PageNumber|Integer|1| The current page number.

 |
|TotalCount|Integer|1| The total number of instance launch templates.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=DescribeLaunchTemplateVersions
&RegionId=cn-hangzhou 
&LaunchTemplateName=lt-name1 
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<DescribeLaunchTemplateVersionsResponse>
  <RequestId>04F0F334-1335-436C-A1D7-6C044FExxxxx</RequestId>
  <TotalCount>1</TotalCount> 
  <PageNumber>1</PageNumber> 
  <PageSize>10</PageSize> 
  <LaunchTemplateVersionSets>
    <LaunchTemplateVersionSet>
      <CreateTime>2018-05-14T14:18:00Z</CreateTime>
      <ModifiedTime>2018-05-14T14:18:00Z</ModifiedTime>
      <LaunchTemplateId>lt-m5e3ofjr1zn1aw7xxxx</LaunchTemplateId>
      <LaunchTemplateName>wd-1526307480xxx</LaunchTemplateName>
      <DefaultVersion>true</DefaultVersion>
      <VersionNumber>1</VersionNumber>
      <CreatedBy>1942111349714xxx</CreatedBy>
      <VersionDescription>wwww</VersionDescription>
      <launchtemplatedata>
        <imageowneralias>ImageOwnerAlias1</imageowneralias>
        <description>Description1</description>
        <resourcegroupid>ResourceGroupId1</resourcegroupid>
        <datadisks>
          <datadisk>
            <snapshotid>SnapshotId1</snapshotid>
            <description>Description1</description>
            <category>cloud_efficiency</category>
            <encrypted>false</encrypted>
            <size>44</size>
            <deletewithinstance>true</deletewithinstance>
            <diskname>DataDiskName1</diskname>
          </datadisk>
        </datadisks>
        <userdata>UserData1</userdata>
        <systemdisk.diskname>SystemDiskDiskName1</systemdisk.diskname>
        <systemdisk.size>44</systemdisk.size>
        <ramrolename>RamRoleName1</ramrolename>
        <networktype>NetworkType1</networktype>
        <networkinterfaces>
          <networkinterface>
            <description>Description1</description>
            <securitygroupid>SecurityGroupId1</securitygroupid>
            <vswitchid>VSwitchId1</vswitchid>
            <networkinterfacename>NetworkInterfaceName1</networkinterfacename>
            <primaryipaddress>PrimaryIpAddress1</primaryipaddress>
          </networkinterface>
        </networkinterfaces>
        <imageid>windows2008.vhd</imageid>
        <spotpricelimit>1</spotpricelimit>
        <systemdisk.category>cloud_efficiency</systemdisk.category>
        <instancetype>ecs.xn4.small</instancetype>
        <spotstrategy>SpotWithPriceLimit</spotstrategy>
        <hostname>HostName1</hostname>
        <tags>
          <instancetag>
            <value>bb</value>
            <key>ss</key>
          </instancetag>
        </tags>
        <keypairname>KeyPairName1</keypairname>
        <systemdisk.iops>22</systemdisk.iops>
        <iooptimized>true</iooptimized>
        <zoneid>ZoneId1</zoneid>
        <systemdisk.description>SystemDiskDescription1</systemdisk.description>
        <securitygroupid>sg-tiantt1234</securitygroupid>
        <vswitchid>vsw-xxxxxx</vswitchid>
        <period>1</period>
        <internetchargetype>PayByBandwidth</internetchargetype>
        <instancename>InstanceName1</instancename>
        <internetmaxbandwidthout>20</internetmaxbandwidthout>
        <internetmaxbandwidthin>1</internetmaxbandwidthin>
        <securityenhancementstrategy>Active</securityenhancementstrategy>
        <autoreleasetime>2019-10-21T00:00:00Z</autoreleasetime>
      </launchtemplatedata>
    </LaunchTemplateVersionSet>
  </LaunchTemplateVersionSets>
</DescribeLaunchTemplateVersionsResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"PageNumber":1,
	"TotalCount":1,
	"PageSize":10,
	"RequestId":"3989ED0C-20A1-4351-A127-2067FF8390AX",
	"LaunchTemplateVersionSets":{
		"LaunchTemplateVersionSet":[
			{
				"LaunchTemplateId":"lt-bp16jovvln1cgaaqg01X",
				"CreateTime":"2018-10-17T07:36:22Z",
				"CreatedBy":"1942111349714xxx",
				"ModifiedTime":"2018-10-17T07:36:22Z",
				"VersionNumber":1,
				"LaunchTemplateData":{
					"ImageId":"centos_7_04_64_20G_alibase_201701015.vhd",
					"SecurityGroupId":"sg-bp1azkttqpldxgtedupX",
					"Description":"DocV587!",
					"NetworkInterfaces":{
						"NetworkInterface":[]
					},
					"DataDisks":{
						"DataDisk":[]
					},
					"SecurityEnhancementStrategy":"Active",
					"ZoneId":"random",
					"ImageOwnerAlias":"system",
					"InternetChargeType":"PayByTraffic",
					"VSwitchId":"vsw-bp1s5fnvk4gn2tws03ziX",
					"VpcId":"vpc-bp1opxu1zkhn00gzv26cX",
					"HostName":"LocalHost",
					"InstanceType":"ecs.g5.large",
					"IoOptimized":"true",
					"NetworkType":"vpc",
					"Tags":{
						"InstanceTag":[]
					},
					"InternetMaxBandwidthOut":5,
					"SystemDisk.Size":40,
					"SystemDisk.Category":"cloud_efficiency",
					"InstanceChargeType":"PostPaid",
					"InstanceName":"JoshuaCentOSPAYG"
				},
				"DefaultVersion":true,
				"LaunchTemplateName":"JoshuaCentOSPAYG",
				"VersionDescription":"EcsV587!"
			}
		]
	}
}
```

## Error codes { .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|400|InvalidRegion.NotExist|%s|The error message returned when the specified region does not exist.|
|400|MissingParameter|%s|The error message returned when a required parameter is not specified.|
|400|InvalidParameter|%s|The error message returned when the parameter format is invalid.|
|404|InvalidLaunchTemplate.NotFound|The specified LaunchTemplate is not found.|The error message returned when the specified launch template does not exist.|
|403|InnerServiceFailed|%s|The error message returned when an internal service failed to be called.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

