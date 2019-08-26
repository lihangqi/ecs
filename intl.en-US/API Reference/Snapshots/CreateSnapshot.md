# CreateSnapshot {#doc_api_Ecs_CreateSnapshot .reference}

You can call this operation to create a snapshot for a disk.

## Description {#description .section}

-   A maximum of 64 snapshots can be created for a single disk.
-   The instance to which the disk is attached must be in the **stopped** \(`Stopped`\) or **running** \(`Running`\) state. Otherwise, the snapshot cannot be created.
-   The disk for which you want to create a snapshot must be attached to an instance.
-   If the instance to which a specified disk is attached has never been started, the snapshot cannot be created.
-   If an ECS instance is locked for [security control](~~25695~~) \(the `OperationLocks` parameter is `"LockReason" : "security"`\), no snapshots can be created for its attached disks.
-   If you have called the [RunInstances](~~63440~~), [ReplaceSystemDisk](~~25521~~), or [CreateDisk](~~25513~~) operation and data has not yet been loaded to the disk, no snapshots can be created. You can create a snapshot about one hour after you create an ECS instance or replace the system disk. The time to wait after you add a data disk before you can create a snapshot depends on the size of the disk data.
-   If a snapshot is still being created, you cannot create another snapshot for the same disk.
-   If a snapshot is still being created, this snapshot cannot be used to create a custom image \([CreateImage](~~25535~~)\).
-   It is allowed to create snapshots for an **expired** \(`Expired`\) subscription cloud disk. Note that if you are creating snapshots while the cloud disk is being deleted, the snapshots that are in the **creating** \(`Creating`\) state are also deleted.

## Debugging {#apiExplorer .section}

Alibaba Cloud provides [OpenAPI Explorer](https://api.aliyun.com/#product=Ecs&api=CreateSnapshot) to simplify API usage. You can use OpenAPI Explorer to search for APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|DiskId|String|Yes|d-diskid1|The ID of the cloud disk for which a snapshot is to be created.

 |
|Action|String|No|CreateSnapshot|The operation that you want to perform. Set the value to CreateSnapshot. If the request HTTP or HTTPS URL contains different parameters, `Action` is required.

 |
|SnapshotName|String|No|FinanceJoshua|The name of the snapshot to be created. The name must be 2 to 128 characters in length. It must start with a letter and cannot start with http:// or https://. It can contain letters, digits, colons \(:\), underscores \(\_\), and hyphens \(-\).

 It cannot start with auto, because snapshot names starting with auto are recognized as automatic snapshots.

 |
|Description|String|No|FinanceDepet|The description of the snapshot to be created. The description must be 2 to 256 characters in length and cannot start with http:// or https://.

 Default value: null

 |
|RetentionDays|Integer|No|30|The retention period of the snapshot to be created. Valid values: 1 to 65,536. Unit: day. The snapshot will be automatically released when the retention period expires.

 Default value: null, indicating that the snapshot will not be released automatically.

 |
|Tag.N.value|String|No|FinanceDept.Joshua|The tag value of the snapshot to be created.

 **Note:** This parameter will be removed in the future. We recommend that you use the Tag.N.Value parameter to ensure compatibility.

 |
|Tag.N.key|String|No|FinanceDept|The tag key of the snapshot to be created.

 **Note:** This parameter will be removed in the future. We recommend that you use the Tag.N.Key parameter to ensure compatibility.

 |
|Tag.N.Key|String|No|FinanceDept|The tag key of the snapshot to be created. Valid values of N: 1 to 20. It cannot be an empty string. It can be up to 64 characters in length and cannot start with aliyun or acs:. It cannot contain http:// or https://.

 |
|Tag.N.Value|String|No|FinanceDept.Joshua|The tag value of the snapshot to be created. Valid values of N: 1 to 20. The tag value can be an empty string. It can be up to 128 characters in length and cannot start with aliyun or acs:. It cannot contain http:// or https://.

 |
|ClientToken|String|No|123e4567-e89b-12d3-a456-426655440000|The client token that is used to ensure the idempotence of the request. You can use the client to generate this value, but you must ensure that it is unique among different requests. The **ClientToken** parameter can contain only ASCII characters, and cannot exceed 64 characters in length. For more information, see [How to ensure idempotence](~~25693~~).

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request.

 |
|SnapshotId|String|s-snapshotid1|The ID of the snapshot created.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=CreateSnapshot
&DiskId=d-diskid1
&SnapshotName=FinanceJoshua
&Description=FinanceDepet
&ClientToken=123e4567-e89b-12d3-a456-426655440000
&Tag. 1.Key=FinanceDept
&Tag. 1.Value=FinanceDept.Joshua
&<Common request parameters>
```

Sample success responses

`XML` format

``` {#xml_return_success_demo}
<CreateSnapshotResponse>
  <RequestId>C8B26B44-0189-443E-9816-D951F59623A9</RequestId>
  <SnapshotId>s-923FE2B**</SnapshotId>
</CreateSnapshotResponse>

```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"C8B26B44-0189-443E-9816-D951F59623A9",
	"SnapshotId":"s-923FE2B**"
}
```

## Error codes { .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|404|InvalidDiskId.NotFound|The specified DiskId does not exist.|The error message returned because the specified DiskId parameter does not exist. Check whether the DiskId parameter is correct.|
|400|InvalidSnapshotName.Malformed|The specified SnapshotName is wrongly formed.|The error message returned because the format of the specified SnapshotName parameter is invalid. The name must be 2 to 128 characters in length. It can contain letters, digits, colons \(:\), underscores \(\_\), and hyphens \(-\). It must start with a letter and cannot start with http:// or https://.|
|404|InvalidDescription.Malformed|The specified description is wrongly formed.|The error message returned because the format of the specified Description parameter is invalid. The description must be 2 to 256 characters in length and cannot start with http:// or https://.|
|400|IncorrectInstanceStatus|The current status of the resource does not support this operation.|The error message returned because the operation is not supported while the resource is in the current state.|
|403|IncorrectDiskStatus.CreatingSnapshot|A previous snapshot creation is in process.|The error message returned because another snapshot is being created. Wait until the snapshot is created and try again.|
|403|InstanceLockedForSecurity|The disk attached instance is locked due to security.|The error message returned because the instance to which the disk is attached is locked to ensure security.|
|403|IncorrectDiskStatus.NeverAttached|The specified disk has never been attached to any instance.|The error message returned because the specified disk has not been attached to any instances and its content remains unchanged.|
|403|QuotaExceed.Snapshot|The snapshot quota exceeds.|The error message returned because the maximum number of snapshots is reached. To create new snapshots, delete any unnecessary snapshots without affecting your business.|
|403|IncorrectDiskStatus.NeverUsed|The specified disk has never been used after creating.|The error message returned because the disk has not been used after being created and its content remains unchanged.|
|403|CreateSnapshot.Failed|The process of creating snapshot is failed.|The error message returned because the snapshot has failed to be created.|
|403|DiskInArrears|The specified operation is denied as your disk has expired.|The error message returned because the disk has expired due to overdue payment.|
|500|InternalError|The request processing has failed due to some unknown error.|The error message returned because an internal error has occurred. Try again later. If the problem persists, submit a ticket.|
|403|DiskId.ValueNotSupported|The specified parameter diskid is not supported.|The error message returned because the operation is not supported by the current disk type.|
|400|DiskCategory.OperationNotSupported|The operation is not supported to the specified disk due to its disk category|The error message returned because the operation is not supported by the specified disk type.|
|403|IncorrectDiskStatus|The current disk status does not support this operation.|The error message returned because the operation is not supported while the disk is in the current state. Ensure that the disk is available and has no overdue payments.|
|403|InvalidAccountStatus.NotEnoughBalance|Your account does not have enough balance.|The error message returned because your account balance is insufficient. Top up your account and try again.|
|403|InvalidAccountStatus.SnapshotServiceUnavailable|Snapshot service has not been opened yet.|The error message returned because the operation is not supported while the snapshot service is not enabled.|
|404|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|The error message returned because the specified InstanceId parameter does not exist.|
|403|IncorrectVolumeStatus|The current volume status does not support this operation.|The error message returned because the operation is not supported while the shared block storage device is in the current state.|
|404|InvalidVolumeId.NotFound|The specified volume does not exist.|The error message returned because the specified VolumeId parameter does not exist.|
|403|IdempotentParameterMismatch|The specified clientToken is used.|The error message returned because the specified token is in use.|
|403|IncorrectDiskStatus.Invalid|The specified device status invalid, restart instance and try again.|The error message returned because the specified disk status is invalid. Restart the instance and try again.|
|403|IncorrectDiskType.NotSupport|The specified device type is not supported.|The error message returned because the operation is not supported by the specified disk type.|
|403|IncorrectDiskStatus.Transferring|The specified device is transferring, you can retry after the process is finished.|The error message returned because the specified disk is being migrated. Wait until the disk is migrated and try again.|
|403|InvalidParameter.KMSKeyId.KMSUnauthorized|ECS service have no right to access your KMS.|The error message returned because ECS is not authorized to access your KMS resources.|
|500|InternalError|The request processing has failed due to some unknown error, exception or failure.|The error message returned because an internal error has occurred.|
|400|Duplicate.TagKey|The Tag.N.Key contain duplicate key.|The error message returned because the specified tag key is not unique.|
|400|InvalidTagKey.Malformed|The specified Tag.n.Key is not valid.|The error message returned because the specified Tag.N.Key parameter is invalid.|
|400|InvalidTagValue.Malformed|The specified Tag.n.Value is not valid.|The error message returned because the specified Tag.N.Value parameter is invalid.|
|403|IdempotentProcessing|The previous idempotent request\(s\) is still processing.|The error message returned because the previous idempotence request is being processed.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

