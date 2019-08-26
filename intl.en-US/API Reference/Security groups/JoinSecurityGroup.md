# JoinSecurityGroup {#doc_api_1031574 .reference}

Adds an instance to a specified security group.

## Description {#description .section}

When you call this operation, note that:

-   Before you add an instance to a security group, the instance must be in the Stopped or Running state.
-   An instance can belong to a maximum of five security groups.
-   You can [submit a ticket](https://workorder-intl.console.aliyun.com/#/ticket/createIndex) to add the instance to more security groups. An instance can belong to a maximum of 16 security groups.
-   A security group can manage up to 1,000 instances.
-   The specified security group and instance must belong to the same region.
-   The specified security group and instance must have the same network type. If the network type is [VPC](~~34217~~), the security group and the instance must be in the same VPC.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=JoinSecurityGroup) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|InstanceId|String|Yes|i-instanceid1| The ID of an instance. You can call [DescribeRegions](~~25609~~) to view the latest regions of Alibaba Cloud.

 |
|SecurityGroupId|String|Yes|sg-securitygroupid1| The ID of the security group to which the instance belongs. You can call [DescribeSecurityGroups](~~25556~~) to view the available security groups.

 |
|Action|String|No|JoinSecurityGroup| The operation that you want to perform. Set the value to JoinSecurityGroup.

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=JoinSecurityGroup
&InstanceId=i-instance1
&SecurityGroupId=F876FF7BA984 
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<JoinSecurityGroupResponse>
  <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</JoinSecurityGroupResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E"
}
```

## Error codes {#section_397_qzn_gqu .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|404|InvalidSecurityGroupId.NotFound|The specified SecurityGroupId does not exist.|The error message returned when the specified security group does not exist under this account. Check whether the security group ID is correct.|
|400|InstanceSecurityGroupLimitExceeded|Exceeding the allowed amount of security groups that an instance can be in.|The error message returned when the number of security groups for an instance reaches the upper limit.|
|403|IncorrectInstanceStatus|The current status of the resource does not support this operation.|The error message returned when this operation is not supported under the current instance state.|
|403|SecurityGroupInstanceLimitExceeded|The maximum number of instances in a security group is exceeded.|The error message returned when the number of instances in a security group reaches the upper limit.|
|403|InvalidInstanceId.AlreadyExists|The specified instance already exists in the specified security group.|The error message returned when the specified instance already exists in the security group.|
|403|SecurityGroupInstanceLimitExceeded|%s|The error message returned when the number of instances in a security group reaches the upper limit.|
|403|AclLimitExceed|%s|The error message returned when the value of AccessPoint exceeds the upper limit.|
|403|InstanceSecurityGroupLimitExceeded|%s|The error message returned when the number of security groups for an instance reaches the upper limit.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

