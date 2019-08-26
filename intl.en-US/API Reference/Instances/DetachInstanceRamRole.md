# DetachInstanceRamRole {#doc_api_1161585 .reference}

Detaches a RAM role from one or more ECS instances.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=DetachInstanceRamRole) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|InstanceIds|String|Yes|\["instanceId1", "instanceId2", "instanceId3"…\]| The instance ID set. A maximum of 100 instances can be entered at a time.

 |
|RegionId|String|Yes|cn-hangzhou| The region ID of the instance. You can call the [DescribeRegions](~~25609~~) operation to view the latest region list.

 |
|Action|String|No|DetachInstanceRamRole| The operation that you want to perform. Set the value to DetachInstanceRamRole.

 |
|RamRoleName|String|No|RamRoleTest| The name of the RAM role for the instance. You can call the [ListRoles](~~28713~~) operation to view RAM roles for the specified instance.

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|DetachInstanceRamRoleResults| | | The returned RAM role information. It is an array that consists of DetachInstanceRamRoleResult data.

 |
|└Code|String|200| Indicates whether the RAM role is detached. If 200 is returned, the operation is successful. If other values are returned, the operation fails. For more information, see Error codes.

 |
|└InstanceId|String|i-instance1| The ID of the ECS instance.

 |
|└InstanceRamRoleSets| | | The RAM role set.

 |
|└InstanceId|String|i-instance1| The ID of the instance.

 |
|└RamRoleName|String|RamRoleTest| The name of the RAM role for the instance.

 |
|└Message|String|Success| Indicates whether the RAM role is detached. If Success is returned, the operation is successful. If other values are returned, the operation fails. For more information, see Error codes.

 |
|└Success|Boolean|true| Indicates whether the RAM role is detached.

 |
|FailCount|Integer|0| The number of RAM roles that fail to be detached.

 |
|RamRoleName|String|RamRoleTest| The name of the RAM role.

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The request ID.

 |
|TotalCount|Integer|1| The number of RAM roles detached.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=DetachInstanceRamRole
&InstanceIds=i-instance1
&RegionId=cn-hangzhou 
&RamRoleName=RamRoleTest 
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<DetachInstanceRamRoleResponse>
  <RequestId>E6352369-5C2B-41CD-AB50-471550C8F674</RequestId>
  <DetachInstanceRamRoleResults> 
    <DetachInstanceRamRoleResult>
      <InstanceId>i-instance1</InstanceId>
      <Code>200</Code>
      <Message>success</Message>
    </DetachInstanceRamRoleResult>
  </DetachInstanceRamRoleResults>
  <TotalCount>1</TotalCount> 
  <FailCount>0</FailCount>
  <RamRoleName>RamRoleTest</RamRoleName>
</DetachInstanceRamRoleResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"TotalCount":1,
	"DetachInstanceRamRoleResults":{
		"DetachInstanceRamRoleResult":[
			{
				"Message":"success",
				"InstanceId":"i-instance1",
				"Code":"200"
			}
		]
	},
	"RequestId":"E6352369-5C2B-41CD-AB50-471550C8F674",
	"RamRoleName":"RamRoleTest",
	"FailCount":0
}
```

## Error codes { .section}

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

