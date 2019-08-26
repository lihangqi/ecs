# ResizeDisk {#doc_api_Ecs_ResizeDisk .reference}

You can call this operation to resize a cloud disk. You can resize both system disks and data disks.

## Description {#description .section}

**Note:** Before calling this operation, you must check the partition format of the cloud disk. If an existing partition of the cloud disk is created by using MBR, you cannot resize the cloud disk to greater than or equal to 2 TiB. Otherwise, data may be lost. If the MBR partition format is used, we recommend that you create and attach another data disk. Format a GPT partition and copy the data in the MBR partition to the GPT partition. For more information, see [Resize cloud disks offline](~~44986~~).

-   You can resize the following cloud disk types: basic disks \(cloud\), ultra disks \(cloud\_efficiency\), SSD disks \(cloud\_ssd\), and ESSD disks \(cloud\_essd\).
-   You cannot resize a cloud disk when a snapshot is being created for it.
-   The instance to which the disk is attached must be in the running or stopped state.
-   After resizing a cloud disk, you must [restart the instance](~~25440~~) in the console or call the [RebootInstance](~~25502~~) operation to validate the operation.
-   After you resize a cloud disk, its partitions and file systems will not change. You can allocate the storage space after resizing.

## Debugging {#apiExplorer .section}

Alibaba Cloud provides [OpenAPI Explorer](https://api.aliyun.com/#product=Ecs&api=ResizeDisk) to simplify API usage. You can use OpenAPI Explorer to search for APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|DiskId|String|Yes|d-diskid| The ID of the cloud disk to be resized.

 |
|NewSize|Integer|Yes|1900| The new disk capacity that you want to specify. Unit: GiB. Valid values:

 -   Basic disk \(cloud\): 5 to 2,000
-   Ultra disk \(cloud\_efficiency\): 20 to 6,144
-   SSD disk \(cloud\_ssd\): 20 to 6,144
-   ESSD disk \(cloud\_essd\): 20 to 32,768

 The new disk capacity must be larger than the original disk capacity. If the original capacity of a cloud disk is less than 6 TiB, you cannot resize it to more than 6 TiB.

 |
|Action|String|No|ResizeDisk| The operation that you want to perform. Set the value to ResizeDisk.

 |
|Type|String|No|offline| The method that you use to resize the cloud disk. Valid values:

 -   offline: In this method, you need to restart the instance to validate the operation. This is the default value.
-   online: In this method, you do not need to restart the instance. This method can only be used on data disk, and only ultra disks and SSD disks are supported.

 |
|ClientToken|String|No|123e4567-e89b-12d3-a456-426655440000| The client token that is used to ensure the idempotence of the request. You can use the client to generate this value, but you must ensure that it is unique among different requests. The **ClientToken** parameter can contain only ASCII characters, and cannot exceed 64 characters in length. For more information, see [How to ensure idempotence](~~25693~~).

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=ResizeDisk
&DiskId=d-diskid
&NewSize=1900
&ClientToken=123e4567-e89b-12d3-a456-426655440000
&<Common request parameters>
```

Sample success responses

`XML` format

``` {#xml_return_success_demo}
<ResizeDiskResponse>
  <RequestId>F3CD6886-D8D0-4FEE-B93E-1B73239673DE</RequestId>
</ResizeDiskResponse>

```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"F3CD6886-D8D0-4FEE-B93E-1B73239673DE"
}
```

## Error codes {#section_p8v_16o_pok .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|403|InvalidDataDiskSize.ValueNotSupported|The specified DataDisk.n.Size beyond the permitted range, or the capacity of snapshot exceeds the size limit of the specified disk category.|The error message returned because the maximum size of the specified data disk is reached.|
|404|InvalidDiskId.NotFound|The specified disk does not exist.|The error message returned because the specified DiskId parameter does not exist. Check whether the DiskId parameter is correct.|
|404|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|The error message returned because the specified InstanceId parameter does not exist.|
|403|OperationDenied|The type of the disk does not support the operation.|The error message returned because the operation is not supported by the specified data disk type.|
|403|OperationDenied|The status of the disk or the instance that the disk is attaching with does not support the operation.|The error message returned because the operation is not supported while the disk or instance is in the current state.|
|403|InvalidDiskSize.TooSmall|Specified new disk size is less than the original disk size.|The error message returned because the specified new disk capacity is smaller than the original disk capacity.|
|403|InvalidDiskSize.TooLarge|Specified new disk size is beyond the permitted range.|The error message returned because the specified new disk capacity is greater than the maximum capacity.|
|403|InstanceExpiredOrInArrears|The specified operation is denied as your prepay instance is expired \(prepay mode\) or in arrears \(afterpay mode\).|The error message returned because the subscription instance has expired. Renew the instance and try again.|
|403|DiskError|IncorrectDiskStatus|The error message returned because the specified DiskStatus parameter is invalid.|
|403|DiskInArrears|The specified operation is denied as your disk owing fee.|The error message returned because the disk has an overdue payment.|
|403|IncorrectInstanceStatus|The current status of the resource does not support this operation.|The error message returned because the operation is not supported while the resource is in the current state.|
|500|InternalError|The request processing has failed due to some unknown error.|The error message returned because an internal error has occurred. Try again later. If the problem persists, submit a ticket.|
|403|DiskCreatingSnapshot|The operation is denied due to a snapshot of the specified disk is not completed yet.|The error message returned because a snapshot is being created for the specified disk.|
|400|InvalidDataDiskCategory.ValueNotSupported|%s|The error message returned because the parameter is not supported.|
|400|InvalidParameter.Conflict|%s|The error message returned because the parameter is conflicting with another parameter.|
|400|InvalidDataDiskSize.ValueNotSupported|%s|The error message returned because the parameter is not supported.|
|403|InvalidDiskSize|Specified new disk size is less than or equal the original disk size.|The error message returned because the specified new disk capacity is smaller than or equal to the original disk capacity.|
|400|IncompleteParamter|Some fields cannot be null in this request.|The error message returned because a required parameter is not specified.|
|403|Operation.Conflict|The operation may conflict with others.|The error message returned because the operation is conflicting with another operation.|
|403|InstanceLockedForSecurity|The instance is locked due to security.|The error message returned because the operation is not supported while the resource is locked to ensure security.|
|403|IncorrectDiskStatus|The current disk status does not support this operation.|The error message returned because the operation is not supported while the disk is in the current state. Ensure that the disk is available and has no overdue payments.|
|403|UserNotInTheWhiteList|The user is not in disk white list.|The error message returned because you are not authorized to use the specified disk.|
|400|InvalidRegionId.MalFormed|The specified RegionId is not valid|The error message returned because the specified RegionId parameter is invalid.|
|403|InvalidDiskCategory.NotSupported|The specified disk category is not supported.|The error message returned because the specified disk type is not supported.|
|400|InvalidParam.Type|The specified type is not supported.|The error message returned because the specified parameter is invalid.|
|403|InvalidRegion.NotSupport|The specified region does not support resize online.|The error message returned because online resizing is not available in the specified region.|
|403|InvalidDiskCategory.NotSupported|The specified disk category does not support resize online.|The error message returned because online resizing is not supported by the specified disk type.|
|403|IncorrectInstanceStatus|The current status of the resource does not support resize online.|The error message returned because the operation is not supported while the resource is in the current state.|
|403|IncorrectDiskStatus|The current status of the resource does not support resize online|The error message returned because online resizing is not supported while the resource is in the current state.|
|403|InvalidOperation.InstanceTypeNotSupport|The instance type of the specified instance does not support resize online.|The error message returned because online resizing is not supported by the instance to which the disk is attached.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

