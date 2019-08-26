# ModifyInstanceVncPasswd {#doc_api_1161588 .reference}

Modifies the Web management terminal password of an ECS instance.

## Description {#description .section}

-   The password must be 6 characters in length and can contain only uppercase and lowercase letters and digits.
-   After you modify the password:
    -   For an optimized instance, the new password takes effect immediately.
    -   For a non-optimized instance, you must [restart the instance](~~25440~~) from the console or call the [RebootInstance](~~25502~~) operation to validate the modifications.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=ModifyInstanceVncPasswd) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|InstanceId|String|Yes|i-AY121018033933eae8689| The ID of the instance.

 |
|RegionId|String|Yes|cn-hangzhou| The region ID of the instance. You can call the [DescribeRegions](~~25609~~) operation to view the latest region list.

 |
|VncPassword|String|Yes|123456| The new password of the management terminal.

 |
|Action|String|No|ModifyInstanceVncPasswd| The operation that you want to perform. Set the value to **ModifyInstanceVncPasswd**.

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The request ID.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=ModifyInstanceVncPasswd
&RegionId=cn-hangzhou 
&InstanceId=i-AY121018033933eae8689
&VncPassword=123456 
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<ModifyInstanceVncPasswdResponse>
  <RequestId>FDB6C963-9CE8-4B7F-BCA3-845F6BD29AFC</RequestId>
</ModifyInstanceVncPasswdResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"FDB6C963-9CE8-4B7F-BCA3-845F6BD29AFC"
}
```

## Error codes { .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|403|IncorrectInstanceStatus|The current status of the resource does not support this operation.|The error message returned when the operation is not supported while the resource is in the current state.|
|400|IncorrectVncPassword.Malformed|The specified parameter VncPassword is not valid.|The error message returned when the specified VNC password is invalid.|
|404|NoSuchResource|The specified resource is not found.|The error message returned when the specified resource does not exist.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

