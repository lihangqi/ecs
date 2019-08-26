# ReInitDisk {#doc_api_1030734 .reference}

Resets a disk to its initial state .

## Description {#description .section}

When you call this operation, note that:

-   The operation can be performed only when the disk is in the In\_use state and the instance that the disk is attached to is in the Stopped state.
-   If the instance has not been activated for the first time after creation, the disks attached to it cannot be reinitialized.
-   A system disk will be initialized to the initial status of the image. If the source image used to create the disk is deleted, the disk cannot be initialized.
-   A user-created data disk will be initialized to the state of an empty data disk.
-   A data disk that was created from a snapshot will be initialized to the state of the snapshot. If the source snapshot used to create the disk is deleted, the disk cannot be initialized and an error will be returned.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=ReInitDisk) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|DiskId|String|Yes|d-diskid1| The ID of the disk.

 |
|Action|String|No|ReInitDisk| The operation that you want to perform. Set the value to ReInitDisk.

 |
|AutoStartInstance|Boolean|No|true| Indicates whether to start the instance after the disk is reinitialized.

 |
|KeyPairName|String|No|JoshuaCentOS| The name of the key pair.

 |
|Password|String|No|EcsV587!| The new password of the instance.

 **Note:** If the Password parameter is specified, use HTTPS to call the operation to avoid password leakage.

 The password must be 8 to 30 characters in length and must contain uppercase or lowercase letters, digits, and special characters. The password of a Windows instance cannot start with a forward slash \(/\). The password can contain any of the following special characters:

 ``` {#codeblock_sz0_x8t_jjk}
()` ~! @#$%^&*-_+=|{}[]:;‘<>,.? /
```

 |
|SecurityEnhancementStrategy|String|No|Active| Indicates whether to enable security hardening and install Alibaba Cloud Security on the system disk. Valid values:

 -   Active: enables security hardening and installs Alibaba Cloud Security for free. This value is applicable to only public images.
-   Deactive: disables security hardening and does not install Alibaba Cloud Security. This value is applicable to all images.

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=ReInitDisk
&DiskId=d-diskid1
&Password=EcsV587!
&KeyPairName=JoshuaCentOS
&AutoStartInstance=true
&SecurityEnhancementStrategy=Active
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<ReInitDiskResponse>
  <RequestId>F3CD6886-D8D0-4FEE-B93E-1B73239673DE</RequestId>
</ReInitDiskResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"F3CD6886-D8D0-4FEE-B93E-1B73239673DE"
}
```

## Error codes {#section_0bu_6sb_cyb .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|403|IncorrectInstanceStatus|The current status of the resource does not support this operation.|The error message returned when the specified resource is in a state that does not support the current operation.|
|403|InstanceLockedForSecurity|The instance is locked due to security.|The error message returned when the specified instance is locked for security reasons and the operation cannot be completed.|
|403|InvalidSnapshot.TooOld|The disk is created from a snapshotId made before 2013-07-15, it cannot be re-initiated the specified disk any more since the detached first time.|The error message returned when the specified snapshot is created on or before July 15, 2013.|
|403|OperationDenied|The snapshot which is used to create the specified disk has been deleted.|The error message returned when the snapshot used to create the specified disk does not exist.|
|403|InstanceExpiredOrInArrears|The specified operation is denied as your prepay instance is expired \(prepay mode\) or in arrears \(afterpay mode\).|The error message returned when the subscription of the instance has expired. You must renew the subscription before proceeding.|
|403|DiskCreatingSnapshot|The operation is denied due to a snapshot of the specified disk is not completed yet.|The error message returned when a snapshot of the specified disk is being created.|
|403|InvalidSourceSnapshot|The snapshot which is used to create the specified disk has been deleted.|The error message returned when the snapshot used to create the specified disk has been deleted.|
|404|InvalidImageId.NotFound|The specified ImageId does not exist.|The error message returned when the specified image does not exist under this account. Check whether the image ID is correct.|
|404|InvalidDiskId.OperationNotSupported|The operation is not supported due to image not exist.|The error message returned when the specified image does not exist.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

