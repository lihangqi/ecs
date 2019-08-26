# RebootInstance {#doc_api_1161595 .reference}

Restarts an ECS instance.

## Description {#description .section}

-   You can only restart an ECS instance which is in the **running** \(`Running`\) state.
-   After you restart an ECS instance, it is in the **starting**\(`Starting`\) state.
-   Force restart \(`ForceStop`\) is supported. Force restart can cause data loss if data in the instance is not yet written to the disk.
-   You cannot restart an ECS instance on which [Security Control](~~25695~~) is enabled and whose `OperationLocks` is tagged as `"LockReason" : "security"`.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=RebootInstance) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|InstanceId|String|Yes|i-instance1| The ID of the instance.

 |
|Action|String|No|RebootInstance| The operation that you want to perform. Set the value to RebootInstance.

 |
|ForceStop|Boolean|No|false| Indicates whether to stop the instance forcibly before you restart it. Default value: false.

 |
|DryRun|Boolean|No|false| Indicates whether to send a check request only.

-   true: Only a check request is sent and no instance is restarted. The system checks whether the required parameters are set, and verifies the request format, service limits, and available ECS instances. If the check fails, the corresponding error code is returned. If the check succeeds, the DryRunOperation error code is returned.
-   false \(Default\): A request is sent and then the instance is restarted.

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The request ID.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=RebootInstance
&InstanceId=i-instance1 
&ForceStop=false
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<RebootInstanceResponse>
  <RequestId>F2E2C40D-AB09-45A1-B5C5-EB9F5C4E4E4A</RequestId>
</RebootInstanceResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"F2E2C40D-AB09-45A1-B5C5-EB9F5C4E4E4A"
}
```

## Error codes { .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|403|IncorrectInstanceStatus|The current status of the resource does not support this operation.|The error message returned when the operation is not supported while the resource is in the current state.|
|403|DiskError|IncorrectDiskStatus.|The error message returned when the specified DiskCategory is invalid.|
|403|InstanceExpiredOrInArrears|The specified operation is denied as your prepay instance is expired \(prepay mode\) or in arrears \(afterpay mode\).|The error message returned when the subscription instance has expired. Renew the instance first.|
|403|IncorrectInstanceStatus|%s|The error message returned when the operation is not supported while the instance is in the current state.|

[View more error codes](https://error-center.aliyun.com/status/product/Ecs)

