# DescribeImages {#doc_api_1023335 .reference}

Queries available images.

## Description {#description .section}

-   You can query your own custom images, public images provided by Alibaba Cloud, available images from Marketplace, and shared images from other Alibaba Cloud users.
-   This operation supports paged query. The response contains the total number of available images and the images on the current page. Ten entries are displayed on each page by default.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=DescribeImages) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|RegionId|String|Yes|cn-hangzhou| The ID of the region to which the instance belongs. You can call [DescribeRegions](~~25609~~) to view the latest regions of Alibaba Cloud.

 |
|Action|String|No|DescribeImages| The operation that you want to perform. Set the value to DescribeImages.

 |
|ActionType|String|No|\*| The operations that the image is used for. Valid values:

 -   \*
-   CreateEcs
-   ChangeOS

 |
|Architecture|String|No|i386| The image architecture. Valid values:

 -   i386
-   x86\_64

 |
|DryRun|Boolean|No|false| Indicates whether the system performs a permission check only.

 -   true: Sends a permission check request, without querying resource status. The system checks whether your AccessKey is valid, whether RAM users are authorized, and whether the required parameters are set. For a failed check, corresponding error message is returned. For a successful check, the DryRunOperation error code is returned.
-   false: Sends a normal request, returns the 2XX HTTP status code after the check, and queries the resource status directly.

 Default value: false.

 |
|Filter.N.Key|String|No|CreationStartTime| The key of the filtering condition.

 |
|Filter.N.Value|String|No|2017-12-05T22:40:00Z| The value of the filtering condition.

 |
|ImageId|String|No|m-imageid1| The ID of the image.

 |
|ImageName|String|No|FinanceJoshua| The name of the image.

 |
|ImageOwnerAlias|String|No|Self| The source of the image. Valid values:

 -   system: public images provided by Alibaba Cloud.
-   self: your custom images.
-   others: shared images from other Alibaba Cloud users.
-   marketplace: available images from Marketplace. If images from Marketplace are returned in the result, you can directly use these images without prior subscription. You must pay attention to the billing details of images from Marketplace.

 Default value: null, indicating that the results matching system, self, and others are returned.

 |
|InstanceType|String|No|ecs.g5.large| The instance type of the images to be queried.

 |
|IsSupportCloudinit|Boolean|No|true| Indicates whether queried images supports cloud-init.

 |
|IsSupportIoOptimized|Boolean|No|true| Indicates whether queried images can be used for I/O optimized instances.

 |
|OSType|String|No|linux| The operating system type of images to be queried. Valid values:

 -   windows
-   linux

 |
|OwnerAccount|String|No|155780923770| The logon name of a RAM user.

 |
|PageNumber|Integer|No|1| The page number that you query in the image list. Starting value: 1.

 Default value: 1.

 |
|PageSize|Integer|No|10| The number of entries per page. Maximum value: 100.

 Default value: 10.

 |
|ResourceGroupId|String|No|rg-resourcegroupid1| The ID of the resource group to which the queried custom images belong.

 |
|ShowExpired|Boolean|No|false| Indicates whether the subscription of a image has expired.

 **Note:** This parameter will be removed in the future. We recommend that you use other parameters to ensure compatibility.

 |
|SnapshotId|String|No|s-snapshotid1| The ID of the snapshot used to create the images to be queried.

 |
|Status|String|No|Available| The status of the image to be queried. Valid values:

 -   Creating: The image is being created.
-   Waiting: Multiple images are waiting to be processed.
-   Available \(default\): The image is available.
-   UnAvailable: The image is unavailable.
-   CreateFailed: The image failed to be created.

 Separate multiple parameter values with commas \(,\).

 |
|Tag.N.Key|String|No|FinanceJoshua| The tag key of the image. Valid values of N: 1 to 20. It cannot be a null string. It can be a maximum of 64 characters in length. It cannot start with aliyun, acs:, http://, or https://.

 |
|Tag.N.Value|String|No|FinanceDept| The tag value of the image. Valid values of N: 1 to 20. It can be a null string. It can be a maximum of 128 characters in length. It cannot start with aliyun, acs:, http://, or https://.

 |
|Tag.N.key|String|No|FinanceJoshua| The tag key of the image.

 **Note:** This parameter will be removed in the future. We recommend that you use the Tag.N.Key parameter to ensure compatibility.

 |
|Tag.N.value|String|No|FinanceDept| The tag value of the image.

 **Note:** This parameter will be removed in the future. We recommend that you use the Tag.N.Value parameter to ensure compatibility.

 |
|Usage|String|No|instance| Queries whether the specified image is running on an ECS instance or not. Valid values:

 -   instance: The image is running on an ECS instance.
-   none: The image is not in use.

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|Images| | | The image information. It is a set of ImageType data.

 |
|└Architecture|String|x86\_64| The system architecture. Valid values:

 -   i386
-   x86\_64

 |
|└CreationTime|String|2018-01-10T01:01:10Z| The creation time of the image.

 |
|└Description|String|FinanceDept| The description of the image.

 |
|└DiskDeviceMappings| | | The description of disks and snapshots related to the image.

 |
|└Device|String|/dev/xvdb| The device information of the created disk, such as /dev/xvdb.

 |
|└Format|String|qcow2| The format of the image.

 |
|└ImportOSSBucket|String|testEcsImport| The OSS bucket where an imported image is stored.

 |
|└ImportOSSObject|String|imageImport| The OSS object corresponding to an imported image file.

 |
|└Progress|String|32%| The progress of an image copy task.

 |
|└RemainTime|Integer|213| The remaining time in seconds for an image copy task.

 |
|└Size|String|80| The size of the created disk.

 |
|└SnapshotId|String|s-snapshotid1| The ID of the snapshot.

 |
|└Type|String|custom| The type of the image.

 |
|└ImageId|String|m-imageid1| The ID of the image.

 |
|└ImageName|String|Joshua-Finance| The name of the image.

 |
|└ImageOwnerAlias|String|self| The source of the image. Valid values:

 -   system: public images provided by Alibaba Cloud.
-   self: your own custom images.
-   others: shared images from other Alibaba Cloud users.
-   marketplace: available images from Marketplace.

 |
|└ImageVersion|String|2| The version of the image.

 |
|└IsCopied|Boolean|false| Indicates whether the image is a copy of another image.

 |
|└IsSelfShared|String|true| Indicates whether the image is shared to other Alibaba Cloud accounts.

 |
|└IsSubscribed|Boolean|false| Indicates whether the user has subscribed to the image corresponding to the ProductCode. Valid values:

 -   true: The user has subscribed to the image.
-   false: The user has not subscribed to the image.

 |
|└IsSupportCloudinit|Boolean|true| Indicates whether the image supports cloud-init.

 |
|└IsSupportIoOptimized|Boolean|true| Indicates whether the image can be used for I/O optimized instances.

 |
|└OSName|String|Aliyun Linux 17.1| The name of the operating system.

 |
|└OSType|String|Linux| The type of the operating system. Valid values:

 -   windows
-   linux

 |
|└Platform|String|Aliyun Linux| The release version of the operating system.

 |
|└ProductCode|String|jxsc000204| The product code of the image from Marketplace.

 |
|└Progress|String|100| The progress of image creation. Unit: percent \(%\).

 |
|└ResourceGroupId|String|rg-resourcegroupid1| The ID of the resource group to which the image belongs.

 |
|└Size|Integer|80| The size of the image.

 |
|└Status|String|Available| The status of the image. Valid values:

 -   UnAvailable
-   Available
-   Creating
-   CreateFailed

 |
|└Tags| | | The tag pair information of the image.

 |
|└TagKey|String|FinanceDept| The tag key of the image.

 |
|└TagValue|String|FinanceJoshua| The tag value of the image.

 |
|└Usage|String|none| The referenced resource type. Valid values:

 -   instance
-   none

 |
|PageNumber|Integer|1| The current page number.

 |
|PageSize|Integer|10| The number of entries on the current page.

 |
|RegionId|String|cn-hangzhou| The ID of the region to which the image belongs.

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request.

 |
|TotalCount|Integer|24| The total number of available images.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=DescribeImages
&RegionId=cn-hangzhou 
&Usage=instance
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<DescribeImagesResponse>
  <Images>
    <Image>
      <Architecture>i386</Architecture>
      <CreationTime>2014-07-22T09:53:44Z</CreationTime>
      <Description/> 
      <DiskDeviceMappings>
        <DiskDeviceMapping>
          <Device>/dev/xvda</Device>
          <Size>20</Size>
          <SnapshotId/>
        </DiskDeviceMapping>
      </DiskDeviceMappings>
      <ImageId>suse11sp3_64_20G_aliaegis_20150428.vhd</ImageId>
      <ImageName>suse11sp3_64_20G_aliaegis_20150428.vhd</ImageName>
      <ImageOwnerAlias>system</ImageOwnerAlias>
      <ImageVersion>1.0</ImageVersion>
      <IsCopied>false</IsCopied>
      <IsSubscribed>false</IsSubscribed>
      <OSName>SUSE Linux  Enterprise Server 11 SP3 64-bit</OSName>
      <ProductCode/> 
      <OSType>linux</OSType> 
      <Platform>SUSE</Platform>
      <Progress>100</Progress> 
      <Size>20</Size>
      <Status>Available</Status> 
      <Usage>instance</Usage>
    </Image>
  </Images>
  <PageNumber>1</PageNumber> 
  <PageSize>2</PageSize>
  <RegionId>cn-hangzhou</RegionId> 
  <TotalCount>24</TotalCount>
  <RequestId>7871BB26-3002-4950-B2E6-98D333077EA5</RequestId>
</DescribeImagesResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"PageNumber":1,
	"TotalCount":24,
	"PageSize":1,
	"RequestId":"49CBCED4-C9B9-4851-BEB5-8FB5E5169E30",
	"RegionId":"cn-hangzhou",
	"Images":{
		"Image":[
			{
				"ImageId":"suse11sp3_64_20G_aliaegis_20150428.vhd",
				"OSType":"linux",
				"Architecture":"x86_64",
				"OSName":"SUSE Linux  Enterprise Server 11 SP3 64-bit",
				"DiskDeviceMappings":{
					"DiskDeviceMapping":[
						{
							"Device":"/dev/xvda",
							"Size":"20"
						}
					]
				},
				"ImageOwnerAlias":"system",
				"Progress":"100%",
				"Usage":"instance",
				"CreationTime":"2015-05-06T09:01:32Z",
				"Status":"Available",
				"ImageVersion":"1",
				"ImageName":"suse11sp3_64_20G_aliaegis_20150428.vhd",
				"IsCopied":false,
				"IsSubscribed":false,
				"Platform":"SUSE",
				"Size":20
			}
		]
	}
}
```

## Error codes {#section_oot_i97_7t9 .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|404|InvalidFilterKey.NotFound| |The error message returned when the specified start time or end time is invalid.|
|404|InvalidFilterValue| |The error message returned when the format of the specified time is invalid.|
|404|InvalidUsage|The specified Usage is not valid|The error message returned when the specified referenced resource type \(image, disk, image\_disk, or none\) is invalid.|
|400|InvalidTag.Mismatch|The specified Tag.n.Key and Tag.n.Value are not match.|The error message returned when the specified Tag.n.Key parameter does not correspond to the specified Tag.n.Value parameter.|
|400|InvalidTagCount|The specified tags are beyond the permitted range.|The error message returned when the number of specified tags has reached the upper limit.|
|400|InvalidInstanceType.ValueNotSupported|The specified InstanceType does not exist or beyond the permitted range.|The error message returned when the specified instance type is not supported|
|404|InvalidOSType|The specified OSType is not valid|The error message returned when the specified operating system is not supported.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

