# ModifyLaunchTemplateDefaultVersion {#doc_api_999545 .reference}

Modifies the default version of a launch template. If you do not specify a template version number when creating an instance \(RunInstances\), the default version will be used.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=ModifyLaunchTemplateDefaultVersion) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|DefaultVersionNumber|Long|Yes|2| The default version number for the instance launch template.

 |
|RegionId|String|Yes|cn-hangzhou| The ID of the region to which the template belongs. You can call [DescribeRegions](~~25609~~) to view the latest regions of Alibaba Cloud.

 |
|Action|String|No|ModifyLaunchTemplateDefaultVersion| The operation that you want to perform. Set the value to ModifyLaunchTemplateDefaultVersion.

 |
|LaunchTemplateId|String|No|lt-templateid1| The ID of the instance launch template. You must specify either the LaunchTemplateId parameter or the LaunchTemplateName parameter to determine a launch template.

 |
|LaunchTemplateName|String|No|lt-name1| The name of the instance launch template. You must specify either the LaunchTemplateId parameter or the LaunchTemplateName parameter to determine a launch template.

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=ModifyLaunchTemplateDefaultVersion
&DefaultVersionNumber=2 
&RegionId=cn-hangzhou 
&LaunchTemplateId=lt-templateid1
&LaunchTemplateName=lt-name1 
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<ModifyLaunchTemplateDefaultVersionResponse>
  <RequestId>04F0F334-1335-436C-A1D7-6C044FExxxxx</RequestId>
</ModifyLaunchTemplateDefaultVersionResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"04F0F334-1335-436C-A1D7-6C044FExxxxx"
}
```

## Error codes { .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|400|InvalidRegion.NotExist|%s|The error message returned when the specified region does not exist.|
|404|InvalidLaunchTemplate.NotFound|%s|The error message returned when the specified launch template name does not exist.|
|400|MissingParameter|%s|The error message returned when a required parameter is not specified.|
|400|InvalidParameter|%s|The error message returned when the parameter format is invalid.|
|403|InnerServiceFailed|%s|The error message returned when an internal service failed to be called.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

