# AttachInstanceRamRole {#doc_api_1161570 .reference}

Attaches a RAM role to one or more ECS instances. You can only attach one RAM role to an instance at any time. If the instance already has a RAM role, an error code is returned when you attach another RAM role to the same instance.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=AttachInstanceRamRole) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|InstanceIds|String|Yes|\[“instanceId1”, “instanceId2”, “instanceId3”…\]| The instance ID set. A maximum of 100 instances can be entered at a time.

 |
|RamRoleName|String|Yes|RamRoleTest| The RAM role name of the instance. You can call the [ListRoles](~~28713~~) operation to view RAM roles for the specified instance.

 |
|RegionId|String|Yes|cn-hangzhou| The region ID of the instance. You can call the [DescribeRegions](~~25609~~) operation to view the latest region list.

 |
|Action|String|No|AttachInstanceRamRole| The operation that you want to perform. Set the value to AttachInstanceRamRole.

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|AttachInstanceRamRoleResults| | | The returned RAM role information. It is an array that consists of AttachInstanceRamRoleResult data.

 |
|└Code|String|200| Indicates whether the RAM role is attached. If 200 is returned, the operation is successful. If other values are returned, the operation fails. For more information, see Error codes.

 |
|└InstanceId|String|i-instanceid1| The ID of the instance.

 |
|└Message|String|Success| Indicates whether the RAM role is attached. If Success is returned, the operation is successful. If other values are returned, the operation fails. For more information, see Error codes.

 |
|└Success|Boolean|true| Indicates whether the RAM role is attached.

 |
|FailCount|Integer|0| The number of RAM roles that fail to be attached.

 |
|RamRoleName|String|RamRoleTest| The name of the RAM role.

 |
|RequestId|String|D9553E4C-6C3A-4D66-AE79-9835AF705639| The request ID.

 |
|TotalCount|Integer|1| The number of RAM roles attached.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=AttachInstanceRamRole
&InstanceIds=["i-instance1"] 
&RamRoleName=RamRoleTest 
&RegionId=cn-hangzhou 
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<AttachInstanceRamRoleResponse>
  <RequestId>E6352369-5C2B-41CD-AB50-471550C8F674</RequestId>
  <AttachInstanceRamRoleResults>
    <AttachInstanceRamRoleResult>
      <InstanceId>i-instance1</InstanceId>
      <Code>200</Code>
      <Message>success</Message>
    </AttachInstanceRamRoleResult>
  </AttachInstanceRamRoleResults>
  <TotalCount>1</TotalCount> 
  <FailCount>0</FailCount>
  <RamRoleName>RamRoleTest</RamRoleName>
</AttachInstanceRamRoleResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"TotalCount":1,
	"RequestId":"D9553E4C-6C3A-4D66-AE79-9835AF705639",
	"AttachInstanceRamRoleResults":{
		"AttachInstanceRamRoleResult":[
			{
				"Message":"success",
				"InstanceId":"i-instance1",
				"Code":"200"
			}
		]
	},
	"RamRoleName":"RamRoleTest",
	"FailCount":0
}
```

## Error codes { .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|404|InvalidRamRole.NotEcsRole|The specified ram role is not authorized for ecs, please check your role policy.|The error message returned when the specified RAM role is not authorized to access ECS.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

