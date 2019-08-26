# AttachNetworkInterface {#doc_api_1000118 .reference}

Attaches an ENI to a VPC-connected instance.

## Description {#description .section}

-   The ENI must be in the Available state.
-   The instance must be in the Running or Stopped state.
-   An ENI can only be attached to a VPC-connected ECS instance, and the ENI must belong to the same VPC as the ECS instance.
-   One ENI can only be attached to one instance.
-   An instance can be attached with multiple ENIs. For more information about the maximum number of ENIs that can be attached to each instance type, see [Elastic network Interface](~~58496~~).
-   Because a VSwitch of a VPC can only be located in a single zone, ensure that the ECS instance to be attached to an ENI is in the same zone as the VSwitch that hosts the ENI.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=AttachNetworkInterface) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can call APIs, dynamically generate SDK example code, and quickly retrieve APIs.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|InstanceId|String|Yes|i-myInstance| The ID of the instance.

 |
|NetworkInterfaceId|String|Yes|\[networkInterfaceId\]| The ID of the ENI.

 |
|RegionId|String|Yes|cn-hangzhou| The ID of the region where the ECS instance resides. You can call [DescribeRegions](~~25609~~) to view the latest regions of Alibaba Cloud.

 |
|Action|String|No|AttachNetworkInterface| The operation that you want to perform. Set the value to AttachNetworkInterface.

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=AttachNetworkInterface
&InstanceId=i-myInstance
&NetworkInterfaceId=[networkInterfaceId]
&RegionId=cn-hangzhou 
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<AttachNetworkInterfaceResponse>
  <RequestId>04F0F334-1335-436C-A1D7-6C044FExxxxx</RequestId>
</AttachNetworkInterfaceResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"04F0F334-1335-436C-A1D7-6C044FExxxxx"
}
```

## Error codes {#section_zug_v14_m2g .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|403|InvalidUserType.NotSupported|%s|The error message returned when your account type is not supported.|
|403|Abs.InvalidAccount.NotFound|%s|The error message returned when the specified Alibaba Cloud account does not exist or your AccessKey has expired.|
|400|MissingParameter|%s|The error message returned when a required parameter is not specified.|
|403|Forbidden.NotSupportRAM|%s|The error message returned when RAM users are not allowed to perform this operation.|
|400|UnsupportedParameter|%s|The error message returned when a parameter is not supported.|
|403|Forbidden.SubUser|%s|The error message returned when a RAM user is unauthorized to perform operations on this resource.|
|400|InvalidParameter|%s|The error message returned when the parameter format is invalid.|
|400|InvalidInstanceId.MalFormed|%s|The error message returned when the instance ID format is invalid.|
|400|InvalidOperation.InvalidRegion|%s|The error message returned when the specified region ID is invalid.|
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
|400|Forbidden.RegionId|%s|The error message returned when this function is not supported in the region.|
|403|InvalidInstanceId.NotFound|%s|The error message returned when the specified instance does not exist.|
|400|InvalidOperation.InvalidGeneration|%s|The error message returned when the instance type is not supported.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

