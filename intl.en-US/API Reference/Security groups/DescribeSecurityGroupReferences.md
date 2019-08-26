# DescribeSecurityGroupReferences {#doc_api_1031572 .reference}

Queries whether a specified security group has been authorized by other security groups.

## Description {#description .section}

When you call this operation, note that:

-   Security group authorization includes authorization for inbound and outbound traffic rules.
-   Each query returns a maximum of 100 records.
-   When you fail to delete a security group \([DeleteSecurityGroup](~~25558~~)\), you can call this operation to determine whether the specified security group has been authorized by other security groups. If the security group to be deleted is authorized by another security group, you need to revoke its authorization before it can be deleted.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=DescribeSecurityGroupReferences) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|RegionId|String|Yes|cn-hangzhou| The ID of the region where the security group resides.

 |
|SecurityGroupId.N|RepeatList|Yes|sg-securitygroupid1| The ID of the security group that you want to query. Valid values of N: 1 to 10.

 |
|Action|String|No|DescribeSecurityGroupReferences| The operation that you want to perform. Set the value to DescribeSecurityGroupReferences.

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request.

 |
|SecurityGroupReferences| | | The information about references between security groups.

 |
|└ReferencingSecurityGroups| | | The information of other security groups referencing this security group.

 |
|└AliUid|String|155780923770| The ID of an Alibaba Cloud user to whom the security group belongs.

 |
|└SecurityGroupId|String|sg-securitygroupid1| The ID of the security group.

 |
|└SecurityGroupId|String|sg-securitygroupid2| The ID of the security group that you want to query.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=DescribeSecurityGroupReferences
&RegionId=cn-hangzhou 
&SecurityGroupId. 1=sg-1133aa
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<DescribeSecurityGroupReferencesResponse>
  <RequestId>CEF72CEB-54B6-4AE8-B225-F876FF7BA984</RequestId> 
  <SecurityGroupReferences>
    <SecurityGroupReference>
      <SecurityGroupId>sg-1133aa</SecurityGroupId>
      <ReferencingSecurityGroups>
        <ReferencingSecurityGroup>
          <SecurityGroupId>sg-2255cc</SecurityGroupId>
          <AliUid>123</AliUid>
        </ReferencingSecurityGroup>
        <ReferencingSecurityGroup>
          <SecurityGroupId>sg-2255dd</SecurityGroupId>
          <AliUid>123</AliUid>
        </ReferencingSecurityGroup>
      </ReferencingSecurityGroups>
    </SecurityGroupReference>
  </SecurityGroupReferences>
</DescribeSecurityGroupReferencesResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"CEF72CEB-54B6-4AE8-B225-F876FF7BA984",
	"SecurityGroupReferences":[
		{
			"SecurityReferencingGroups":[
				{
					 "SecurityGroupId":"sg-2255cc",
					"AliUid":123
				},
				{
					"SecurityGroupId":"sg-2255dd",
					"AliUid":123
				}
			],
			"SecurityGroupId":"sg-1133aa"
		}
	]
}
```

## Error codes {#section_xae_3qb_k5n .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|400|InvalidSecurityGroupId.Malformed|The specified parameter SecurityGroupId is essential and size should less than 10|The error message returned when the security group ID is invalid.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

