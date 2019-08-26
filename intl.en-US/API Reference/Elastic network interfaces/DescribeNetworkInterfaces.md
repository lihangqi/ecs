# DescribeNetworkInterfaces {#doc_api_1006040 .reference}

You can call this operation to query ENIs.

## Description {#description .section}

-   You can specify attribute values to filter the results.
-   If no attribute values are specified, all ENIs are returned.
-   You can query a maximum of 100 ENIs at a time.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=DescribeNetworkInterfaces) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can call APIs, dynamically generate SDK example code, and quickly retrieve APIs.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|RegionId|String|Yes|cn-hangzhou| The ID of the region where the ECS instance resides. You can call [DescribeRegions](~~25609~~) to view the latest regions of Alibaba Cloud.

 |
|Action|String|No|DescribeNetworkInterfaces| The operation that you want to perform. Set the value to DescribeNetworkInterfaces.

 |
|InstanceId|String|No|AY121018033933eaxxxxx| The ID of the instance to which an ENI is attached.

 |
|NetworkInterfaceId.N|RepeatList|No|eni-bp17pdijfczaxZZZZxxxxx| The ID of the ENI. You can query a maximum of 100 ENIs at a time.

 |
|NetworkInterfaceName|String|No|my-eni-name| The name of an ENI.

 |
|PageNumber|Integer|No|1| The page number of the query result. The parameter value is a positive integer.

 Default value: 1.

 |
|PageSize|Integer|No|100| The number of entries on each page. Valid values: 1 to 100.

 Default value: 10.

 |
|PrimaryIpAddress|String|No|172.17. XX.XXX| The private IP address of the primary ENI.

 |
|ResourceGroupId|String|No|rg-resourcegroupid1| The ID of the resource group.

 |
|SecurityGroupId|String|No|sg-bp144yr32sx6ndwxxxxx| The ID of the security group.

 |
|Tag.N.Key|String|No|test| The tag key of an ENI. Valid values of N: 1 to 20. It cannot be a null string. It can be a maximum of 64 characters in length. It cannot start with aliyun or acs:. It cannot contain http:// or https://.It cannot start with aliyun or acs:. It cannot contain http:// or https://.

 |
|Tag.N.Value|String|No|api| The tag value of an ENI. Valid values of N: 1 to 20. It can be a null string. It can be a maximum of 128 characters in length. It cannot start with aliyun or acs:. It cannot contain http:// or https://.It cannot start with aliyun or acs:. It cannot contain http:// or https://.

 |
|Type|String|No|Secondary| The type of an ENI. Valid values:

 -   Primary
-   Secondary

 |
|VSwitchId|String|No|vsw-bp16usj2p27htro3xxxxx| The ID of the VSwitch associated with the ENIs to be queried.

 |
|VpcId|String|No|vsw-bp16usj2p27htro3xxxxx| The ID of the VPC to which an ENI belongs.

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|NetworkInterfaceSets| | | A set of ENIs.

 |
|└AssociatedPublicIp| | | The public IP address associated with the secondary private IP address of an ENI.

 |
|└AllocationId|String|eip-2ze88m67qx5zxxxxx| The ID of an EIP.

 |
|└PublicIpAddress|String|116.62.129.250| The public IP address of the instance.

 |
|└CreationTime|String|2017-11-24T06:14:22Z| The creation time of the instance.

 |
|└Description|String|test1| Description

 |
|└InstanceId|String|AY121018033933eaxxxxx| The ID of the instance.

 |
|└Ipv6Sets| | | A set of IPv6 addresses assigned to an ENI.

 |
|└Ipv6Address|String|2001:db8:1234:1a00::XXX| The IPv6 address assigned to an ENI.

 |
|└MacAddress|String|00:16:3e:0f:XX:XX| The MAC address of an ENI.

 |
|└NetworkInterfaceId|String|eni-bp17pdijfczaxZZZZxxxxx| The ID of an ENI.

 |
|└NetworkInterfaceName|String|my-eni-name| The name of an ENI.

 |
|└PrivateIpAddress|String|172.17. XX.XXX"| The private IP address of the instance.

 |
|└PrivateIpSets| | | A set of private IP addresses.

 |
|└AssociatedPublicIp| | | The public IP address associated with an ENI.

 |
|└AllocationId|String|eip-2ze88m67qx5zxxxxx| The ID of an EIP.

 |
|└PublicIpAddress|String|116.62.129.250| The public IP address of the instance.

 |
|└Primary|Boolean|true| Indicates whether the IP address is primary.

 |
|└PrivateIpAddress|String|172.17. XX.XXX| The private IP address of the instance.

 |
|└ResourceGroupId|String|rg-resourcegroupid1| The ID of the resource group.

 |
|└SecurityGroupIds| |sg-bp144yr32sx6ndwxxxxx| The IDs of security groups to which the specified ENIs belong.

 |
|└Status|String|Available| The status of an ENI.

 |
|└Tags| | | The tag of an ENI.

 |
|└TagKey|String|test| The tag key of an ENI.

 |
|└TagValue|String|api| The tag value of an ENI.

 |
|└Type|String|Secondary| The type of an ENI.

 |
|└VSwitchId|String|vsw-bp16usj2p27htro3xxxxx| The ID of the VSwitch associated with the ENIs to be queried.

 |
|└VpcId|String|vpc-bp1j7w3gc1cexjqdxxxxx| The ID of the VPC to which an ENI belongs.

 |
|└ZoneId|String|cn-hangzhou-e| The ID of the zone in which an ENI resides.

 |
|PageNumber|Integer|1| The page number that you query in the instance list.

 |
|PageSize|Integer|100| The number of entries per page.

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request.

 |
|TotalCount|Integer|1| The total number of instances.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=DescribeNetworkInterfaces
&RegionId=cn-hangzhou 
&Tag.1.Key=test
&Tag.1.Value=api
&ResourceGroupId=rg-resourcegroupid1
&VSwitchId=vsw-bp16usj2p27htro3xxxxx
&VpcId=vsw-bp16usj2p27htro3xxxxx
&PrimaryIpAddress=172.17. XX.XXX
&SecurityGroupId=sg-bp144yr32sx6ndwxxxxx
&NetworkInterfaceName=my-eni-name
&Type=Secondary
&InstanceId=AY121018033933eaxxxxx
&NetworkInterfaceId. 1=eni-bp17pdijfczaxZZZZxxxxx
&PageNumber=1
&PageSize=100
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<DescribeNetworkInterfacesResponse>
  <NetworkInterfaceSets> 
    <NetworkInterfaceSet> 
      <AssociatedPublicIp/> 
      <CreationTime>2017-11-24T06:14:22Z</CreationTime> 
      <InstanceId>AY121018033933eaxxxxx</InstanceId> 
      <MacAddress>00:16:3e:0f:XX:XX</MacAddress> 
      <NetworkInterfaceId>eni-bp17pdijfczaxZZZZxxxxx</NetworkInterfaceId> 
      <PrivateIpAddress>XXX.XXX.XX.XX</PrivateIpAddress> 
      <PrivateIpSets>
        <PrivateIpSet>
          <AssociatedPublicIp/> 
          <Primary>true</Primary> 
          <PrivateIpAddress>XXX.XXX.XX.XX</PrivateIpAddress> 
        </PrivateIpSet>
      </PrivateIpSets> 
      <SecurityGroupIds> 
        <SecurityGroupId>sg-bp144yr32sx6ndwxxxxx</SecurityGroupId> 
      </SecurityGroupIds>
      <Status>Available</Status> 
      <Type>Secondary</Type> 
      <VpcId>vpc-bp1j7w3gc1cexjqdxxxxx</VpcId> 
      <VSwitchId>vsw-bp16usj2p27htro3xxxxx</VSwitchId> 
      <ZoneId>cn-hangzhou-e</ZoneId> 
    </NetworkInterfaceSet> 
  </NetworkInterfaceSets>
  <PageNumber>1</PageNumber> 
  <PageSize>100</PageSize> 
  <RequestId>CEE5C347-0B64-4535-A061-95BE95Axxxxx</RequestId> 
  <TotalCount>1</TotalCount> 
</DescribeNetworkInterfacesResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"PageNumber":1,
	"TotalCount":1,
	"PageSize":100,
	"RequestId":"CEE5C347-0B64-4535-A061-95BE95Axxxxx",
	"NetworkInterfaceSets":{
		"NetworkInterfaceSet":[
			{
				"Type":"Secondary",
				"InstanceId":"AY121018033933eaxxxxx",
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
				"VSwitchId":"vsw-bp16usj2p27htro3xxxxx",
				"VpcId":"vpc-bp1j7w3gc1cexjqdxxxxx",
				"AssociatedPublicIp":{},
				"NetworkInterfaceId":"eni-bp17pdijfczaxZZZZxxxxx",
				"CreationTime":"2017-11-24T06:14:22Z",
				"Status":"Available",
				"MacAddress":"00:16:3e:0f:XX:XX",
				"SecurityGroupIds":{
					"SecurityGroupId":[
						"sg-bp144yr32sx6ndwxxxxx"
					]
				},
				"PrivateIpAddress":"XXX.XXX.XX.XX"
			}
		]
	}
}
```

## Error codes {#section_hd8_k41_zbn .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|403|InvalidUserType.NotSupported|%s|The error message returned when your account type is not supported.|
|403|Abs.InvalidAccount.NotFound|%s|The error message returned when the specified Alibaba Cloud account does not exist or your AccessKey has expired.|
|400|MissingParameter|%s|The error message returned when a required parameter is not specified.|
|403|Forbidden.NotSupportRAM|%s|The error message returned when RAM users are not allowed to perform this operation.|
|400|UnsupportedParameter|%s|The error message returned when a parameter is not supported.|
|403|Forbidden.SubUser|%s|The error message returned when a RAM user is not authorized to perform operations on this resource.|
|400|InvalidParameter|%s|The error message returned when the parameter format is invalid.|
|400|InvalidInstanceID.Malformed|%s|The error message returned when the instance ID format is invalid.|
|400|InvalidOperation.InvalidEcsState|%s|The error message returned when the private IP address cannot be released under the instance state.|
|400|InvalidOperation.InvalidEniState|%s|The error message returned when the private IP address cannot be released under the ENI state.|
|400|InvalidOperation.DetachPrimaryEniNotAllowed|%s|The error message returned when the primary ENI cannot be detached from the instance.|
|404|InvalidEcsId.NotFound|%s|The error message returned when the specified instance ID does not exist.|
|404|InvalidEniId.NotFound|%s|The error message returned when the specified ENI ID does not exist.|
|404|InvalidVSwitchId.NotFound|%s|The error message returned when the specified VSwitch ID does not exist.|
|404|InvalidSecurityGroupId.NotFound|%s|The error message returned when the specified security group ID does not exist.|
|403|EniPerInstanceLimitExceeded|%s|The error message returned when the number of ENIs exceeds the upper limit for the specified instance type.|
|403|InvalidOperation.AvailabilityZoneMismatch|%s|The error message returned when the specified VSwitch, ENI, and instance are not in the same zone.|
|403|InvalidOperation.VpcMismatch|%s|The error message returned when the specified ENI and security group do not belong to the same VPC.|
|403|SecurityGroupInstanceLimitExceed|%s|The error message returned when the number of instances in the specified security group exceeds the upper limit.|
|403|InvalidSecurityGroupId.NotVpc|%s|The error message returned when the specified security group is not VPC-connected.|
|403|InvalidOperation.InvalidEniType|%s|The error message returned when the ENI type is not supported.|
|400|Forbidden.RegionId|%s|The error message returned when this operation is not supported in the region.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

