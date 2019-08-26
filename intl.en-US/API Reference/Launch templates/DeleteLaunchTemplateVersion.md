# DeleteLaunchTemplateVersion {#doc_api_999544 .reference}

Deletes an instance launch template version. This operation does not delete the default version of an instance launch template. To delete the default version, you must call DeleteLaunchTemplate to delete the instance launch template.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=DeleteLaunchTemplateVersion) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|DeleteVersion.N|RepeatList|Yes|2| The version number of the template. Valid values of N: 1 to 29. You can call [DescribeLaunchTemplateVersions](~~73761~~) to query all versions of an instance launch template.

 |
|RegionId|String|Yes|cn-hangzhou| The ID of the region to which the template belongs. You can call [DescribeRegions](~~25609~~) to view the latest regions of Alibaba Cloud.

 |
|Action|String|No|DeleteLaunchTemplateVersion| The operation that you want to perform. Set the value to DeleteLaunchTemplateVersion.

 |
|LaunchTemplateId|String|No|lt-bp1apo0bbbkuy0rj3b9X| The ID of the instance launch template. For more information, call [DescribeLaunchTemplates](~~73759~~).

 |
|LaunchTemplateName|String|No|JoshuaWinPostPaid| The name of the instance launch template.

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=DeleteLaunchTemplateVersion
&DeleteVersion. 1=2
&RegionId=cn-hangzhou 
&LaunchTemplateId=lt-bp1apo0bbbkuy0rj3b9X 
&LaunchTemplateName=JoshuaWinPostPaid 
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<DeleteLaunchTemplateVersionResponse>
  <RequestId>04F0F334-1335-436C-A1D7-6C044FExxxxx</RequestId>
</DeleteLaunchTemplateVersionResponse>
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

