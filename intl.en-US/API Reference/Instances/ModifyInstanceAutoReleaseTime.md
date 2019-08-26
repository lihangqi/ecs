# ModifyInstanceAutoReleaseTime {#doc_api_1161583 .reference}

Sets or cancels the automatic release time for a Pay-As-You-Go instance. Use caution when you set the automatic release time, because the instance is automatically released upon expiration.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=ModifyInstanceAutoReleaseTime) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|InstanceId|String|Yes|i-instanceid1| The ID of the instance.

 |
|Action|String|No|ModifyInstanceAutoReleaseTime| The operation that you want to perform. Set the value to **ModifyInstanceAutoReleaseTime**.

 |
|AutoReleaseTime|String|No|2018-01-01T01:02:03Z| The automatic release time of the instance. The time follows the [ISO 8601](~~25696~~) standard and is in UTC time. Format: yyyy-MM-ddTHH:mm:ssZ.

 -   If `ss` is set to a value other than `00`, only the value of `mm` is used, with ss changed to 00.
-   The automatic release time must be at least half an hour later than the current time.
-   The automatic release time must be less than 3 years since the current time.

 If `AutoReleaseTime` is not specified, it indicates that the automatic release attribute is canceled and the ECS instance is not automatically released.

 |
|RegionId|String|No|cn-hangzhou| The region ID of the instance. You can call the [DescribeRegions](~~25609~~) operation to view the latest region list.

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The request ID. The system returns a unique RequestId for each API request, regardless of whether the API operation is successful.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=ModifyInstanceAutoReleaseTime
&InstanceId=i-instance1 
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<ModifyInstanceAutoReleaseTimeResponse>
  <RequestId>04F0F334-1335-436C-A1D7-6C044FE73368</RequestId> 
</ModifyInstanceAutoReleaseTimeResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"C0003E8B-B930-4F59-ADC0-0E209A9012A8"
}
```

## Error codes { .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|400|MissingParameter|InstanceId should not be null.|The error message returned when RegionId is not specified.|
|500|InternalError|The request processing has failed due to some unknown error, exception or failure.|The error message returned when an unknown error occurs.|
|403|ChargeTypeViolation|The operation is not permitted due to charge type of the instance.|The error message returned when this operation is not supported while this billing method is selected.|
|404|NoSuchResource|The specified resource is not found.|The error message returned when the specified resource does not exist.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

