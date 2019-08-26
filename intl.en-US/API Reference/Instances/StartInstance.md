# StartInstance {#doc_api_1161593 .reference}

Starts an ECS instance.

## Description {#description .section}

-   The instance must be in the **stopped** \(`Stopped`\) state.
-   After the instance is started, it is in the **starting**\(`Starting`\) state.
-   You cannot start an ECS instance on which [Security Control](~~25695~~) is enabled and whose `OperationLocks` is tagged as `"LockReason" : "security"`.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=StartInstance) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|InstanceId|String|Yes|i-instanceid1| The ID of the instance.

 |
|Action|String|No|StartInstance| The operation that you want to perform. Set the value to StartInstance.

 |
|InitLocalDisk|Boolean|No|false| Indicates whether to restore the initial health status of the instance. It is applicable to those instances of the [instance type families](~~25378~~) that contain local disks such as D1, I1, and I2. If a local disk of the D1, I1, or I2 instance type fails, you can use this parameter to restore the initial health status of the instance when you start the instance. After that, all data in the local disk will be lost. Default value: false.

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The request ID.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=StartInstance
&InstanceId=i-instanceid1
&InitLocalDisk=false
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<StartInstanceResponse>
  <RequestId>C0003E8B-B930-4F59-ADC0-0E20xxxxxxxx</RequestId>
</StartInstanceResponse> 
```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"C0003E8B-B930-4F59-ADC0-0E20xxxxxxxx"
}
```

## Error codes { .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|403|IncorrectInstanceStatus|The current status of the resource does not support this operation.|The error message returned when the operation is not supported while the resource is in the current state.|
|403|DiskError|IncorrectDiskStatus.|The error message returned when the specified DiskCategory is invalid.|
|403|InstanceExpired|The postPaid instance has been expired. Please ensure your account have enough balance.|The error message returned when the Pay-As-You-Go instance is stopped due to overdue payment.|
|403|InstanceExpired|The prePaid instance has been expired.|The error message returned when the Pay-As-You-Go instance is stopped due to overdue payment.|
|403|InstanceNotReady|The specified instance is not ready for use|The error message returned when the operation is not supported while the resource is in the current state. Retry the operation after a few minutes.|
|403|IncorrectInstanceStatus|%s|The error message returned when the operation is not supported while the instance is in the current state.|
|403|InvalidParameter.KMSKeyId.KMSUnauthorized|ECS service have no right to access your KMS.|The error message returned when ECS is not authorized to access your KMS.|
|500|InternalError|The request processing has failed due to some unknown error, exception or failure.|The error message returned when an unknown error occurs.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

