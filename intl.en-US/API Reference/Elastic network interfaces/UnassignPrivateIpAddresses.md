# UnassignPrivateIpAddresses {#doc_api_1023027 .reference}

Deletes one or multiple secondary private IP addresses from an ENI.

## Description {#description .section}

-   The ENI must be in the Available or InUse state.
-   When you perform operations on the primary ENI, the instance to which the ENI is attached must be in the Running or Stopped state.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=UnassignPrivateIpAddresses) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can call APIs, dynamically generate SDK example code, and quickly retrieve APIs.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|NetworkInterfaceId|String|Yes|eni-myeni| The ID of the ENI.

 |
|PrivateIpAddress.N|RepeatList|Yes|192.168.0.1| The secondary private IP addresses to be deleted. Valid values of N:

 -   When the ENI is in the Available state: 1 to 10.
-   When the ENI is in the InUse state: subject to the instance type.

 |
|RegionId|String|Yes|cn-hangzhou| The ID of the region where the ECS instance resides. You can call [DescribeRegions](~~25609~~) to view the latest regions of Alibaba Cloud.

 |
|Action|String|No|UnassignPrivateIpAddresses| The operation that you want to perform. Set the value to UnassignPrivateIpAddresses.

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=UnassignPrivateIpAddresses
&NetworkInterfaceId=eni-myeni
&PrivateIpAddress.1=192.168.0.1
&RegionId=cn-hangzhou 
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<UnassignPrivateIpAddressesResponse>
  <RequestId>04F0F334-1335-436C-A1D7-6C044FE70008</RequestId>
</UnassignPrivateIpAddressesResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"04F0F334-1335-436C-A1D7-6C044FE70008"
}
```

## Error codes {#section_0zq_v0b_1v9 .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|403|InvalidUserType.NotSupported|%s|The error message returned when your account type is not supported.|
|403|Abs.InvalidAccount.NotFound|%s|The error message returned when the specified Alibaba Cloud account does not exist or your AccessKey has expired.|
|403|MissingParameter|%s|The error message returned when a required parameter is not specified.|
|403|Forbidden.NotSupportRAM|%s|The error message returned when RAM users are not allowed to perform this operation.|
|400|UnsupportedParameter|%s|The error message returned when a parameter is not supported.|
|403|Forbidden.SubUser|%s|The error message returned when a RAM user is not authorized to perform operations on this resource.|
|400|InvalidParameter|%s|The error message returned when the parameter format is invalid.|
|400|InvalidInstanceId.MalFormed|%s|The error message returned when the instance ID format is invalid.|
|400|InvalidOperation.InvalidEcsState|%s|The error message returned when the private IP address cannot be released under the instance state.|
|400|InvalidOperation.InvalidEniState|%s|The error message returned when the private IP address cannot be released under the ENI state.|
|400|InvalidOperation.DetachPrimaryEniNotAllowed|%s|The error message returned when the primary ENI cannot be detached from its instance.|
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
|404|InvalidInstanceId.NotFound|%s|The error message returned when the specified instance does not exist.|
|403|InvalidVSwitchId.IpInvalid|%s|The error message returned when the specified private IP address is invalid.|
|403|InvalidIp.IpUnassigned|%s|The error message returned when the specified IP address is not assigned.|
|403|Operation.Conflict|%s|The error message returned when operations conflict. You need to try again.|
|400|Forbidden.RegionId|%s|The error message returned when this function is not supported in the region.|
|400|InvalidAction|%s|The error message returned when the operation is invalid.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

