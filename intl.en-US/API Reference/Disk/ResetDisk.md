# ResetDisk {#doc_api_1030729 .reference}

Rolls back a disk to the specific disk status by using one of its snapshots.

## Description {#description .section}

When you call this operation, note that:

-   The operation can be performed only when the disk is in the In\_use state.
-   The instance that the specified disk is attached to must be in the Stopped state.
-   The specified snapshot must be created from the disk specified by the DiskId parameter.
-   The instance must not be locked by [security control](~~25695~~) \(the OperationLocks parameter is "LockReason": "security"\).

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=ResetDisk) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|DiskId|String|Yes|d-diskid1| The ID of the disk.

 |
|SnapshotId|String|Yes|s-snapshotid1| The ID of the snapshot that is used to roll back the disk to a specific state.

 |
|Action|String|No|ResetDisk| The operation that you want to perform. Set the value to ResetDisk.

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=ResetDisk
&DiskId=d-diskid1
&SnapshotId=s-snapshotid1
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<ResetDiskResponse>
  <RequestId>F3CD6886-D8D0-4FEE-B93E-1B73239673DE</RequestId>
</ResetDiskResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"F3CD6886-D8D0-4FEE-B93E-1B73239673DE"
}
```

## Error codes {#section_5kh_q3n_s35 .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|404|Disk.NotFound|The specified disk does not exist.|The error message returned when the specified disk does not exist. Check whether the disk ID is correct.|
|403|IncorrectInstanceStatus|The current status of the resource does not support this operation.|The error message returned when the specified resource is in a state that does not support the current operation.|
|403|InstanceLockedForSecurity|The instance is locked due to security.|The error message returned when the specified instance is locked for security reasons and the operation cannot be completed.|
|403|InvalidParameter.Mismatch|The specified snapshot is not created from the specified disk.|The error message returned when the specified snapshot was not created from the specified disk.|
|403|InvalidSnapshot.TooOld|The snapshotId is created before 2013-07-15, it cannot be restored since the first time the disk detached.|The error message returned when the specified snapshot was created on or before July 15, 2013.|
|403|InstanceExpiredOrInArrears|The specified operation is denied as your prepay instance is expired \(prepay mode\) or in arrears \(afterpay mode\).|The error message returned when the subscription of the instance has expired. You must renew the subscription before proceeding.|
|403|OperationDenied|The specified snapshot does not support ResetDisk.|The error message returned when the specified snapshot does not support the ResetDisk operation.|
|403|InvalidSnapshotId.NotReady|The specified snapshot has not completed yet.|The error message returned when the specified snapshot is being created.|
|403|InvalidAccountStatus.NotEnoughBalance|Your account does not have enough balance.|The error message returned when your account balance is insufficient. You must top up your account before proceeding.|
|403|Operation.Conflict|The operation may conflicts with others.|The error message returned when the specified operation conflicts with other operations.|
|403|UserNotInTheWhiteList|The user is not in disk white list.|The error message returned when you are not authorized to use the specified disk.|
|500|InternalError|The request processing has failed due to some unknown error, exception or failure.|The error message returned when an unknown error occurred.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

