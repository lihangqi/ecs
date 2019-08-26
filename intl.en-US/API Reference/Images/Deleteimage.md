# DeleteImage {#DeleteImage .reference}

Deletes a specified custom image.

## Request parameters {#RequestParameter .section}

|Name|Type |Required|Description|
|:---|:----|:-------|:----------|
|Action|String|Yes|The name of this interface. Value: DeleteImage.|
|RegionId|String|Yes|ID of an Alibaba Cloud region to where the image belongs. You can call [DescribeRegions](intl.en-US/API Reference/Regions/DescribeRegions.md#) to obtain the latest region list.|
|ImageId|String|Yes|ID of an image.|
|Force|String|No|Whether to directly delete the custom image or not. Optional values:-   true: Directly deletes the custom image, and ignores the usage status of the image.
-   false: Verifies whether the image has been used by any instance before the deletion.

|

## Response parameters {#section_jlg_ggz_xdb .section}

All are common response parameters. For more information, see [Common parameters](intl.en-US/API Reference/Call methods/Common parameters.md#commonResponseParameters).

## Examples { .section}

**Request example** 

```
https://ecs.aliyuncs.com/?Action=DeleteImage
&RegionId=cn-hangzhou
&ImageId=m-63DFD5FB2
&<Common Request Parameters>
```

**Response example** 

**XML format**

```
<DeleteImageResponse>
     <RequestId>CEF72CEB-54B6-4AE8-B225-F876FF7BA984</RequestId>
</DeleteImageResponse>
```

 **JSON format** 

```

    "RequestId": "CEF72CEB-54B6-4AE8-B225-F876FF7BA984"

```

## Error codes {#ErrorCode .section}

Error codes specific to this interface are as follows. For more information, see [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

|Error code |Error message |HTTP status code |Meaning|
|:----------|:-------------|:----------------|:------|
|ImageUsingByInstance|The specified image has been used to create instances.|403|The specified image is used by other instances and cannot be deleted.|
|ImageIsCreating|The specified image is being created.|403|The specified custom image is being created, please try again later.|
|ImageUseShared|The specified image has been shared to others.|403|The specified image cannot be deleted because you have shared it to other users.|
|OperationDenied.ImageCopying|The specified image is being copied.|403|The specified custom image is being copied, please try again later.|
|InvalidRegionId.NotFound|The specified region does not exist.|404|The specified `RegionId` does not exist.|

