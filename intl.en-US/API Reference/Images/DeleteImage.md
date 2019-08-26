# DeleteImage {#doc_api_999576 .reference}

Deletes a custom image.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=DeleteImage) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|ImageId|String|Yes|m-imageid1| The ID of the custom image. If the specified custom image does not exist, the request will be ignored.

 |
|RegionId|String|Yes|cn-hangzhou| The ID of the region to which the custom image belongs. You can call [DescribeRegions](~~25609~~) to view the latest regions of Alibaba Cloud.

 |
|Action|String|No|DeleteImage| The operation that you want to perform. Set the value to DeleteImage.

 |
|Force|Boolean|No|false| Indicates whether to force delete the custom image. Valid values:

 -   true: Force deletes the custom image, regardless of whether the image is currently being used by other instances.
-   false: Verifies that the image is not currently in use by any other instances before deleting the image.

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=DeleteImage
&ImageId=m-imageid1
&RegionId=cn-hangzhou 
&Force=false
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<DeleteImageResponse>
  <RequestId>CEF72CEB-54B6-4AE8-B225-F876FF7BA984</RequestId> 
</DeleteImageResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"CEF72CEB-54B6-4AE8-B225-F876FF7BA984"
}
```

## Error codes {#section_hos_wu4_saf .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|403|ImageUsingByInstance|The specified image has been used to create instances.|The error message returned when the specified image is currently in use by other instances and cannot be deleted.|
|403|ImageIsCreating|The specified image is being created.|The error message returned when the specified image is being created.|
|403|ImageIsImporting|The specified Image is importing.|The error message returned when the specified image is being imported and cannot be deleted.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

