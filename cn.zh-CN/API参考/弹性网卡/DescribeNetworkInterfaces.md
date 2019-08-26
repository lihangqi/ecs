# DescribeNetworkInterfaces {#doc_api_Ecs_DescribeNetworkInterfaces .reference}

调用DescribeNetworkInterfaces查看弹性网卡（ENI）列表。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=DescribeNetworkInterfaces)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|RegionId|String|是|cn-hangzhou|所在地域ID。您可以调用 [DescribeRegions](~~25609~~) 查看最新的阿里云地域列表。

 |
|Action|String|否|DescribeNetworkInterfaces|系统规定参数。取值：DescribeNetworkInterfaces

 |
|NetworkInterfaceId.N|RepeatList|否|eni-bp17pdijfczaxZZZZ\*\*\*\*\*|弹性网卡ID。一次最多查看100个。

 |
|Tag.N.Key|String|否|test|弹性网卡的标签值。N 的取值范围：1~20。一旦传入该值，可以为空字符串。最多支持 128 个字符，不能以 aliyun 和 acs: 开头，不能包含 http:// 或者 https:// 。

 |
|Tag.N.Value|String|否|api-test|弹性网卡的标签键。N 的取值范围：1~20。一旦传入该值，则不允许为空字符串。最多支持 64 个字符，不能以 aliyun 和 acs: 开头，不能包含 http:// 或者 https:// 。

 |
|ResourceGroupId|String|否|rg-resourcegroupid1|资源组ID。

 |
|VSwitchId|String|否|vsw-bp16usj2p27htro3\*\*\*\*\*|VPC的虚拟交换机ID。

 |
|VpcId|String|否|vsw-bp16usj2p27htro3\*\*\*\*\*|网卡所属的专有网络VPC ID。

 |
|SecurityGroupId|String|否|sg-bp144yr32sx6ndw\*\*\*\*\*|安全组ID。

 |
|NetworkInterfaceName|String|否|my-eni-name|弹性网卡的名称。

 |
|Type|String|否|Secondary|弹性网卡类型。取值范围：

 -   Primary
-   Secondary

 |
|InstanceId|String|否|i-bpm21018033933ea\*\*\*\*\*|弹性网卡当前关联的实例ID。

 |
|PrimaryIpAddress|String|否|172.17.\*\*.\*\*\*|弹性网卡主私有IP地址。

 |
|PageNumber|Integer|否|1|查询结果的页码。取值为正整数。

 默认值：1

 |
|PageSize|Integer|否|100|查询结果的分页大小。取值范围：1~100

 默认值：10

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|NetworkInterfaceSets| | |弹性网卡信息组成的集合

 |
|AssociatedPublicIp| | |弹性网卡辅助私有IP地址关联的公有 IP

 |
|AllocationId|String|eip-2ze88m67qx5z\*\*\*\*\*|EIP的ID

 |
|PublicIpAddress|String|116.62.129.250|实例的公网IP

 |
|CreationTime|String|2017-11-24T06:14:22Z|创建时间

 |
|Description|String|test1|描述

 |
|InstanceId|String|i-instanceId|弹性网卡绑定的实例ID

 **说明：** 由其他阿里云服务管理和控制的弹性网卡不会返回实例ID。

 |
|Ipv6Sets| | |为弹性网卡分配的IPv6地址集合。

 |
|Ipv6Address|String|2001:db8:1234:1a00::\*\*\*|为弹性网卡指定的 IPv6 地址。

 |
|MacAddress|String|00:16:3e:0f:\*\*:\*\*|弹性网卡的 MAC 地址

 |
|NetworkInterfaceId|String|eni-bp17pdijfczaxZZZZ\*\*\*\*\*|弹性网卡ID

 |
|NetworkInterfaceName|String|my-eni-name|弹性网卡的名称

 |
|PrivateIpAddress|String|172.17.\*\*.\*\*\*|实例的私有IP

 |
|PrivateIpSets| | |PrivateIp 组成的集合

 |
|AssociatedPublicIp| | |弹性网卡关联的公有 IP

 |
|AllocationId|String|eip-2ze88m67qx5z\*\*\*\*\*|EIP的ID

 |
|PublicIpAddress|String|116.62.\*\*.250|实例的公网IP

 |
|Primary|Boolean|true|是否是主 IP 地址。

 |
|PrivateIpAddress|String|172.17.\*\*.\*\*\*|实例的私有IP

 |
|ResourceGroupId|String|rg-resourcegroupid1|资源组ID

 |
|SecurityGroupIds| |sg-bp144yr32sx6ndw\*\*\*\*\*|所属的安全组集合

 |
|Status|String|Available|弹性网卡的状态

 |
|Tags| | |标签

 |
|TagKey|String|test|标签键

 |
|TagValue|String|api|标签值

 |
|Type|String|Secondary|弹性网卡类型

 |
|VSwitchId|String|vsw-bp16usj2p27htro3\*\*\*\*\*|VPC的虚拟交换机ID

 |
|VpcId|String|vpc-bp1j7w3gc1cexjqd\*\*\*\*\*|网卡所属的专有网络VPC ID

 |
|ZoneId|String|cn-hangzhou-e|可用区ID

 |
|PageNumber|Integer|1|实例列表的页码

 |
|PageSize|Integer|100|输入时设置的每页行数

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID

 |
|TotalCount|Integer|1|实例总个数

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=DescribeNetworkInterfaces
&RegionId=cn-hangzhou
&Tag.1.Key=test
&Tag.1.Value=api
&ResourceGroupId=rg-resourcegroupid1
&VSwitchId=vsw-bp16usj2p27htro3*****
&VpcId=vsw-bp16usj2p27htro3*****
&PrimaryIpAddress=172.17.**.***
&SecurityGroupId=sg-bp144yr32sx6ndw*****
&NetworkInterfaceName=my-eni-name
&Type=Secondary
&InstanceId=i-AY121018033933ea*****
&NetworkInterfaceId.1=eni-bp17pdijfczaxZZZZ*****
&PageNumber=1
&PageSize=100
&<公共请求参数>
```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeNetworkInterfacesResponse>
  <NetworkInterfaceSets>
    <NetworkInterfaceSet>
      <AssociatedPublicIp/>
      <CreationTime>2017-11-24T06:14:22Z</CreationTime>
      <InstanceId>AY121018033933ea*****</InstanceId>
      <MacAddress>00:16:3e:0f:XX:XX</MacAddress>
      <NetworkInterfaceId>eni-bp17pdijfczaxZZZZ*****</NetworkInterfaceId>
      <PrivateIpAddress>XXX.XXX.XX.XX</PrivateIpAddress>
      <PrivateIpSets>
        <PrivateIpSet>
          <AssociatedPublicIp/>
          <Primary>true</Primary>
          <PrivateIpAddress>XXX.XXX.XX.XX</PrivateIpAddress>
        </PrivateIpSet>
      </PrivateIpSets>
      <SecurityGroupIds>
        <SecurityGroupId>sg-bp144yr32sx6ndw*****</SecurityGroupId>
      </SecurityGroupIds>
      <Status>Available</Status>
      <Type>Secondary</Type>
      <VpcId>vpc-bp1j7w3gc1cexjqd*****</VpcId>
      <VSwitchId>vsw-bp16usj2p27htro3*****</VSwitchId>
      <ZoneId>cn-hangzhou-e</ZoneId>
    </NetworkInterfaceSet>
  </NetworkInterfaceSets>
  <PageNumber>1</PageNumber>
  <PageSize>100</PageSize>
  <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
  <TotalCount>1</TotalCount>
</DescribeNetworkInterfacesResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"PageNumber":1,
	"TotalCount":1,
	"PageSize":100,
	"RequestId":"473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E",
	"NetworkInterfaceSets":{
		"NetworkInterfaceSet":[
			{
				"Type":"Secondary",
				"InstanceId":"AY121018033933ea*****",
				"PrivateIpSets":{
					"PrivateIpSet":[
						{
							"PrivateIpAddress":"XXX.XXX.XX.XX",
							"Primary":true,
							"AssociatedPublicIp":{}
						}
					]
				},
				"ZoneId":"cn-hangzhou-e",
				"VSwitchId":"vsw-bp16usj2p27htro3*****",
				"VpcId":"vpc-bp1j7w3gc1cexjqd*****",
				"AssociatedPublicIp":{},
				"NetworkInterfaceId":"eni-bp17pdijfczaxZZZZ*****",
				"CreationTime":"2017-11-24T06:14:22Z",
				"Status":"Available",
				"MacAddress":"00:16:3e:0f:XX:XX",
				"SecurityGroupIds":{
					"SecurityGroupId":[
						"sg-bp144yr32sx6ndw*****"
					]
				},
				"PrivateIpAddress":"XXX.XXX.XX.XX"
			}
		]
	}
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|403|InvalidUserType.NotSupported|%s|此操作暂不支持您的账号类型。|
|403|Abs.InvalidAccount.NotFound|%s|您的阿里云账号不存在，或者您的AccessKey已经过期。|
|400|MissingParameter|%s|缺失必需参数。|
|403|Forbidden.NotSupportRAM|%s|暂不支持 RAM 用户执行该操作。|
|400|UnsupportedParameter|%s|不支持参数。|
|403|Forbidden.SubUser|%s|子账号没有授权操作此资源。|
|400|InvalidParameter|%s|参数格式不正确。|
|400|InvalidInstanceID.Malformed|%s|实例 ID 格式不正确。|
|400|InvalidOperation.InvalidEcsState|%s|ECS 实例当前状态不支持释放私网 IP。|
|400|InvalidOperation.InvalidEniState|%s|弹性网卡当前状态不支持释放私网 IP。|
|400|InvalidOperation.DetachPrimaryEniNotAllowed|%s|不允许分离主网卡。|
|404|InvalidEcsId.NotFound|%s|指定的实例ID不存在。|
|404|InvalidEniId.NotFound|%s|指定的网卡ID不存在。|
|404|InvalidVSwitchId.NotFound|%s|指定的交换机ID。|
|404|InvalidSecurityGroupId.NotFound|%s|指定的安全组ID不存在。|
|403|EniPerInstanceLimitExceeded|%s|弹性网卡的数量超过了指定实例类型允许的最大值。|
|403|InvalidOperation.AvailabilityZoneMismatch|%s|指定的VPC交换机ID、弹性网卡和实例ID不在同一个可用区。|
|403|InvalidOperation.VpcMismatch|%s|指定的弹性网卡和安全组ID不在同一个 VPC。|
|403|SecurityGroupInstanceLimitExceed|%s|该安全组内已有的实例数量已超出最大限制。|
|403|InvalidSecurityGroupId.NotVpc|%s|指定的安全组 ID 不是 VPC 类型。|
|403|InvalidOperation.InvalidEniType|%s|当前弹性网卡类型不支持该操作。|
|400|Forbidden.RegionId|%s|前区域暂不支持此功能。|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

