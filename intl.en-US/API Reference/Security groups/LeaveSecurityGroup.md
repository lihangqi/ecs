# LeaveSecurityGroup {#doc_api_1031575 .reference}

Removes an instance from a specified security group.

## Description {#description .section}

When you call this operation, note that:

-   Before you remove an instance from a security group, the instance must be in the Stopped or Running state.
-   An instance must belong to at least one security group. You cannot perform the LeaveSecurityGroup operation to remove an instance from the only security group it belongs to.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=LeaveSecurityGroup) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|InstanceId|String|Yes|i-instanceid1| The ID of an instance.

 |
|SecurityGroupId|String|Yes|sg-securitygroupid1| The ID of the security group to which the instance belongs.

 |
|Action|String|No|LeaveSecurityGroup| The operation that you want to perform. Set the value to LeaveSecurityGroup.

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=LeaveSecurityGroup
&InstanceId=i-instance1
&SecurityGroupId=F876FF7BA984 
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<LeaveSecurityGroupResponse>
   <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</LeaveSecurityGroupResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E"
}
```

## Error codes {#section_mvj_6jr_tvi .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|404|InvalidSecurityGroupId.NotFound|The specified SecurityGroupId does not exist.|The error message returned when the specified security group does not exist under this account. Check whether the security group ID is correct.|
|403|IncorrectInstanceStatus|The current status of the resource does not support this operation.|The error message returned when this operation is not supported under the current instance state.|
|504|RequestTimeout|The request encounters an upstream server timeout.|The error message returned when the request encounters an upstream server timeout.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

