# AttachDisk {#doc_api_1030732 .reference}

Attaches a data disk to an ECS instance.

## Description {#description .section}

When you call this operation, note that:

-   The operation can be performed only when the instance is in the Running or Stopped state.
-   The data disk to be attached must be in the Available state.
-   The instance must not be locked by [security control](~~25695~~). The OperationLocks parameter of the ECS instance must not be set to "LockReason": "security".
-   If an instance is locked for security reasons \(the OperationLocks parameter is "LockReason": "security"\), the DeleteWithInstance attribute will be ignored and the disk will be released together with the instance.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=AttachDisk) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|DiskId|String|Yes|d-23jbf2v5m| The ID of the disk to be attached. The disk and the instance must belong to the same zone.

 |
|InstanceId|String|Yes|i-instance1| The ID of the ECS instance that the disk is to be attached to.

 |
|Action|String|No|AttachDisk| The operation that you want to perform. Set the value to AttachDisk.

 |
|DeleteWithInstance|Boolean|No|false| Indicates whether the disk is to be released together with the instance. Default value: false.

 |
|Device|String|No|/dev/xvda| The name of the disk. This parameter will be removed in the future. We recommend that you use other parameters to ensure compatibility.

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=AttachDisk
&DiskId=d-23jbf2v5m
&InstanceId=i-instance1 
&DeleteWithInstance=false 
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<AttachDiskResponse>
  <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId> 
</AttachDiskResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E"
}
```

## Error codes {#section_0qw_vss_rft .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|400|InvalidDevice.Malformed|The specified port is not valid.|The error message returned when the specified disk name does not exist.|
|403|InstanceDiskLimitExceeded|The amount of the disk on instance in question reach its limits.|The error message returned when the specified instance is already attached with the maximum number of disks.|
|403|InvalidDevice.InUse|The specified device has been occupied.|The error message returned when the specified device already has an attached disk.|
|403|InstanceLockedForSecurity|The instance is locked due to security.|The error message returned when the specified instance is locked for security reasons and the operation cannot be completed.|
|403|InstanceExpiredOrInArrears|The specified operation is denied as your prepay instance is expired \(prepay mode\) or in arrears \(afterpay mode\).|The error message returned when the subscription of the instance has expired. You must renew the subscription before proceeding.|
|400|IncorrectInstanceStatus|The current status of the resource does not support this operation.|The error message returned when the specified resource is in a state that does not support the current operation.|
|403|DiskError|IncorrectDiskStatus.|The error message returned when the status of the specified disk is invalid.|
|403|DiskId.ValueNotSupported|The specified parameter diskid is not supported.|The error message returned when the specified disk type does not support this operation.|
|403|DiskId.StatusNotSupported|The specified disk status is not supported.|The error message returned when the specified disk is in a state that does not support this operation.|
|404|InvalidDisk.InUse|The specified disk has been occupied.|The error message returned when the specified disk is already in use.|
|403|UserNotInTheWhiteList|The user is not in disk white list.|The error message returned when you are not authorized to use the specified disk.|
|400|InvalidOperation.InstanceTypeNotSupport|The instance type of the specified instance does not support hot attach disk.|The error message returned when the instance that the disk is attached to does not support the hot swapping of disks.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

