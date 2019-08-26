# DescribeSecurityGroups {#doc_api_Ecs_DescribeSecurityGroups .reference}

You can call the DescribeSecurityGroups action to query basic information about your security groups, such as the security group ID and description. Security groups are displayed in descending order of security group IDs.

## Debugging {#apiExplorer .section}

Alibaba Cloud provides [OpenAPI Explorer](https://api.aliyun.com/#product=Ecs&api=DescribeSecurityGroups) to simplify API usage. You can use OpenAPI Explorer to search for APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|RegionId|String|Yes|cn-hangzhou| The region ID of the security group. You can call the [DescribeRegions](~~25609~~) operation to query the latest region list.

 |
|Action|String|No|DescribeSecurityGroups| The operation that you want to perform. Set this value to DescribeSecurityGroups.

 |
|DryRun|Boolean|No|false| Specifies whether to send a check request only. Default value: false.

 -   true: Only a check request is sent and no query is performed. The system checks whether your AccessKey is valid, whether RAM users are authorized, and whether the required parameters are set. If the check fails, the corresponding error code is returned. If the check succeeds, the DryRunOperation error code is returned.
-   false: A request is sent. If the 2XX HTTP status code is returned, the query is performed.

 Default value: false

 |
|NetworkType|String|No|vpc| The network type.

 |
|PageNumber|Integer|No|1| The number of the page to return. Pages start from page 1.

 Default value: 1

 |
|PageSize|Integer|No|10| The number of entries to return on each page. Maximum value: 50.

 Default value: 10

 |
|ResourceGroupId|String|No|rg-resourcegroupid1| The ID of the resource group to which the security group belongs.

 |
|SecurityGroupId|String|No|sg-securitygroupid| The ID of the security group.

 |
|SecurityGroupIds|String|No|\["sg-id1", "sg-id2", "sg-id2",....\]| A JSON array of security group IDs. A maximum of 100 security group IDs can be entered at a time. Separate multiple security group IDs with commas \(,\).

 |
|SecurityGroupName|String|No|test1| The name of the security group.

 |
|Tag.N.Key|String|No|FinanceDept| The tag key of the security group. Valid values of N: 1 to 20. The tag key cannot be an empty string. It can be up to 64 characters in length and cannot start with aliyun or acs:. It cannot contain http:// or https://.

 |
|Tag.N.Value|String|No|FinanceJoshua| The tag value of the security group. Valid values of N: 1 to 20. The tag value can be an empty string. It can be up to 128 characters in length and cannot start with aliyun or acs:. It cannot contain http:// or https://.

 |
|Tag.N.key|String|No|FinanceDept| The tag key of the security group.

 **Note:** This parameter will be removed in the future. We recommend that you use Tag.N.Key to ensure future compatibility.

 |
|Tag.N.value|String|No|FinanceJoshua| The tag value of the security group. Valid values of N: 1 to 20. It can be an empty string. It can be up to 128 characters in length. It cannot start with aliyun, acs:, http://, or https://.

 **Note:** This parameter will be removed in the future. We recommend that you use Tag.N.Value to ensure future compatibility.

 |
|VpcId|String|No|vpc-vpcid1| The ID of the VPC to which the security group belongs.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|PageNumber|Integer|1| The number of the page that was returned.

 |
|PageSize|Integer|10| The number of entries that were returned on each page.

 |
|RegionId|String|cn-hangzhou| The region ID of the security group.

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request.

 |
|SecurityGroups| | | The returned security group information. It is an array that consists of SecurityGroups data.

 |
|└CreationTime|String|2017-12-05T22:40:00Z| The time when the security group was created. The time follows the [ISO 8601](~~25696~~) standard in the yyyy-MM-ddThh:mmZ format. The time is displayed in UTC.

 |
|└Description|String|FinanceDept| The description of the security group.

 |
|└ResourceGroupId|String|rg-resourcegroupid1| The ID of the resource group to which the security group belongs.

 |
|└SecurityGroupId|String|sg-securitygroupid1| The ID of the security group.

 |
|└SecurityGroupName|String|FinanceJoshua| The name of the security group.

 |
|└SecurityGroupType|String|normal| The type of the security group. Valid values:

 -   normal: basic security group
-   enterprise: advanced security group

 |
|└Tags| | | The tag of the security group.

 |
|└TagKey|String|FinanceDept| The tag value of the security group.

 |
|└TagValue|String|FinanceJoshua| The tag key of the security group.

 |
|└VpcId|String|vpc-vpcid1| The ID of the VPC to which the security group belongs.

 |
|TotalCount|Integer|4| The total number of security groups.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=DescribeSecurityGroups
&RegionId=cn-hangzhou
&<Common request parameters>
```

Sample success responses

`XML` format

``` {#xml_return_success_demo}
<DescribeSecurityGroupsResponse>
  <RequestId>94D38899-626D-434A-891F-7E1F77A81525</RequestId>
  <TotalCount>4</TotalCount>
  <PageNumber>1</PageNumber>
  <PageSize>10</PageSize>
  <RegionId>cn-hangzhou</RegionId>
  <SecurityGroups>
    <SecurityGroup>
      <SecurityGroupId>sg-securityGroupId1</SecurityGroupId>
      <Description>Test</Description>
    </SecurityGroup>
    <SecurityGroup>
      <SecurityGroupId>sg-securityGroupId2</SecurityGroupId>
      <Description>test00212</Description>
    </SecurityGroup>
    <SecurityGroup>
      <SecurityGroupId>sg-securityGroupId3</SecurityGroupId>
      <Description>cn-hangzhou test group</Description>
    </SecurityGroup>
    <SecurityGroup>
      <SecurityGroupId>sg-securityGroupId4</SecurityGroupId>
      <Description>cn-hangzhou test group</Description>
    </SecurityGroup>
  </SecurityGroups>
</DescribeSecurityGroupsResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"PageNumber":"1",
	"TotalCount":4,
	"PageSize":"10",
	"RegionId":"cn-hangzhou",
	"RequestId":"94D38899-626D-434A-891F-7E1F77A81525",
	"SecurityGroups":{
		"SecurityGroup":[
			{
				"SecurityGroupId":"sg-securityGroupId1",
				"Description":"TestByXcf"
			},
			{
				"SecurityGroupId":"sg-securityGroupId2",
				"Description":"test00212"
			},
			{
				"SecurityGroupId":"sg-securityGroupId3",
				"Description":"cn-hangzhou test group"
			},
			{
				"SecurityGroupId":"sg-securityGroupId4",
				"Description":"cn-hangzhou test group"
			}
		]
	}
}
```

## Error codes {#section_igl_dua_gdv .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|500|InternalError|The request processing has failed due to some unknown error.|The error message returned because an internal error has occurred. Try again later. If the problem persists, submit a ticket.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

