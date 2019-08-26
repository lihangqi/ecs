# ModifySecurityGroupAttribute {#doc_api_1031576 .reference}

Modifies the attributes of the specified security group, including the name and description of the security group.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=ModifySecurityGroupAttribute) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|RegionId|String|Yes|cn-hangzhou| The ID of the region where the security group resides. You can call [DescribeRegions](~~25609~~) to view the latest regions of Alibaba Cloud.

 |
|SecurityGroupId|String|Yes|sg-securitygroupid1| The ID of the security group.

 |
|Action|String|No|ModifySecurityGroupAttribute| The operation that you want to perform. Set the value to ModifySecurityGroupAttribute.

 |
|Description|String|No|FinanceDept| The description of the security group. The description must be 2 to 256 characters in length and cannot start with http:// or https://. Default value: null.

 |
|SecurityGroupName|String|No|FinanceJoshua| The name of the security group. It must be 2 to 128 characters in length. It must start with a letter and cannot start with http:// or https://. It can contain letters, digits, colons \(:\), underscores \(\_\), and hyphens \(-\). Default value: null.

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=ModifySecurityGroupAttribute
&SecurityGroupId=sg-F876FF7BA
&RegionId=cn-hangzhou 
&SecurityGroupName=NewName
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<ModifySecurityGroupAttributeResponse>
  <RequestId>CEF72CEB-54B6-4AE8-B225-F876FF7BA984</RequestId> 
</ModifySecurityGroupAttributeResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"CEF72CEB-54B6-4AE8-B225-F876FF7BA984"
}
```

## Error codes {#section_a8m_sfe_eqi .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|404|InvalidSecurityGroupId.NotFound|The specified security group does not exist.|The error message returned when the specified security group does not exist under this account. Check whether the security group ID is correct.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

