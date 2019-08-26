# ExportImage {#doc_api_1061139 .reference}

Exports a custom image to an OSS bucket in the same region as the custom image.

## Description {#description .section}

-   This operation cannot export custom images that were created from the system disk snapshots of images available in Marketplace.
-   A custom disk cannot be exported if it contains more than four data disk snapshots or if any of the data disks exceed 500 GB in size.
-   You must [submit a ticket](https://workorder-intl.console.aliyun.com/#/ticket/createIndex) to activate the image export feature.
-   You must use RAM to authorize a RAM role for ECS to write data to OSS. Refer to the following section to create and authorize the RAM role:

    1. Create a role named `AliyunECSImageExportDefaultRole`. Any other role names are invalid. Refer to the following code to configure the policy for the role:

    ``` {#codeblock_4uj_sc3_0nk}
    
             {
               "Statement": [
                 {
                   "Action": "sts:AssumeRole",
                   "Effect": "Allow",
                   "Principal": {
                     "Service": [
                       "ecs.aliyuncs.com"
                     ]
                   }
                 }
               ],
               "Version": "1"
             }
            
    ```

    2. In the role `AliyunECSImageExportDefaultRole`, add the following default system permission policy: `AliyunECSImageExportRolePolicy`. This policy is the default policy for ECS to export images. For more information, see [RAM](https://ram.console.aliyun.com/?spm=5176.2020520101.0.0.64c64df5dfpmdY#/role/authorize?request=%7B%22Requests%22:%20%7B%22request1%22:%20%7B%22RoleName%22:%20%22AliyunECSImageImportDefaultRole%22,%20%22TemplateId%22:%20%22ECSImportRole%22%7D,%20%22request2%22:%20%7B%22RoleName%22:%20%22AliyunECSImageExportDefaultRole%22,%20%22TemplateId%22:%20%22ECSExportRole%22%7D%7D,%20%22ReturnUrl%22:%20%22https:%2F%2Fecs.console.aliyun.com%2F%22,%20%22Service%22:%20%22ECS%22%7D). You can also create your custom policies with the following permissions:

    ``` {#codeblock_kap_5xg_mzc}
    
             {
               "Version": "1",
               "Statement": [
                 {
                   "Action": [
                     "oss:GetObject",
                     "oss:PutObject",
                     "oss:DeleteObject",
                     "oss:GetBucketLocation",
                     "oss:GetBucketInfo",
                     "oss:AbortMultipartUpload",
                     "oss:ListMultipartUploads",
                     "oss:ListParts"
                   ],
                   "Resource": "*",
                   "Effect": "Allow"
                 }
               ]
             }
            
    ```


## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=ExportImage) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|ImageId|String|Yes|m-imageid1| The ID of the custom image.

 |
|OSSBucket|String|Yes|testexportImage| The OSS bucket to which the image is to be exported.

 |
|RegionId|String|Yes|cn-hangzhou| The ID of the region to which the custom image belongs. You can call [DescribeRegions](~~25609~~) to view the latest regions of Alibaba Cloud.

 |
|Action|String|No|ExportImage| The operation that you want to perform. Set the value to ExportImage.

 |
|OSSPrefix|String|No|EcsExport| The prefix of your OSS object. It must be 1 to 30 characters in length and can contain digits and letters.

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|RegionId|String|cn-hangzhou| The ID of the region.

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request.

 |
|TaskId|String|tsk-231234567| The ID of the image export task.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=ExportImage
&ImageId=m-imageid1
&OSSBucket=testexportImage
&RegionId=cn-hangzhou 
&OSSPrefix=EcsExport
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<ExportImageResponse>
  <RequestId>C8B26B44-0189-443E-9816-D951F59623A9</RequestId>
  <ExportTaskId>tsk-231234567</ExportTaskId>
  <RegionId>cn-hangzhou</RegionId> 
</ExportImageResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"RegionId":"cn-hangzhou",
	"RequestId":"C8B26B44-0189-443E-9816-D951F59623A9",
	"ExportTaskId":"tsk-231234567"
}
```

## Error codes {#section_6s2_5uv_fq3 .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|400|MissingParameter|An input parameter "RegionId" that is mandatory for processing the request is not supplied.|The error message returned when the required RegionId parameter is not specified.|
|400|MissingParameter|An input parameter ImageId that is mandatory for processing the request is not supplied.|The error message returned when the required ImageId parameter is not specified.|
|400|InvalidRegionId.NotFound|The specified RegionId does not exist.|The error message returned when the specified Region ID does not exist. Check whether the service is available in this region.|
|400|InvalidRegion.NotSupport|The specified region does not support image import or export.|The error message returned when the specified region does not support this operation.|
|404|InvalidImageId.NotFound|The specified ImageId does not exist.|The error message returned when the specified image does not exist under this account. Check whether the image ID is correct.|
|400|IncorrectImageStatus|The specified Image is not available.|The error message returned when the specified source image is in a state that does not support the current operation.|
|403|ImageNotSupported|The specified image from the image market, do not support export image.|The error message returned when you are trying to export images from Marketplace.|
|400|InvalidImageFormat.Malformed|The specified Image Format is wrongly formed.|The error message returned when the format of the AssociateInstanceType parameter is incorrect.|
|403|ExportImageFailed|Exporting image is failed, Please contact the administrator.|The error message returned when the image failed to be exported. Contact a system administrator.|
|400|InvalidImage.DiskAmountOrSize|The diskSize or diskAmount of the image exceeds the limitation.|The error message returned when the disk size or number of disks has reached the upper limit for image export.|
|400|ImageNotSupported|The specified Image contains encrypted snapshots, do not support export.|The error message returned when the specified image contains encrypted snapshots and cannot be exported.|
|400|ImageNotSupported|Image from image market does not support exporting.|The error message returned when you are trying to export images from Marketplace.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

