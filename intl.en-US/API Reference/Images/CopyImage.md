# CopyImage {#doc_api_999578 .reference}

Copies a custom image from one region to another. You can use copied images to perform operations in the target region, such as creating instances \(RunInstances\) and replacing system disks \(ReplaceSystemDisk\).

## Description {#description .section}

When you call this operation, note that:

-   You can only copy the custom image when it is in the Available state.
-   You can only copy the image belonging to your Alibaba Cloud account. Images cannot be copied from one account to another.
-   If the copying is not completed, you cannot call [DeleteImage](~~25537~~) to delete the image but you can call [CancelCopyImage](~~25539~~) to cancel the copying.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=CopyImage) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|ImageId|String|Yes|m-imageid1| The ID of the source custom image.

 |
|RegionId|String|Yes|cn-hangzhou| The ID of the region to which the source custom image belongs. You can call [DescribeRegions](~~25609~~) to view the latest regions of Alibaba Cloud.

 |
|Action|String|No|CopyImage| The operation that you want to perform. Set the value to CopyImage.

 |
|DestinationDescription|String|No|FinanceDept| The description of the destination custom image. The description must be 2 to 256 characters in length and cannot start with http:// or https://. Default value: null.

 |
|DestinationImageName|String|No|FinanceJoshua| The name of the destination custom image. The name must be 2 to 128 characters in length. It must start with a letter and cannot start with http:// or https://. It can contain letters, digits, colons \(:\), underscores \(\_\), and hyphens \(-\). Default value: null.

 |
|DestinationRegionId|String|No|cn-shanghai| The ID of the region to which the destination custom image belongs.

 |
|Encrypted|Boolean|No|false| Indicates whether to encrypt the image.

 |
|Tag.N.Key|String|No|FinanceJoshua| The tag key of the custom image.

 |
|Tag.N.Value|String|No|FinanceDept| The tag value of the custom image.

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|ImageId|String|m-imageid2| The ID of the destination custom image.

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=CopyImage
&ImageId=m-imageid1
&RegionId=cn-hangzhou 
&DestinationImageName=FinanceJoshua
&DestinationDescription=FinanceDept
&DestinationRegionId=cn-shanghai
&Encrypted=false
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<CopyImageResponse>
  <RequestId>C8B26B44-0189-443E-9816-D951F59623A9</RequestId>
  <ImageId>Img-231234567</ImageId>
</CopyImageResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"ImageId":"Img-231234567",
	"RequestId":"C8B26B44-0189-443E-9816-D951F59623A9"
}
```

## Error codes {#section_a7f_h7q_lff .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|401|InvalidAliUid.IsNull|The aliUid must not be null|The error message returned when the required AliUid parameter is not specified.|
|403|Forbidden|User not authorized to operate on the specified resource.|The error message returned when you are not authorized to access the specified resource.|
|400|InvalidDescription.Malformed|The specified destination description is wrongly formed.|The error message returned when the specified description is invalid. The description must be 2 to 256 characters in length and cannot start with http:// or https://.|
|400|InvalidDescription.Malformed|The specified description is wrongly formed.|The error message returned when the specified description is invalid. The description must be 2 to 256 characters in length and cannot start with http:// or https://.|
|404|InvalidImageId.NotFound|The specified ImageId does not exist.|The error message returned when the specified image does not exist under this account. Check whether the image ID is correct.|
|400|IncorrectImageStatus|The image not available.|The error message returned when the specified image is unavailable.|
|403|QuotaExceed.Image|The Image Quota exceeds.|The error message returned when the custom image quota has been exhausted.|
|403|QuotaExceed.Snapshot|The snapshot quota exceeds.|The error message returned when the snapshot quota has been exhausted. To store new snapshots, you can delete existing snapshots without affecting your business.|
|403|OperationDenied|The specified snapshot is not allowed to create image.|The error message returned when the specified snapshot cannot be used to create images.|
|403|SizeExceed.Image|The image exceeds the maximum size. Please open a ticket to add the account to the white list.|The error message returned when the specified image size has reached the upper limit. If the problem persists, please submit a ticket to contact Alibaba Cloud technical support personnel.|
|403|OperationDeined.EncryptedSnapshot|The image contains encrypted snapshots, which do not support copying.|The error message returned when the specified image contains encrypted snapshots and cannot be copied.|
|403|OperationDenied.SameRegionOnly|The image shared from others can not be copied to another region directly.|The error message returned when the specified image is shared by other accounts and cannot be copied.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

