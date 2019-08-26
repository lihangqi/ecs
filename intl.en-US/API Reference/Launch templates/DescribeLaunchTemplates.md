# DescribeLaunchTemplates {#doc_api_1006047 .reference}

Queries one or more instance launch templates.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=DescribeLaunchTemplates) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|RegionId|String|Yes|cn-hangzhou| The ID of the region. You can call [DescribeRegions](~~25609~~) to view the latest regions of Alibaba Cloud.

 |
|Action|String|No|DescribeLaunchTemplates| The operation that you want to perform. Set the value to DescribeLaunchTemplates.

 |
|LaunchTemplateId.N|RepeatList|No|lt-m5e3ofjr1zn1aw7qdxxx| The IDs of one or more instance launch templates to be queried. You can specify a maximum of 100 launch template IDs. You must specify either the LaunchTemplateId parameter or the LaunchTemplateName parameter to determine a launch template.

 |
|LaunchTemplateName.N|RepeatList|No|wd-1526307480xxx| The names of one or more instance launch templates to be queried. You can specify a maximum of 100 launch template names.

 |
|PageNumber|Integer|No|1| The page number that you query in the instance launch template list. Starting value: 1.

 Default value: 1.

 |
|PageSize|Integer|No|10| The number of entries per page. Maximum value: 50.

 Default value: 10.

 |
|TemplateResourceGroupId|String|No|rg-resourcegroupid1| The ID of the resource group to which the launch template belongs.

 |
|TemplateTag.N.Key|String|No|FinanceDept| The tag key of the launch template. Valid values of N: 1 to 20.

 |
|TemplateTag.N.Value|String|No|FinanceDepltJoshua| The tag value of the launch template. Valid values of N: 1 to 20.

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|LaunchTemplateSets| | | A set of instance launch templates.

 |
|└CreateTime|String|2018-05-14T14:18:00Z| The creation time of the instance launch template.

 |
|└CreatedBy|String|1942111349714xxx| The creator of the instance launch template.

 |
|└DefaultVersionNumber|Long|1| The default version number of the template.

 |
|└LatestVersionNumber|Long|1| The latest version number of the template.

 |
|└LaunchTemplateId|String|lt-m5e3ofjr1zn1aw7qdxxx| The ID of the instance launch template.

 |
|└LaunchTemplateName|String|wd-1526307480xxx| The name of the instance launch template.

 |
|└ModifiedTime|String|2018-05-14T14:18:00Z| The time when the template was last modified.

 |
|└ResourceGroupId|String|rg-resourcegroupid1| The ID of the resource group to which the launch template belongs.

 |
|└Tags| | | The tag of the launch template.

 |
|└TagKey|String|FinanceDept| The tag key of the launch template.

 |
|└TagValue|String|FinanceDeptJoshua| The tag value of the launch template.

 |
|PageNumber|Integer|1| The current page number.

 |
|PageSize|Integer|10| The number of entries per page.

 |
|RequestId|String|04F0F334-1335-436C-A1D7-6C044FExxxxx| The ID of the request. This parameter is returned regardless of whether the operation is successful.

 |
|TotalCount|Integer|1| The total number of instance launch templates.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=DescribeLaunchTemplates
&RegionId=cn-hangzhou 
&TemplateTag. 1. Key=FinanceDept
&TemplateTag. 1. Value=FinanceDepltJoshua
&LaunchTemplateId. 1=lt-m5e3ofjr1zn1aw7qdxxx
&LaunchTemplateName. 1=wd-1526307480xxx
&PageNumber=1 
&PageSize=10 
&TemplateResourceGroupId=rg-resourcegroupid1
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<DescribeLaunchTemplatesResponse>
  <RequestId>04F0F334-1335-436C-A1D7-6C044FExxxxx</RequestId>
  <TotalCount>1</TotalCount> 
  <PageNumber>1</PageNumber> 
  <PageSize>10</PageSize> 
  <LaunchTemplateSets>
    <LaunchTemplateSet>
      <CreateTime>2018-05-14T14:18:00Z</CreateTime>
      <ModifiedTime>2018-05-14T14:18:00Z</ModifiedTime>
      <LaunchTemplateid>lt-m5e3ofjr1zn1aw7xxxx</LaunchTemplateid>
      <LaunchTemplateName>wd-1526307480xxx</LaunchTemplateName>
      <DefaultVersionNumber>1</DefaultVersionNumber>
      <LatestVersionNumber>1</LatestVersionNumber>
      <CreatedBy>1942111349714xxx</CreatedBy>
    </LaunchTemplateSet>
  </LaunchTemplateSets>
</DescribeLaunchTemplatesResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"PageNumber":1,
	"TotalCount":1,
	"LaunchTemplateSets":{
		"LaunchTemplateSet":[
			{
				"DefaultVersionNumber":1,
				"LaunchTemplateId":"lt-m5e3ofjr1zn1aw7qdxxx",
				"LatestVersionNumber":1,
				"CreateTime":"2018-05-14T14:18:00Z",
				"CreatedBy":"1942111349714xxx",
				"ModifiedTime":"2018-05-14T14:18:00Z",
				"LaunchTemplateName":"wd-1526307480xxx"
			}
		]
	},
	"PageSize":10,
	"RequestId":"04F0F334-1335-436C-A1D7-6C044FExxxxx"
}
```

## Error codes { .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|400|InvalidRegion.NotExist|%s|The error message returned when the specified region does not exist.|
|400|MissingParameter|%s|The error message returned when a required parameter is not specified.|
|400|InvalidParameter|%s|The error message returned when the parameter format is invalid.|
|403|InnerServiceFailed|%s|The error message returned when an internal service failed to be called.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

