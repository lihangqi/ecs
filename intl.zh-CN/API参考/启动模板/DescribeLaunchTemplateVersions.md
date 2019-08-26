# DescribeLaunchTemplateVersions {#doc_api_Ecs_DescribeLaunchTemplateVersions .reference}

查询实例启动模板版本。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=DescribeLaunchTemplateVersions)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|RegionId|String|是|cn-hangzhou|实例启动模板所属的地域 ID。您可以调用 [DescribeRegions](~~25609~~) 查看最新的阿里云地域列表。

 |
|Action|String|否|DescribeLaunchTemplateVersions|系统规定参数。取值：DescribeLaunchTemplateVersions

 |
|DefaultVersion|Boolean|否|true|是否查询默认版本。

 |
|LaunchTemplateId|String|否|lt-launchtemplateid1|实例启动模板 ID。您必须指定 LaunchTemplateId 或 LaunchTemplateName 以确定模板。

 |
|LaunchTemplateName|String|否|FinanceJoshua|实例启动模板名称。

 |
|LaunchTemplateVersion.N|RepeatList|否|1|一个或多个实例启动模板版本。

 |
|MaxVersion|Long|否|10|通过范围指定版本时的最大版本号。

 |
|MinVersion|Long|否|1|通过范围指定版本时的最小版本号。

 |
|PageNumber|Integer|否|1|实例启动模板列表的页码。起始值：1

 默认值：1

 |
|PageSize|Integer|否|10|分页查询时设置的每页行数。最大值：50

 默认值：10

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|LaunchTemplateVersionSets| | |关于模板版本的信息

 |
|└CreateTime|String|2018-05-14T14:18:00Z|模板创建时间

 |
|└CreatedBy|String|1942111349714xxx|模板的创建者

 |
|└DefaultVersion|Boolean|true|模板默认版本

 |
|└LaunchTemplateData| | |模板具体配置

 |
|└AutoReleaseTime|String|2018-05-14T14:18:00Z|自动释放时间

 |
|└DataDisks| | |数据盘和信合集

 |
|└Category|String|cloud\_ssd|数据盘的磁盘种类

 |
|└DeleteWithInstance|Boolean|true|数据盘是否随实例释放而释放

 |
|└Description|String|FinanceDept|数据盘描述

 |
|└Device|String|/dev/xvda|数据盘的设备名

 |
|└DiskName|String|FinanceJoshua|数据盘名称

 |
|└Encrypted|String|false|数据盘是否加密

 |
|└Size|Integer|2000|数据盘大小

 |
|└SnapshotId|String|s-snapshotid1|数据盘使用的快照 ID

 |
|└Description|String|FinanceDept|实例描述

 |
|└EnableVmOsConfig|Boolean|false|是否启用实例操作系统配置。

 **说明：** 该参数即将被弃用，为提高兼容性，请尽量使用其他参数。

 |
|└HostName|String|JoshuaHost|实例主机名

 |
|└ImageId|String|m-imagid1|实例使用的镜像 ID

 |
|└ImageOwnerAlias|String|system|镜像来源。

 |
|└InstanceChargeType|String|Postpaid|实例计费类型。

 |
|└InstanceName|String|FinanceJoshua|实例名称

 |
|└InstanceType|String|ecs.g5.large|实例规格

 |
|└InternetChargeType|String|PayByTraffic|公网带宽计费方式

 |
|└InternetMaxBandwidthIn|Integer|5|网入带宽最大值

 |
|└InternetMaxBandwidthOut|Integer|200|公网出带宽最大值

 |
|└IoOptimized|String|none|是否为 I/O 优化实例

 |
|└KeyPairName|String|FinanceJoshuaV25|密钥对名称

 |
|└NetworkInterfaces| | |弹性网卡的属性集合

 |
|└Description|String|FinanceDept|弹性网卡描述信息

 |
|└NetworkInterfaceName|String|FinanceJoshua|弹性网卡名称

 |
|└PrimaryIpAddress|String|203.0.113.2|主私有 IP 地址

 |
|└SecurityGroupId|String|sg-securitygroupid1|所属的安全组 ID 必须是同一个 VPC 下的安全组

 |
|└VSwitchId|String|vsw-vswitchid1|弹性网卡所属的虚拟交换机 ID

 |
|└NetworkType|String|vpc|网络类型

 |
|└PasswordInherit|Boolean|true|是否继承原镜像里设置的用户名密码

 |
|└Period|Integer|1|购买资源的时长

 |
|└RamRoleName|String|FinanceDeptTest|实例 RAM 角色名称

 |
|└ResourceGroupId|String|rg-resourcegroupid1|启动模板所在的企业资源组 ID。

 |
|└SecurityEnhancementStrategy|String|active|是否开启安全加固

 |
|└SecurityGroupId|String|sg-securitygroupid1|安全组 ID

 |
|└SpotDuration|Integer|1|实例保护周期。

 |
|└SpotPriceLimit|Float|0.98|设置实例的每小时最高价格

 |
|└SpotStrategy|String|NoSpot|按量付费实例的竞价策略

 |
|└SystemDisk.Category|String|cloud\_ssd|系统盘种类

 |
|└SystemDisk.Description|String|FinanceDept|系统盘描述

 |
|└SystemDisk.DiskName|String|FinanceJoshua|系统盘名称

 |
|└SystemDisk.Iops|Integer|30000|系统盘每秒I/O次数。

 **说明：** 该参数即将被弃用，为提高兼容性，请尽量使用其他参数。

 |
|└SystemDisk.Size|Integer|80|系统盘大小，单位为 GiB

 |
|└Tags| | |实例的标签

 |
|└Key|String|FinanceDept|实例的标签键

 |
|└Value|String|FinanceDeptJoshua|实例的标签值

 |
|└UserData|String|SGVsbG9FQ1M=|实例自定义数据，以 Base64 方式编码

 |
|└VSwitchId|String|vsw-vswitchid2|实例所属的虚拟交换机 ID

 |
|└VpcId|String|v-vpcid2|专有网络VPC ID。

 |
|└ZoneId|String|cn-hangzhou-g|可用区 ID

 |
|└LaunchTemplateId|String|lt-launchtemplateid|模板 ID

 |
|└LaunchTemplateName|String|FinanceJoshua|模板名称

 |
|└ModifiedTime|String|2018-05-14T14:18:00Z|模板修改时间

 |
|└VersionDescription|String|InitialVersion|模板版本描述

 |
|└VersionNumber|Long|1|模板版本号

 |
|RequestId|String|04F0F334-1335-436C-A1D7-6C044FExxxxx|请求 ID

 |
|PageSize|Integer|10|分页查询时设置的每页行数

 |
|PageNumber|Integer|1|当前页码

 |
|TotalCount|Integer|1|实例启动模板总数

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

https://ecs.aliyuncs.com/?Action=DescribeLaunchTemplateVersions
&RegionId=cn-hangzhou
&LaunchTemplateName=lt-name1
&<公共请求参数>

```

正常返回示例

`XML` 格式

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

`JSON` 格式

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

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InvalidRegion.NotExist|%s|指定的Region不存在。|
|400|MissingParameter|%s|缺失必需参数。|
|400|InvalidParameter|%s|参数格式不正确。|
|404|InvalidLaunchTemplate.NotFound|The specified LaunchTemplate is not found.|指定的模板未找到。|
|403|InnerServiceFailed|%s|内部服务调用失败。|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Ecs)

