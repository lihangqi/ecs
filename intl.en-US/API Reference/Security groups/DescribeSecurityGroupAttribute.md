# DescribeSecurityGroupAttribute {#doc_api_1031571 .reference}

Views the details of a security group.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=DescribeSecurityGroupAttribute) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|RegionId|String|Yes|cn-hangzhou| The ID of the region to which a security group belongs. You can call [DescribeRegions](~~25609~~) to view the latest regions of Alibaba Cloud.

 |
|SecurityGroupId|String|Yes|sg-securitygroupid1| The ID of the security group.

 |
|Action|String|No|DescribeSecurityGroupAttribute| The operation that you want to perform. Set the value to DescribeSecurityGroupAttribute.

 |
|Direction|String|No|all| The direction in which a security group rule is applied. Valid values:

 -   egress: Outbound traffic is allowed for the security group.
-   ingress: Inbound traffic is allowed for the security group.
-   all: Both inbound and outbound traffic is allowed for the security group.

 Default value: all.

 |
|NicType|String|No|intranet| The NIC type. Valid values:

 -   internet
-   intranet

 Default value: internet.

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|Description|String|FinanceDept| The description of the security group.

 |
|InnerAccessPolicy|String|accept| The access control policy within a security group. Valid values:

 -   accept: All instances within the security group can communicate with each other.
-   drop: All instances within the security group are isolated from each other.

 |
|Permissions| | | The permission rules of the security group.

 |
|└CreateTime|String|2018-12-12T07:28:38Z| The creation time of the security group in UTC.

 |
|└Description|String|FinanceDept| The description of the security group.

 |
|└DestCidrIp|String|0.0.0.0/0| The destination IP address segment for outbound authorization.

 |
|└DestGroupId|String|sg-securitygroupid1| The ID of the destination security group for outbound authorization.

 |
|└DestGroupName|String|SecurityGuard| The name of the destination security group.

 |
|└DestGroupOwnerAccount|String|SecurityGuard| The Alibaba Cloud account that manages the destination security group.

 |
|└Direction|String|ingress| The allowed direction of traffic.

 |
|└IpProtocol|String|TCP| The IP protocol that the security group applies to.

 |
|└Ipv6DestCidrIp|String|2001:db8:1234:1a00::XXX| The destination IPv6 address segment.

 |
|└Ipv6SourceCidrIp|String|2001:db8:1234:1a00::XXX| The source IPv6 address segment.

 |
|└NicType|String|intranet| The network type.

 |
|└Policy|String|Accept| The authorization policy.

 |
|└PortRange|String|80/80| The port number range.

 |
|└Priority|String|1| The rule priority.

 |
|└SourceCidrIp|String|0.0.0.0/0| The source IP address segment for inbound authorization.

 |
|└SourceGroupId|String|sg-securitygroupid2| The source security group for inbound authorization.

 |
|└SourceGroupName|String|FinanceDeptJoshua| The name of the source security group.

 |
|└SourceGroupOwnerAccount|String|FinanceJoshua| The Alibaba Cloud account that manages the source security group.

 |
|└SourcePortRange|String|80/80| The range of the source port.

 |
|RegionId|String|cn-hangzhou| The ID of the region where the security group resides.

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request.

 |
|SecurityGroupId|String|sg-securityid1| The ID of the destination security group.

 |
|SecurityGroupName|String|FinanceJoshua| The name of the destination security group.

 |
|VpcId|String|v-vpcid1| The ID of the VPC to which the security group belongs. If a VPC ID is returned, the network type of the security group is VPC. Otherwise, the network type of the security group is classic.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
http(s)://ecs.aliyuncs.com/?RegionId=cn-hangzhou
&SecurityGroupId=sg-securitygroupid1
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<DescribeSecurityGroupAttributeResponse>
  <SecurityGroupId>sg-bp1gxw6bznjjvhu3gtrz</SecurityGroupId>
  <InnerAccessPolicy>Accept</InnerAccessPolicy>
  <SecurityGroupName>FinanceJoshua</SecurityGroupName>
  <Description>FinanceDept</Description>
  <RegionId>cn-hangzhou</RegionId>
  <RequestId>A72322C1-47C0-491E-8088-8B17E4EA859F</RequestId>
  <Permissions>
    <Permissions>
      <SourceCidrIp>0.0.0.0/0</SourceCidrIp>
      <Description/>
      <DestCidrIp/>
      <NicType>intranet</NicType>
      <DestGroupName/>
      <PortRange>22/22</PortRange>
      <DestGroupId/>
      <Ipv6DestCidrIp/> 
      <Direction>ingress</Direction>
      <Priority>1</Priority>
      <IpProtocol>TCP</IpProtocol>
      <SourcePortRange/>
      <SourceGroupOwnerAccount/>
      <Policy>Accept</Policy>
      <CreateTime>2018-12-12T07:28:38Z</CreateTime>
      <SourceGroupId/>
      <DestGroupOwnerAccount/>
      <Ipv6SourceCidrIp/>
      <SourceGroupName/>
    </Permission>
    <Permission>
      <SourceCidrIp>0.0.0.0/0</SourceCidrIp> 
      <Description/>
      <DestCidrIp/>
      <NicType>intranet</NicType>
      <DestGroupName/>
      <PortRange>443/443</PortRange>
      <DestGroupId/>
      <Ipv6DestCidrIp/> 
      <Direction>ingress</Direction>
      <Priority>1</Priority>
      <IpProtocol>TCP</IpProtocol>
      <SourcePortRange/>
      <SourceGroupOwnerAccount/>
      <Policy>Accept</Policy>
      <CreateTime>2018-12-12T07:28:38Z</CreateTime>
      <SourceGroupId/>
      <DestGroupOwnerAccount/>
      <Ipv6SourceCidrIp/>
      <SourceGroupName/>
    </Permission>
    <Permission>
      <SourceCidrIp>0.0.0.0/0</SourceCidrIp> 
      <Description/>
      <DestCidrIp/>
      <NicType>intranet</NicType>
      <DestGroupName/>
      <PortRange>80/80</PortRange>
      <DestGroupId/>
      <Ipv6DestCidrIp/> 
      <Direction>ingress</Direction>
      <Priority>1</Priority>
      <IpProtocol>TCP</IpProtocol>
      <SourcePortRange/>
      <SourceGroupOwnerAccount/>
      <Policy>Accept</Policy>
      <CreateTime>2018-12-12T07:28:38Z</CreateTime>
      <SourceGroupId/>
      <DestGroupOwnerAccount/>
      <Ipv6SourceCidrIp/>
      <SourceGroupName/>
    </Permission>
    <Permission>
      <SourceCidrIp>0.0.0.0/0</SourceCidrIp>
      <Description/>
      <DestCidrIp/>
      <NicType>intranet</NicType>
      <DestGroupName/>
      <PortRange>-1/-1</PortRange>
      <DestGroupId/>
      <Ipv6DestCidrIp/> 
      <Direction>ingress</Direction>
      <Priority>1</Priority>
      <IpProtocol>ICMP</IpProtocol>
      <SourcePortRange>-1/-1</SourcePortRange>
      <SourceGroupOwnerAccount/>
      <Policy>Accept</Policy>
      <CreateTime>2018-12-12T07:28:38Z</CreateTime>
      <SourceGroupId/>
      <DestGroupOwnerAccount/>
      <Ipv6SourceCidrIp/>
      <SourceGroupName/>
    </Permission>
  </Permissions>
  <VpcId>vpc-bp1opxu1zkhn00gzv26cZ</VpcId>
</DescribeSecurityGroupAttributeResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"SecurityGroupId":"sg-bp1gxw6bznjjvhu3gtrz",
	"Description":"FinanceDept",
	"SecurityGroupName":"FinanceJoshua",
	"InnerAccessPolicy":"Accept",
	"RequestId":"A72322C1-47C0-491E-8088-8B17E4EA859F",
	"RegionId":"cn-hangzhou",
	"Permissions":{
		"Permission":[
			{
				"SourceCidrIp":"0.0.0.0/0",
				"Description":"",
				"DestCidrIp":"",
				"NicType":"intranet",
				"DestGroupName":"",
				"PortRange":"22/22",
				"DestGroupId":"",
				"Ipv6DestCidrIp":"",
				"Direction":"ingress",
				"Priority":1,
				"IpProtocol":"TCP",
				"SourcePortRange":"",
				"SourceGroupOwnerAccount":"",
				"Policy":"Accept",
				"CreateTime":"2018-12-12T07:28:38Z",
				"SourceGroupId":"",
				"DestGroupOwnerAccount":"",
				"Ipv6SourceCidrIp":"",
				"SourceGroupName":""
			},
			{
				"SourceCidrIp":"0.0.0.0/0",
				"Description":"",
				"DestCidrIp":"",
				"NicType":"intranet",
				"DestGroupName":"",
				"PortRange":"443/443",
				"DestGroupId":"",
				"Ipv6DestCidrIp":"",
				"Direction":"ingress",
				"Priority":1,
				"IpProtocol":"TCP",
				"SourcePortRange":"",
				"SourceGroupOwnerAccount":"",
				"Policy":"Accept",
				"CreateTime":"2018-12-12T07:28:38Z",
				"SourceGroupId":"",
				"DestGroupOwnerAccount":"",
				"Ipv6SourceCidrIp":"",
				"SourceGroupName":""
			},
			{
				"SourceCidrIp":"0.0.0.0/0",
				"Description":"",
				"DestCidrIp":"",
				"NicType":"intranet",
				"DestGroupName":"",
				"PortRange":"80/80",
				"DestGroupId":"",
				"Ipv6DestCidrIp":"",
				"Direction":"ingress",
				"Priority":1,
				"IpProtocol":"TCP",
				"SourcePortRange":"",
				"SourceGroupOwnerAccount":"",
				"Policy":"Accept",
				"CreateTime":"2018-12-12T07:28:38Z",
				"SourceGroupId":"",
				"DestGroupOwnerAccount":"",
				"Ipv6SourceCidrIp":"",
				"SourceGroupName":""
			},
			{
				"SourceCidrIp":"0.0.0.0/0",
				"Description":"",
				"DestCidrIp":"",
				"NicType":"intranet",
				"DestGroupName":"",
				"PortRange":"-1/-1",
				"DestGroupId":"",
				"Ipv6DestCidrIp":"",
				"Direction":"ingress",
				"Priority":1,
				"IpProtocol":"ICMP",
				"SourcePortRange":"-1/-1",
				"SourceGroupOwnerAccount":"",
				"Policy":"Accept",
				"CreateTime":"2018-12-12T07:28:38Z",
				"SourceGroupId":"",
				"DestGroupOwnerAccount":"",
				"Ipv6SourceCidrIp":"",
				"SourceGroupName":""
			}
		]
	},
	"VpcId":"vpc-bp1opxu1zkhn00gzv26cZ"
}
```

## Error codes {#section_1kf_414_bee .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|404|InvalidRegionId.NotFound|The specified RegionId does not exist.|The error message returned when the specified region ID does not exist. Check whether the service is applicable in this region.|
|404|InvalidSecurityGroupId.NotFound|The specified SecurityGroupId does not exist.|The error message returned when the specified security group does not exist under this account. Check whether the security group ID is correct.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

