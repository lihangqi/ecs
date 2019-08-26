# ModifyInstanceAutoRenewAttribute {#doc_api_1161584 .reference}

Sets one or more subscription instances to the automatic renewal status. To reduce the maintenance workload when an instance expires, you can set automatic renewal for subscription ECS instances.

## Description {#description .section}

-   The payment for automatic renewal is first made at 08:00:00 \(UTC+8\) nine days before the instance expires.
-   If payment fails for the first time, this process repeats itself each day until the payment is made or the instance is locked after the nine-day period ends. You must confirm that your payment account has sufficient balance or credit.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=ModifyInstanceAutoRenewAttribute) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|InstanceId|String|Yes|i-instance1,i-instance2| The ID of the instance. A maximum of 100 instance IDs can be entered at a time. Separate multiple instance IDs with commas \(,\).

 |
|RegionId|String|Yes|cn-hangzhou| The region ID of the instance. You can call the [DescribeRegions](~~25609~~) operation to view the latest region list.

 |
|Action|String|No|ModifyInstanceAutoRenewAttribute| The operation that you want to perform. Set the value to **ModifyInstanceAutoRenewAttribute**.

 |
|AutoRenew|Boolean|No|true| Indicates whether to enable automatic renewal. Default value: false.

 |
|Duration|Integer|No|2| The automatic renewal period.

 -   `PeriodUnit`If it is set to `Year`, `Duration` can be \{"1", "2", "3 "\}.
-   `PeriodUnit`If it is set to `Month`, `Duration` can be \{"1", "2", "3", "6", "12 "\}.

 |
|PeriodUnit|String|No|Week| The unit of `Period`. Default value: month. Valid values:

 -   Month.
-   Year.

 |
|RenewalStatus|String|No|AutoRenewal| Indicates whether to renew the instance. `RenewalStatus` has a higher priority than `AutoRenew`. If `RenewalStatus` is not specified, the value of `AutoRenew` is used by default. Valid values:

 -   AutoRenewal: enables automatic renewal.
-   Normal: disables automatic renewal.
-   NotRenewal: No renewal is used. The system no longer sends an expiration reminder, but sends only a non-renewal reminder three days before the expiration date. For an instance for which no renewal is used, you can change its automatic renewal status to `Normal`. Then you can manually renew it or set it to automatic renewal.

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The request ID.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=ModifyInstanceAutoRenewAttribute
&RegionId=cn-hangzhou 
&InstanceId=i-instance1,i-instance2 
&Duration=2 
&AutoRenew=True 
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<ModifyInstanceAutoRenewAttributeResponse>
  <RequestId>04F0F334-1335-436C-A1D7-6C044FE73368</RequestId> 
</ModifyInstanceAutoRenewAttributeResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"04F0F334-1335-436C-A1D7-6C044FE73368"
}
```

## Error codes { .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|403|MissingParameter.InstanceId|InstanceId should not be null.|The error message returned when InstanceId is not specified.|
|403|InvalidParameter.InvalidInstanceId|%s|The error message returned when the specified InstanceId is invalid.|
|403|IncorrectInstanceStatus|The current status of the resource does not support this operation.|The error message returned when the operation is not supported while the resource is in the current state.|
|403|InvalidParameter.Duration|%s|The error message returned when the Duration parameter is invalid.|
|403|InvalidParameter.RenewalStatus|%s|The error message returned when the RenewalStatus parameter is invalid.|
|403|InvalidPeriodUnit.ValueNotSupported|The specified parameter “Period” is not valid.|The error message returned when the specified PeriodUnit is invalid.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

