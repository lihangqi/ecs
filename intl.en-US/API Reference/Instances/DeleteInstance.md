# DeleteInstance {#doc_api_1161573 .reference}

Releases a Pay-As-You-Go instance or a subscription instance that expires.

## Description {#description .section}

-   After an instance is released, all the physical resources used by the instance are reclaimed. The data is erased and cannot be restored. The attached data disks with the `DeleteWithInstance=True` value will be released, but their automatic snapshots are retained. This depends on the value of `DeleteAutoSnapshot`. If the value is `DeleteAutoSnapshot=false`, their automatic snapshots are retained. If the value is `DeleteAutoSnapshot=true`, their automatic snapshots are released.
-   For an ECS instance on which [Security Control](~~25695~~) is enabled and whose `OperationLocks` is tagged as `"LockReason" : "security"`, even if `DeleteWithInstance` of attached data disks is set to `False`, this value will be ignored and attached data disks will be released.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=DeleteInstance) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|InstanceId|String|Yes|i-instance1| The ID of the instance.

 |
|Action|String|No|DeleteInstance| The operation that you want to perform. Set the value to DeleteInstance.

 |
|Force|Boolean|No|false| Indicates whether to forcibly release an instance which is in the **running** \(`Running`\) state. Default value: false. Valid values:

 -   true: forcibly releases an instance which is in the **running** \(`Running`\) state. When this value is selected, temporary data in the memory and storage for the instance is erased and cannot be restored.
-   false: You can select this value only for an instance which is in the **stopped** \(`Stopped`\) state.

 |
|TerminateSubscription|Boolean|No|false| Indicates whether to release an expired subscription instance. Default value: false.

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The request ID.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=DeleteInstance
&InstanceId=i-instance1 
&Force=false
&TerminateSubscription=false
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<DeleteInstanceResponse>
  <RequestId>928E2273-5715-46B9-A730-238DC996A533</RequestId>
</DeleteInstanceResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"928E2273-5715-46B9-A730-238DC996A533"
}
```

## Error codes { .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|403|IncorrectInstanceStatus|The current status of the resource does not support this operation.|The error message returned when the operation is not supported while the resource is in the current state.|
|403|ChargeTypeViolation|The operation is not permitted due to charge type of the instance.|The error message returned when this operation is not supported while this billing method is selected.|
|400|DependencyViolation.RouteEntry|Specified instance is used by route entry.|The error message returned when custom routing rules still exist in the VPC.|
|400|InvalidParameter|The input parameter InstanceId is invalid.|The error message returned when the specified InstanceId is invalid. Check whether the InstanceId exists and is correct.|
|403|IncorrectInstanceStatus.Initializing|The specified instance status does not support this operation.|The error message returned when the instance is being initialized and cannot be released. Try again later.|
|403|IncorrectInstanceStatus|The specified instance is still attached by volumes.|The error message returned when the specified instance still has data volumes.|
|403|InvalidOperation.DeletionProtection|%s|The error message returned when release protection is enabled for the instance.|
|403|InvalidOperation.NotInWhiteList|%s|The error message returned when the parameter is not in the whitelist.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

