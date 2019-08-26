# ImportImage {#doc_api_1062165 .reference}

Imports an on-premises image to Alibaba Cloud ECS and use it as a custom image within its region.

## Methods {#description .section}

You can use the imported image to create an ECS instance \(RunInstances\) or replace the system disk of an instance \(ReplaceSystemDisk\). When you call this operation, note that:

-   You must [upload the image file to OSS](~~31886~~) before you can import the image.
-   You can only import an image to the same region as the OSS bucket that the image file is uploaded to.
-   Valid values of n in the `DiskDeviceMapping.n` parameter: 1 to 17. When n is 1, the disk is a system disk. When n is 2 to 17, the disk is a data disk.
-   You cannot delete an image that is being imported. However, you can call [CancelTask](~~25624~~) to cancel the image import task.
-   To use [RAM](~~28627~~) to allow ECS to access OSS for your Alibaba Cloud account, follow these steps:

    1. Create a role named `AliyunECSImageImportDefaultRole`.**You must use this exact name** or else the image will fail to be imported. Refer to the following code to set the policy for the role:

    ``` {#codeblock_89v_l9f_nv1}
    
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

    2. Attach the permission policy `AliyunECSImageImportRolePolicy` to the role. This policy is the default policy for ECS image import. For more information, see [RAM](https://ram.console.aliyun.com/?spm=5176.2020520101.0.0.64c64df5dfpmdY#/role/authorize?request=%7B%22Requests%22:%20%7B%22request1%22:%20%7B%22RoleName%22:%20%22AliyunECSImageImportDefaultRole%22,%20%22TemplateId%22:%20%22ECSImportRole%22%7D,%20%22request2%22:%20%7B%22RoleName%22:%20%22AliyunECSImageExportDefaultRole%22,%20%22TemplateId%22:%20%22ECSExportRole%22%7D%7D,%20%22ReturnUrl%22:%20%22https:%2F%2Fecs.console.aliyun.com%2F%22,%20%22Service%22:%20%22ECS%22%7D). You can also create your custom policies with the following permissions:

    ``` {#codeblock_egv_4ob_pmf}
    
            {
    			"Version": "1",
    			"Statement": [
    			{
    				"Action": [
            				"oss:GetObject",
            				"oss:GetBucketLocation",
            				"oss:GetBucketInfo"
    			],
            			"Resource": "*",
            			"Effect": "Allow"
            			}
    			]
            }
            
    ```


## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=ImportImage) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|RegionId|String|Yes|cn-hangzhou| The ID of the region to which the source custom image belongs. You can call [DescribeRegions](~~25609~~) to view the latest regions of Alibaba Cloud.

 |
|Action|String|No|ImportImage| The operation that you want to perform. Set the value to ImportImage.

 |
|Architecture|String|No|x86\_64| The system architecture. Valid values:

 -   i386
-   x86\_64 \(default\)

 |
|Description|String|No|FinanceDeptJoshua| The description of the image. The description must be 2 to 256 characters in length and cannot start with http:// or https://. Default value: null.

 |
|DiskDeviceMapping.N.Device|String|No|/dev/xvda| The name of disk N in the custom image. Valid values: /dev/xvda to /dev/xvdz.

 |
|DiskDeviceMapping.N.DiskImSize|Integer|No|80| The size of the custom image.

 **Note:** This parameter will be removed in the future. We recommend that you use the DiskDeviceMapping.N.DiskImageSize parameter to ensure compatibility.

 |
|DiskDeviceMapping.N.DiskImageSize|Integer|No|80| The size of the image. The space of the system disk must be greater than or equal to the actual used space of file systems. Valid values:

 -   5 to 500 GiB when n is set to 1
-   5 to 1000 GiB when n is set to 2 to 17

 When you import an image, the system automatically scans and checks the size of the image, and the checking result is used as the default value of this parameter.

 |
|DiskDeviceMapping.N.Format|String|No|qcow2| The format of the image. Valid values:

 -   RAW
-   VHD
-   qcow2

 When you import an image, the system automatically scans and checks the format of the image, and the checking result is used as the default value of this parameter.

 |
|DiskDeviceMapping.N.OSSBucket|String|No|ecsimageos| The OSS bucket where the image file is stored.

 |
|DiskDeviceMapping.N.OSSObject|String|No|CentOS\_5.4\_32.raw| The key of the OSS bucket where the image file is to be stored.

 |
|ImageName|String|No|FinanceJoshua| The name of the image. The name must be 2 to 128 characters in length. It must start with a letter and cannot start with http:// or https://. It can contain letters, digits, colons \(:\), underscores \(\_\), and hyphens \(-\). Default value: null.

 |
|OSType|String|No|linux| The type of the operating system. Valid values:

 -   windows
-   linux \(default\)

 |
|Platform|String|No|Other Linux| The release version of the operating system. Valid values:

 -   CentOS
-   Ubuntu
-   SUSE
-   OpenSUSE
-   Debian
-   CoreOS
-   Aliyun
-   Windows Server 2003
-   Windows Server 2008
-   Windows Server 2012
-   Others Linux \(default\)
-   Customized Linux

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|ImageId|String|m-imageid2| The ID of the image.

 |
|RegionId|String|cn-hangzhou| The ID of the region.

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request.

 |
|TaskId|String|123-345-2332-22323| The ID of an image import task.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=ImportImage
&RegionId=cn-hangzhou 
&DiskDeviceMapping.1.Format=qcow2
&DiskDeviceMapping.1.OSSBucket=ecsimageos
&DiskDeviceMapping.1.OSSObject=CentOS_5.4_32.raw
&DiskDeviceMapping.1.DiskImageSize=80
&ImageName=FinanceJoshua
&Description=FinanceDeptJoshua
&Architecture=x86_64
&OSType=linux
&Platform=Other Linux
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<ImportImageResponse>
  <RequestId>C8B26B44-0189-443E-9816-D951F59623A9</RequestId>
  <ImageId>Img-231234567</ImageId>
  <ImportTaskId>123-345-2332-22323</ImportTaskId>
</ImportImageResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"ImageId":"Img-231234567",
	"ImportTaskId":"123-345-2332-22323",
	"RequestId":"C8B26B44-0189-443E-9816-D951F59623A9"
}
```

## Error codes {#section_buj_dqc_zky .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|400|MissingParameter|An input parameter "RegionId" that is mandatory for processing the request is not supplied.|The error message returned when the required RegionId parameter is not specified.|
|400|InvalidImageSize|The specified DiskDeviceMapping.n.DiskImageSize beyond the permitted range.|The error message returned when the specified image does not exist.|
|400|InvalidImageFormat.Malformed|The specified Image Format is wrongly formed.|The error message returned when the format of the AssociateInstanceType parameter is incorrect.|
|400|InvalidRegionId.NotFound|The specified RegionId does not exist.|The error message returned when the specified Region ID does not exist. Check whether the service is available in this region.|
|400|InvalidRegion.NotSupport|The specified region does not support image import or export.|The error message returned when the specified region does not support this operation.|
|403|ImageIsImporting|The specified Image is importing.|The error message returned when the specified image is being imported and cannot be operated.|
|403|QuotaExceed.Image|The Image Quota exceeds.|The error message returned when the custom image quota has been exhausted.|
|403|ImportImageFailed|Importing image is failed, Please contact the administrator.|The error message returned when the image failed to be imported. Contact a system administrator.|
|403|InvalidParameter.Malformed|The specified parameter DiskDeviceMapping.n.Device is not valid.|The error message returned when the specified value of the DiskDeviceMapping.n.Device parameter is invalid.|
|400|InvalidOSSObject.NotFound|The specified OSS object does not exist in this region.|The error message returned when the specified OSS object does not exist.|
|400|InvalidOSSObject.NotFound|The specified OSS object cannot be retrieved.|The error message returned when the specified OSS object information cannot be read.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

