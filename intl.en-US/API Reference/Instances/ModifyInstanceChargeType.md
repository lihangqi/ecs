# ModifyInstanceChargeType {#doc_api_1161589 .reference}

Changes the billing method for one or more instances. You can change the billing method between Pay-As-You-Go and subscription, or change all Pay-As-You-Go data disks attached to an instance to subscription ones.

## Description {#description .section}

When you call this operation, note that:

-   The instance must be in the **running**\(`Running`\) or **stopped**\(`Stopped`\) state and has no overdue payment.
-   **From subscription to Pay-As-You-Go**:
    -   Users that achieve a certain level of trust can change the billing method from subscription to Pay-As-You-Go.
    -   After you change the billing method from subscription to Pay-As-You-Go, the new billing method will take effect for the entire lifecycle of the instance. The price difference is refunded to the payment account you used. Price difference of coupon purchases are not refunded.
    -   **Refund rule**: You can only freely use a certain amount of refund within a month, and the refund that is not used within the current month will not be accumulated to the next month. After you have used up the refund amount for this month, you can only change the billing method when the next month arrives. The refund amount incurred when you change billing methods is calculated with the following formula: **Number of vCPUs × \(Number of remaining days × 24 ± Number of remaining or elapsed hours\)**.
-   **From Pay-As-You-Go to subscription**:
    -   You can change all Pay-As-You-Go data disks attached to an instance to subscription ones.
    -   This operation cannot be called if the automatic release time has been set for the Pay-As-You-Go instance.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=ModifyInstanceChargeType) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|InstanceIds|String|Yes|\["i-xxxxx1","i-xxxxx2"\]| The ID of the instance. The value can be a JSON array that consists of multiple instance IDs. Separate multiple instance IDs with commas \(`,`\). A maximum of 20 IDs can be entered at a time.

 |
|RegionId|String|Yes|cn-hangzhou| The region ID of the instance. You can call the [DescribeRegions](~~25609~~) operation to view the latest region list.

 |
|Action|String|No|ModifyInstanceChargeType| The operation that you want to perform. Set the value to **ModifyInstanceChargeType**.

 |
|AutoPay|Boolean|No|false| Indicates whether to enable automatic payment. When OperatorType is set to downgrade, AutoPay is ignored. Default value: true. Valid values:

 -   true: enables automatic payment. Make sure that your account has sufficient balance. Otherwise, your order becomes invalid and you have to cancel this order.
-   false: No payment is made and only an order is generated. After you change the billing method, AutoPay is set to true. Make sure that your account has sufficient balance. Otherwise, your order becomes invalid and you have to cancel this order. If your account balance is insufficient, you can set **AutoPay** to **false**. Then, an order is generated. You can log on to the ECS console to pay for it.

 |
|DryRun|Boolean|No|false| Indicates whether to send a check request only. Default value: false.

 -   true: Only a check request is sent and no query is performed. The system checks whether your AccessKey is valid, whether RAM users are authorized, and whether the required parameters are set. If the check fails, the corresponding error code is returned. If the check succeeds, the `DryRunOperation` error code is returned.
-   false: A request is sent and then the query is performed if the 2XX HTTP status code is returned.

 |
|IncludeDataDisks|Boolean|No|true| Indicates whether to change all Pay-As-You-Go data disks attached to the instance to subscription ones. Default value: true.

 |
|InstanceChargeType|String|No|PrePaid| The new billing method. Default value: PrePaid. Valid values:

 -   PrePaid: Subscription.
-   PostPaid: Pay-As-You-Go.

 |
|Period|Integer|No|2| The renewal period of the subscription instance. If DedicatedHostId is specified, the value range of the Period parameter must be within the subscription period of the DDH. Valid values:

 -   `If PeriodUnit is set to Month,``Period` can be \{ “1”, “2”, “3”, “4”, “5”, “6”, “7”, “8”, “9”, “12”, “24”, “36”,”48”,”60”\}

 |
|PeriodUnit|String|No|Month| The unit of `Period`. Default value: Month. Valid values:

 -   Month.

 |
|ClientToken|String|No|123e4567-e89b-12d3-a456-426655440000| The token used to ensure idempotence. You can generate the token in your client, but you must ensure that it is globally unique.**ClientToken** can contain only ASCII characters. It must be no more than 64 characters in length. For more information, see [How to ensure idempotence](~~25693~~).

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|OrderId|String|10111111111xxxxx| The ID of the order.

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The request ID.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=ModifyInstanceChargeType
&RegionId=cn-hangzhou 
&InstanceIds=["i-xxxxx1","i-xxxxx2"] 
&Period=1 
&PeriodUnit=Month 
&AutoPay=false 
&IncludeAllDisks=true 
&ClientToken=xxxxxxxxxxxxxx 
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<ModifyInstanceChargeTypeResponse>
  <RequestId>04F0F334-1335-436C-A1D7-6C044FExxxxx</RequestId>
  <OrderId>10111111111xxxxx</OrderId> 
</ModifyInstanceChargeTypeResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"OrderId":"10111111111xxxxx",
	"RequestId":"04F0F334-1335-436C-A1D7-6C044FExxxxx"
}
```

## Error codes { .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|400|InvalidParameter.InstanceIds|The specified InstanceIds are invalid.|The error message returned when the specified instance is invalid.|
|400|InvalidParameter|%s|The error message returned when the parameter format is incorrect.|
|400|InvalidStatus.ValueNotSupported|%s|The error message returned when the operation is not supported while the resource is in the current state.|
|400|InvalidInstanceChargeType.ValueNotSupported|%s|The error message returned when the specified billing method is not supported.|
|403|InvalidInstance.TempBandwidthUpgrade|Cannot switch to Pay-As-You-Go during the period of temporary bandwidth upgrade.|The error message returned when you change the billing method to Pay-As-You-Go during temporary bandwidth upgrade.|
|400|InvalidInternetChargeType.ValueNotSupported|%s|The error message returned when the parameter is invalid.|
|403|InvalidInstanceType.ValueNotSupported|The specified InstanceType does not exist or beyond the permitted range.|The error message returned when the specified instance type is not supported.|
|403|InstanceType.Offline|%s|The error message returned when the specified instance type is unavailable.|
|500|InternalError|The request processing has failed due to some unknown error, exception or failure.|The error message returned when an unknown error occurs.|
|400|ReleaseTimeHaveBeenSet|The specified instance has been set released time.|The error message returned when the automatic release time has been set for the specified instance.|
|403|InvalidAccountStatus.NotEnoughBalance|Your account does not have enough balance.|The error message returned when your account has insufficient balance.|
|403|Account.Arrearage|Your account has an outstanding payment.|The error message returned when you have unpaid orders under your account.|
|403|InvalidParameter.NotMatch|%s|The error message returned when the parameter is in conflict with another parameter.|
|403|InvalidAction|%s|The error message returned when the operation is invalid.|
|400|Throttling|%s|The error message returned when the request is denied due to request throttling.|
|400|InvalidParameter.Bandwidth|%s|The error message returned when the parameter is invalid.|
|400|InvalidPeriod.UnitMismatch|The specified Period must be correlated with the PeriodUnit.|The error message returned when the specified renewal period and its unit do not match.|
|400|InvalidImageType.NotSupported|%s|The error message returned when the specified image type is invalid.|
|400|InvalidPeriod.ExceededDedicatedHost|Instance expired date can't exceed dedicated host expired date.|The error message returned when the expiration date of the instance is later than that of the DDH.|
|400|InvalidMarketImageChargeType.NotSupport|The specified chargeType of marketImage is unsupported.|The error message returned when the billing method for marketplace images is invalid.|
|403|ImageNotSupportInstanceType|The specified instanceType is not supported by instance with marketplace image.|The error message returned when the marketplace image does not support the instance type.|
|403|InvalidInstanceType.PhasedOut|This instanceType is no longer offered.|The error message returned when the instance type is unavailable on the Alibaba Cloud market.|
|400|InvalidSystemDiskCategory.ValueNotSupported|%s|The error message returned when the parameter is invalid.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

