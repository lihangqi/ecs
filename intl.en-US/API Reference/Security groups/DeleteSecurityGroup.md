# DeleteSecurityGroup {#doc_api_1031564 .reference}

Deletes a security group. Before deleting a security group, make sure that no instance exists in the security group and that the security group is not referenced by other security groups. Otherwise, the DeleteSecurityGroup request fails.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=DeleteSecurityGroup) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|RegionId|String|Yes|cn-hangzhou| The ID of the region where a security group resides. You can call [DescribeRegions](~~25609~~) to view the latest regions of Alibaba Cloud.

 |
|SecurityGroupId|String|Yes|sg-securitygroupid1| The ID of the security group.

 |
|Action|String|No|DeleteSecurityGroup| The operation that you want to perform. Set the value to DeleteSecurityGroup.

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
 https://ecs.aliyuncs.com/?Action=DeleteSecurityGroup
&RegionId=cn-hangzhou
&SecurityGroupId=sg-F876FF7BA
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<DeleteSecurityGroupResponse>
  <RequestId>CEF72CEB-54B6-4AE8-B225-F876FF7BA984</RequestId>
</DeleteSecurityGroupResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"CEF72CEB-54B6-4AE8-B225-F876FF7BA984"
}
```

## Error codes {#section_z6k_io3_mpk .section}

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

