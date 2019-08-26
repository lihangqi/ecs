# AssignPrivateIpAddresses {#doc_api_1023028 .reference}

Assigns one or multiple secondary private IP addresses to an ENI. You can specify private IP addresses within the CIDR block of the VSwitch that hosts the ENI. Alternatively, you can specify the number of private IP addresses for ECS to assign them automatically.

## Description {#description .section}

-   The ENI to which you want to assign IP addresses must be in the Available or InUse state.
-   When you perform operations on the primary ENI, the instance to which the ENI is attached must be in the Running or Stopped state.
-   When an ENI is in the Available state, you can assign up to 10 secondary private IP addresses to the ENI. When an ENI is attached to an instance, the number of private IP addresses that can be assigned to the ENI is subject to the instance type. For more information, see [Instance type families](~~25378~~).

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=AssignPrivateIpAddresses) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can call APIs, dynamically generate SDK example code, and quickly retrieve APIs.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|NetworkInterfaceId|String|Yes|eni-myeni| The ID of the ENI.

 |
|RegionId|String|Yes|cn-hangzhou| The ID of the region where the ECS instance resides. You can call [DescribeRegions](~~25609~~) to view the latest regions of Alibaba Cloud.

 |
|Action|String|No|AssignPrivateIpAddresses| The operation that you want to perform. Set the value to AssignPrivateIpAddresses.

 |
|PrivateIpAddress.N|RepeatList|No|172.17. XX.XXX| One or multiple secondary private IP addresses selected from the CIDR block of the VSwitch that hosts the ENI. Valid values of N:

 -   When the ENI is in the Available state: 1 to 10.
-   When the ENI is in the InUse state: limited by the instance type. For more information, see [Instance type families](~~25378~~).

 You must specify either the PrivateIpAddress.N parameter or the SecondaryPrivateIpAddressCount parameter to assign secondary private IP addresses.

 |
|SecondaryPrivateIpAddressCount|Integer|No|1| The specified number of private IP addresses to be assigned by the ECS instance.

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=AssignPrivateIpAddresses
&NetworkInterfaceId=eni-myeni
&RegionId=cn-hangzhou 
&PrivateIpAddress. 1=172.17. XX.XXX
&SecondaryPrivateIpAddressCount=1
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<AssignPrivateIpAddressesResponse>
  <RequestId>04F0F334-1335-436C-A1D7-6C044FE70008</RequestId>
</AssignPrivateIpAddressesResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"04F0F334-1335-436C-A1D7-6C044FE70008"
}
```

## Error codes {#section_lbw_kks_p57 .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|403|InvalidUserType.NotSupported|%s|The error message returned when your account type is not supported.|
|403|Abs.InvalidAccount.NotFound|%s|The error message returned when the specified Alibaba Cloud account does not exist or your AccessKey has expired.|
|403|MissingParameter|%s|The error message returned when a required parameter is not specified.|
|403|Forbidden.NotSupportRAM|%s|The error message returned when RAM users are not allowed to perform this operation.|
|400|UnsupportedParameter|%s|The error message returned when a parameter is not supported.|
|403|Forbidden.SubUser|%s|The error message returned when a RAM user is not authorized to perform operations on this resource.|
|400|InvalidParameter|%s|The error message returned when the parameter format is invalid.|
|400|InvalidInstanceID.Malformed|%s|The error message returned when the instance ID format is invalid.|
|400|InvalidOperation.InvalidEcsState|%s|The error message returned when the private IP address cannot be released under the instance state.|
|400|InvalidOperation.InvalidEniState|%s|The error message returned when the private IP address cannot be released under the ENI state.|
|400|InvalidOperation.DetachPrimaryEniNotAllowed|%s|The error message returned when the primary ENI cannot be detached from its instance.|
|404|InvalidEcsId.NotFound|%s|The error message returned when the specified instance ID does not exist.|
|404|InvalidEniId.NotFound|%s|The error message returned when the specified ENI ID does not exist.|
|404|InvalidVSwitchId.NotFound|%s|The error message returned when the specified VSwitch ID does not exist.|
|404|InvalidSecurityGroupId.NotFound|%s|The error message returned when the specified security group ID does not exist.|
|403|EniPerInstanceLimitExceeded|%s|The error message returned when the number of ENIs exceeds the upper limit for the specified instance type.|
|403|InvalidOperation.AvailabilityZoneMismatch|%s|The error message returned when the specified VSwitch, ENI, and instance do not belong to the same zone.|
|403|InvalidOperation.VpcMismatch|%s|The error message returned when the specified ENI and security group do not belong to the same VPC.|
|403|SecurityGroupInstanceLimitExceed|%s|The error message returned when the number of instances in the specified security group exceeds the upper limit.|
|403|InvalidSecurityGroupId.NotVpc|%s|The error message returned when the specified security group is not VPC-connected.|
|403|InvalidOperation.InvalidEniType|%s|The error message returned when the ENI type is not supported.|
|404|InvalidInstanceId.NotFound|%s|The error message returned when the specified instance does not exist.|
|403|InvalidVSwitchId.IpNotEnough|%s|The error message returned when IP addresses in the specified VSwitch are insufficient.|
|403|InvalidVSwitchId.IpInvalid|%s|The error message returned when the specified private IP address is invalid.|
|403|InvalidIp.IpAssigned|%s|The error message returned when the specified IP address is already assigned.|
|403|Operation.Conflict|%s|The error message returned when operations conflict. You need to try again.|
|400|Forbidden.RegionId|%s|The error message returned when this function is not supported in the region.|
|400|InvalidAction|%s|The error message returned when the operation is invalid.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

