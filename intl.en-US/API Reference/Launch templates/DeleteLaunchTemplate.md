# DeleteLaunchTemplate {#doc_api_999543 .reference}

Deletes an instance launch template.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=DeleteLaunchTemplate) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|RegionId|String|Yes|cn-hangzhou| The ID of the region to which the instance launch template belongs. You can call [DescribeRegions](~~25609~~) to view the latest regions of Alibaba Cloud.

 |
|Action|String|No|DeleteLaunchTemplate| The operation that you want to perform. Set the value to DeleteLaunchTemplate.

 |
|LaunchTemplateId|String|No|lt-bp1apo0bbbkuy0rj3b9X| The ID of the instance launch template. For more information, call [DescribeLaunchTemplates](~~73759~~). You must specify either the `LaunchTemplateId` parameter or the `LaunchTemplateName` parameter to determine a launch template.

 |
|LaunchTemplateName|String|No|JoshuaWinPostPaid| The name of the instance launch template. You must specify either the `LaunchTemplateId` parameter or the `LaunchTemplateName` parameter to determine a launch template.

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=DeleteLaunchTemplate
&RegionId=cn-hangzhou 
&LaunchTemplateId=lt-bp1apo0bbbkuy0rj3b9X
&LaunchTemplateName=JoshuaWinPostPaid
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<DeleteLaunchTemplateResponse>
  <RequestId>04F0F334-1335-436C-A1D7-6C044FExxxxx</RequestId>
</DeleteLaunchTemplateResponse>
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
|400|MissingParameter|%s|The error message returned when a required parameter is not specified.|
|400|InvalidParameter|%s|The error message returned when the parameter format is invalid.|
|403|InnerServiceFailed|%s|The error message returned when an internal service failed to be called.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

