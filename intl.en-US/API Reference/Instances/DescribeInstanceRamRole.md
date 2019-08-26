# DescribeInstanceRamRole {#doc_api_1161572 .reference}

You can call this operation to query RAM roles attached to one or more ECS instances.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=DescribeInstanceRamRole) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|RegionId|String|Yes|cn-hangzhou| The region ID of the RAM role. You can call the [DescribeRegions](~~25609~~) operation to view the latest region list.

 |
|Action|String|No|DescribeInstanceRamRole| The operation that you want to perform. Set the value to **DescribeInstanceRamRole**.

 |
|InstanceIds|String|No|\["instanceId1", "instanceId2", "instanceId3"…\]| The instance ID set. A maximum of 100 instances can be entered at a time.

 |
|PageNumber|Integer|No|1| The page number.

 This value starts from 1.

 Default value: 1.

 |
|PageSize|Integer|No|10| The number of rows per page.

 Maximum value: 50.

 Default value: 10.

 |
|RamRoleName|String|No|FinanceDeptOnly| All ECS instances to which the specified RAM role is attached. You can call the [ListRoles](~~28713~~) operation to view RAM roles for the specified instance.

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|InstanceRamRoleSets| | | The returned RAM role information. It is an array that consists of **InstanceRamRoleSetType** data.

 |
|└InstanceId|String|i-instance1| The ID of the instance.

 |
|└RamRoleName|String|FinanceDeptOnly| The list of RAM role names.

 |
|RegionId|String|cn-hangzhou| The region ID of the RAM role. You can call the [DescribeRegions](~~25609~~) operation to view the latest region list.

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The request ID.

 |
|TotalCount|Integer|1| The total number of RAM roles.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

https://ecs.aliyuncs.com/?Action=DescribeInstanceRamRole
&RegionId=cn-hangzhou 
&InstanceIds=["i-instance1"] 
&PageNumber=1 
&PageSize=10 
&RamRoleName=FinanceDeptOnly
&<Common request parameters>

```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<DescribeInstanceRamRoleResponse>
  <RequestId>8F4CAE3F-7892-4662-83A5-2C2FFD639553</RequestId>
  <InstanceRamRoleSets>
    <InstanceRamRoleSet>
      <InstanceId>i-instance1</InstanceId>
      <RamRoleName>RamRoleTest</RamRoleName>
    </InstanceRamRoleSet>
  </InstanceRamRoleSets>
  <TotalCount>1</TotalCount> 
</DescribeInstanceRamRoleResponse>

```

`JSON` format

``` {#json_return_success_demo}
{
	"TotalCount":1,
	"RequestId":"8F4CAE3F-7892-4662-83A5-2C2FFD639553",
	"InstanceRamRoleSets":{
		"InstanceRamRoleSet":[
			{
				"InstanceId":"i-instance1",
				"RamRoleName":"RamRoleTest"
			}
		]
	}
}
```

## Error codes {#section_gk8_cnm_4a9 .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|403|InvalidParameter.AllEmpty|%s|The error message returned when a required parameter is not specified.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

