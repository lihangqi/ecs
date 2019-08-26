# CreateSecurityGroup {#doc_api_Ecs_CreateSecurityGroup .reference}

You can call the CreateSecurityGroup action to create a security group. Only instances within the security group are granted access permissions by default. If you want to allow requests from the Internet or requests from instances in other security groups, you can call AuthorizeSecurityGroup to grant access permissions to these instances or groups.

## Description {#description .section}

When you call this operation, note that:

-   You can create up to 100 security groups in a region.
-   VpcId must be specified when you create a VPC-type security group.

## Debugging {#apiExplorer .section}

Alibaba Cloud provides [OpenAPI Explorer](https://api.aliyun.com/#product=Ecs&api=CreateSecurityGroup) to simplify API usage. You can use OpenAPI Explorer to search for APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|RegionId|String|Yes|cn-hangzhou-b| The region ID of the security group. You can call the [DescribeRegions](~~25609~~) operation to query the latest region list.

 |
|Action|String|No|CreateSecurityGroup| The operation that you want to perform. Set this value to CreateSecurityGroup.

 |
|ClientToken|String|No|123e4567-e89b-12d3-a456-426655440000| The client token that is used to ensure the idempotence of the request. You can use the client to generate this value, but you must ensure that it is unique among different requests.**ClientToken** can contain only ASCII characters, and cannot exceed 64 characters in length. For more information, see [How to ensure idempotence](~~25693~~).

 |
|Description|String|No|FinanceDept| The description of the security group. It must be 2 to 256 characters in length and cannot start with http:// or https://. Default value: null

 |
|ResourceGroupId|String|No|rg-resourcegrouid| The ID of the resource group to which the security group belongs.

 |
|SecurityGroupName|String|No|FinanceJoshua| The name of the security group. It must be 2 to 128 characters in length. It must start with a letter but cannot start with http:// or https://. It can contain letters, digits, colons \(:\), underscores \(\_\), and hyphens \(-\). Default value: null

 |
|SecurityGroupType|String|No|enterprise| The type of the security group. Valid values:

 -   normal: basic security group
-   enterprise: advanced security group For more information, see [Advanced security group overview](~~120621~~).

 |
|Tag.N.Key|String|No|FinanceDept| The tag key of the security group. Valid values of N: 1 to 20. The tag key cannot be an empty string. It can be up to 64 characters in length and cannot start with aliyun or acs:. It cannot contain http:// or https://.

 |
|Tag.N.Value|String|No|FinanceDeptJoshua| The tag value of the security group. Valid values of N: 1 to 20. The tag value can be an empty string. It can be up to 128 characters in length and cannot start with aliyun or acs:. It cannot contain http:// or https://.

 |
|Tag.N.key|String|No|FinanceDept| The tag key of the security group.

 **Note:** This parameter will be removed in the future. We recommend that you use Tag.N.Key to ensure future compatibility.

 |
|Tag.N.value|String|No|FinanceDeptJoshua| The tag value of the security group.

 **Note:** This parameter will be removed in the future. We recommend that you use Tag.N.Value to ensure future compatibility.

 |
|VpcId|String|No|vpc-vpcid1| The ID of the VPC to which the security group belongs.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request.

 |
|SecurityGroupId|String|sg-F876FF7BA| The ID of the security group.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=CreateSecurityGroup
&RegionId=cn-hangzhou
&Description=for_demo
&<Common request parameters>
```

Sample success responses

`XML` format

``` {#xml_return_success_demo}
<CreateSecurityGroupResponse>
  <RequestId>CEF72CEB-54B6-4AE8-B225-F876FF7BA984</RequestId>
  <SecurityGroupId>sg-securitygroupid</SecurityGroupId>
</CreateSecurityGroupResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"SecurityGroupId":"sg-securitygroupid",
	"RequestId":"CEF72CEB-54B6-4AE8-B225-F876FF7BA984"
}
```

## Error codes {#section_nau_zx9_o06 .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|400|InvalidDescription.Malformed|The specified parameter "Description" is not valid.|The error message returned because the specified description is invalid. It must be 2 to 256 characters in length and cannot start with http:// or https://.|
|403|QuotaExceed.SecurityGroup|The maximum number of security groups is reached.|The error message returned because the maximum number of security groups is reached. Submit a ticket to apply for a whitelist.|
|404|InvalidVpcId.NotFound|Specified VPC does not exist.|The error message returned because the specified VPC ID does not exist.|
|400|InvalidSecurityGroupName.Malformed|Specified security group name is not valid.|The error message returned because the specified security group name is invalid. The name is displayed in the console. By default, no name is specified for a security group. The name must be 2 to 128 characters in length. It must start with a letter and can contain letters, digits, colons \(:\), underscores \(\_\), and hyphens \(-\). It cannot start with http:// or https://.|
|400|InvalidSecurityGroupDiscription.Malformed|Specified security group description is not valid.|The error message returned because the specified description is invalid.|
|500|InternalError|The request processing has failed due to some unknown error.|The error message returned because an internal error has occurred. Try again later. If the problem persists, submit a ticket.|
|403|InvalidVpcId.NotFound|vpc id must not empty when only support vpc vm.|The error message returned because the specified VPC ID is empty.|
|400|IncorrectVpcStatus|Current VPC status does not support this operation.|The error message returned because the operation is not supported while the VPC is in the current state.|
|400|InvalidTagKey.Malformed|Specified key is not valid.|The error message returned because the specified tag key is invalid.|
|400|InvalidTagValue.Malformed|Specified end time is not valid.|The error message returned because the specified tag value is invalid.|
|404|InvalidResourceGroup.NotFound|The ResourceGroup provided does not exist in our records.|The error message returned because the resource group does not exist in the records.|
|400|Duplicate.TagKey|The Tag.N.Key contain duplicate key.|The error message returned because the specified tag key is repeated.|
|400|InvalidTagKey.Malformed|The specified Tag.N.Key is not valid.|The error message returned because the specified Tag.N.Value is invalid.|
|400|InvalidTagValue.Malformed|The specified Tag.N.Value is not valid.|The error message returned because the specified Tag.N.Value is invalid.|
|403|IdempotentProcessing|The previous idempotent request\(s\) is still processing.|The error message returned because the previous idempotence request is being processed.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

