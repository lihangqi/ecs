# StopInstance {#doc_api_1161592 .reference}

Stops an ECS instance.

## Description {#description .section}

-   You can only stop an instance which is in the **running** \(`Running`\) state.
-   After you call this operation, the instance enters the **stopping** \(`Stopping`\) state. After the instance is stopped, it is in the **stopped** \(`Stopped`\) state.
-   You can force stop an instance. However, this operation can cause data loss if data in the instance is not yet written to the disk.
-   You cannot stop an ECS instance on which [Security Control](~~25695~~) is enabled and whose `OperationLocks` is tagged as `"LockReason" : "security"`.
-   For an instance on which [Local Disk Storage](~~63138~~) \(Local\_storage\) is configured and which is of the [I1 instance type family](~~25378#i1~~), you must specify `ConfirmStop` and set its value to `True`. Otherwise, an error is returned.
-   For the I1 instance type family, data in the local disk is cleared after the instance is stopped. We recommend that you implement data redundancy at the application layer to guarantee data availability.
-   For instances of other instance type families, the `ConfirmStop` parameter is ignored.
-   If [StopCharging](~~63353~~) is selected, you can configure `StoppedMode=KeepCharging` to KeepCharging. Then the instance is charged after it is stopped. The instance type in stock and public IP address are reserved for this instance.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=StopInstance) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|InstanceId|String|Yes|i-instanceid1| The ID of the instance.

 |
|Action|String|No|StopInstance| The operation that you want to perform. Set the value to StopInstance.

 |
|StoppedMode|String|No|KeepCharging| Indicates whether the ECS instance is still charged after it is stopped. Valid values: KeepCharging

 If [StopCharging](~~63353~~) is selected, you can configure `StoppedMode=KeepCharging` to KeepCharging. Then the instance is charged after it is stopped. The instance type in stock and public IP address are reserved for this instance.

 |
|ForceStop|Boolean|No|false| Indicates whether to stop the instance forcibly. Default values: false.

 |
|ConfirmStop|Boolean|No|true| Indicates whether to confirm the stop operation. This parameter is required and applies only to instances of the I1 instance type family. Default value: false.

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The request ID.

 |

## Examples {#demo .section}

Sample request

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=StopInstance
&InstanceId=i-instanceid1
&ConfirmStop=true
&ForceStop=false
&StoppedMode=keepcharging
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<StopInstanceResponse>
  <RequestId>1C488B66-B819-4D14-8711-C4EAAA13AC01</RequestId>
</StopInstanceResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"1C488B66-B819-4D14-8711-C4EAAA13AC01"
}
```

## Error codes { .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|403|IncorrectInstanceStatus|The current status of the resource does not support this operation.|The error message returned when the operation is not supported while the resource is in the current state.|
|403|InstanceType.ParameterMismatch|The input parameter ConfirmStop must be true when an instance have localstorage.|The error message returned when Local Disk Storage is configured for the instance. The ConfirmStop parameter must be set to true.|
|403|InstanceExpiredOrInArrears|The specified operation is denied as your prepay instance is expired \(prepay mode\) or in arrears \(afterpay mode\).|The error message returned when the subscription instance has expired. Renew the instance first.|
|403|InvalidInstanceId.NotSupport|Classic network Instance does not support this operation.|The error message returned when the operation is not supported in classic instances.|
|403|InvalidInstanceId.NotSupport|Pre pay instance does not support this operation.|The error message returned when the operation is not supported in subscription instances.|
|403|InvalidInstanceId.NotSupport|Local disk instance does not support this operation.|The error message returned when the operation is not supported in local disk instances.|
|403|InvalidInstanceId.NotSupport|Spot instance does not support this operation.|The error message returned when the operation is not supported in preemptible instances.|
|403|IncorrectInstanceStatus|%s|The error message returned when the operation is not supported while the instance is in the current state.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

