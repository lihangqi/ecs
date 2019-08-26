# RenewInstance {#doc_api_1161591 .reference}

Renews a subscription ECS instance.

## Description {#description .section}

When you call this operation, note that:

-   Only subscription ECS instances are supported.
-   The renew operation will use available coupons under your account by default. This does not apply to discount accounts.
-   You must confirm that your payment account has sufficient balance or credit.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=RenewInstance) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|InstanceId|String|Yes|i-instance1| The ID of the instance.

 |
|Period|Integer|Yes|1| The renewal period of the subscription instance. If **DedicatedHostId** is specified, the value range of the Period parameter must be within the subscription period of the DDH. Valid values:

 -   1 to 12, 24, 36, 48, and 60 if PeriodUnit is set to Month.

 |
|Action|String|No|RenewInstance| The operation that you want to perform. Set the value to **RenewInstance**.

 |
|OwnerAccount|String|No|happyCustomer| The logon name of the RAM user.

 |
|PeriodUnit|String|No|Month| The unit of the renewal period \(**Period**\). Default value: Month. Valid values:

 -   Month.

 |
|ClientToken|String|No|0c593ea1-3bea-11e9-b96b-88e9fe637760| The token used to ensure idempotence. You can generate the token in your client, but you must ensure that it is globally unique.**ClientToken** can contain only ASCII characters. It must be no more than 64 characters in length. For more information, see [How to ensure idempotence](~~25693~~).

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The request ID.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=RenewInstance
&InstanceId=i-instance1 
&Period=1 
&PeriodUnit=Month 
&ClientToken=0c593ea1-3bea-11e9-b96b-88e9fe637760
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<ModifyInstanceSpecResponse> 
  <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId> 
</ModifyInstanceSpecResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E"
}
```

## Error codes { .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|400|InvalidInternetChargeType.ValueNotSupported|The specified InternetChargeType is not valid.|The error message returned when the specified instance type does not exist.|
|400|IdempotenceParamNotMatch|Request uses a client token in a previous request but is not identical to that request.|The error message returned when ClientToken in this request is not identical to the one used in the previous request.|
|403|ChargeTypeViolation|The operation is not permitted due to charge type of the instance.|The error message returned when this operation is not supported while this billing method is selected.|
|400|InvalidInstanceType.ValueNotSupported|The specified InstanceType does not exist or beyond the permitted range.|The error message returned when the specified instance type is not supported.|
|403|IncorrectInstanceStatus|The current status of the resource does not support this operation.|The error message returned when the operation is not supported while the resource is in the current state.|
|400|InvalidInternetChargeType.InstanceNotSupported|The specified instance which is in vpc is not support the parameter InternetChargeType.|The error message returned when the specified billing method is not supported in the specified VPC-type instance.|
|400|Invalidperiod|The specified period is not valid.|The error message returned when the specified period is invalid.|
|403|Instance.UnPaidOrder|The specified instance has unpaid order.|The error message returned when you have unpaid orders under the specified instance.|
|400|OperationDenied|Specified instance is in VPC.|The error message returned when the specified instance is in a VPC.|
|400|InvalidParameter|The specified parameter " InternetMaxBandwidthOut " is not valid.|The error message returned when the specified InternetMaxBandwidthOut is invalid.|
|400|DependencyViolation.InstanceType|Current instancetype cannot be changed to the specified one.|The error message returned when the current instance type is modified to the specified one.|
|400|InvalidPeriodUnit.ValueNotSupported|The specified parameter PeriodUnit is not valid.|The error message returned when the specified PeriodUnit is invalid.|
|400|InvalidDedicatedHostId.NotFound|The specified DedicatedHostId does not exist.|The error message returned when the specified DDH ID does not exist.|
|400|InvalidDedicatedHostStatus.NotSupport|Operation denied due to dedicated host status|The error message returned when the operation is not supported while the resource is in the current state.|
|400|IncorrectDedicatedHostStatus|The current status of the resource does not support this operation.|The error message returned when the operation is not supported while the resource is in the current state.|
|400|InvalidPeriod.ExceededDedicatedHost|Instance expired date can't exceed dedicated host expired date.|The error message returned when the expiration date of the instance is later than that of the DDH.|
|400|InvalidStatus.Upgrading|The instance is upgrading; please try again later.|The error message returned when the specified instance is being upgraded. Try again later.|
|400|InvalidPeriod.ExceededMaximumExpirationDate|The specified renewal period cannot exceed the maximum expiration date. We recommend you try shortening the renewal period at next attempt.|The error message returned when the specified renewal period is later than the maximum expiration date.|
|400|LastOrderProcessing|The previous order is still processing, please try again later.|The error message returned when the order is being processed. Try again later.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

