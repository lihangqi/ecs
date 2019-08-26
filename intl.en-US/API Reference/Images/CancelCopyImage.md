# CancelCopyImage {#doc_api_999585 .reference}

Cancels an image copy task.

## Description {#description .section}

When you call this operation, note that:

-   After you cancel the task, the destination image created in the target region is deleted, and the source image remains unchanged.
-   If the image copy process is completed, the CancelCopyImage operation fails and an error will be returned.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=CancelCopyImage) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|ImageId|String|Yes|m-imageid1| The ID of the image being copied.

 |
|RegionId|String|Yes|cn-hangzhou| The ID of the region to which the image belongs. You can call [DescribeRegions](~~25609~~) to view the latest regions of Alibaba Cloud.

 |
|Action|String|No|CancelCopyImage| The operation that you want to perform. Set the value to CancelCopyImage.

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=CancelCopyImage
&ImageId=m-imageid1
&RegionId=cn-hangzhou 
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<CancelCopyImageResponse>
  <RequestId>C8B26B44-0189-443E-9816-D951F59623A9</RequestId>
</CancelCopyImageResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"C8B26B44-0189-443E-9816-D951F59623A9"
}
```

## Error codes {#section_s6s_4hb_h8p .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|404|InvalidRegionId.NotFound|The specified RegionId does not exist.|The error message returned when the specified Region ID does not exist. Check whether the service is available in this region.|
|404|InvalidImageId.NotFound|The specified ImageId does not exist.|The error message returned when the specified image does not exist under this account. Check whether the image ID is correct.|
|400|IncorrectImageStatus|The image is copied finished.|The error message returned when the specified image has been copied and the copy task cannot be canceled.|
|400|InvalidDescription.Malformed|The specified description is wrongly formed.|The error message returned when the specified description is invalid. The description must be 2 to 256 characters in length and cannot start with http:// or https://.|
|400|IncorrectImageStatus|The specified snapshot is not coping.|The error message returned when the specified snapshot is not being copied.|
|400|IncorrectImageStatus|The specified image is not coping.|The error message returned when the specified image is not being copied.|
|400|IncorrectImageStatus|The image has completed copy.|The error message returned when the specified image has been copied and the copy task cannot be canceled.|
|400|IncorrectImageStatus|The Image copy has been failed.|The error message returned when the specified image failed to be copied.|
|400|CancelNotSupported|The specified image copying can not be cancelled.|The error message returned when the specified copy task cannot be canceled.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

