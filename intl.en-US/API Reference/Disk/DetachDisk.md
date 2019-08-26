# DetachDisk {#doc_api_999557 .reference}

Detaches a Pay-As-You-Go disk from an instance. The disk types that support Pay-As-You-Go billing are basic disks, ultra disks, and SSDs.

## Description {#description .section}

When you call this operation, note that:

-   The Portable attribute of the disk must be set to true.
-   The disk to be detached must be in the In\_use state.
-   The instance that the disk is attached to must be in the Running or Stopped state.
-   The instance must not be locked by [security control](~~25695~~). The OperationLocks parameter of the ECS instance must not be set to "LockReason": "security".
-   After the disk is detached from an instance, its DeleteWithInstance attribute will be set to false. Because it is no longer attached to the instance, it can no longer be released together with the instance.
-   The DetachDisk operation is asynchronous. After a response is returned, it will take about a minute before the disk is detached.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=DetachDisk) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|DiskId|String|Yes|d-diskid1| The ID of the disk to be detached.

 |
|InstanceId|String|Yes|i-instanceid1| The ID of the ECS instance from which the disk is to be detached.

 |
|Action|String|No|DetachDisk| The operation that you want to perform. Set the value to DetachDisk.

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=DetachDisk
&DiskId=d-diskid1
&InstanceId=i-instanceid1
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<DetachDiskResponse>
  <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId> 
</DetachDiskResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E"
}
```

## Error codes {#section_9pa_776_y2b .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|403|InstanceLockedForSecurity|The instance is locked due to security.|The error message returned when the specified instance is locked for security reasons and the operation cannot be completed.|
|400|InvalidOperation.InstanceTypeNotSupport|The instance type of the specified instance does not support hot detach disk.|The error message returned when the instance that the disk is attached to does not support the hot swapping of disks.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

