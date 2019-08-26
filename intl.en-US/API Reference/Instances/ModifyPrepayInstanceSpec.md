# ModifyPrepayInstanceSpec {#doc_api_1161590 .reference}

Changes the type of your subscription instance. The new instance type will take effect for the entire lifecycle of the instance.

## Description {#description .section}

Before you call this operation, make sure that you have fully understood the billing methods and pricing schedule of [ECS](../../../../reseller.en-US/Pricing/Pricing overview.md#). For more information about instance configuration change types, see [Query available resources for configuration changes](../../../../reseller.en-US/SDK Reference/Use API to run ECS/Query available resources for configuration changes.md#).

When you call this operation, note that:

-   The instance must be in the **stopped** \(`Stopped`\) state.
-   The specified instance cannot have overdue payment.
-   Before changing the [subscription](~~56220~~) instance type, you can call the [DescribeResourcesModification](~~66187~~) operation to query the instance types you can change to.
-   For instance type downgrade:
    -   You can downgrade the type of an instance up to three times. The refund for the price difference cannot exceed three times.
    -   The price difference is refunded to the payment account you used. Price difference of coupon purchases are not refunded.
    -   You have to wait for five minutes to initiate another instance type downgrade after a successful downgrade for an instance.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=ModifyPrepayInstanceSpec) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|InstanceId|String|Yes|i-xxxxx1| The ID of the instance.

 |
|InstanceType|String|Yes|ecs.s1.large| The new instance type. For more information, see [Instance type families](~~25378~~), or call the [DescribeInstanceTypes](~~25620~~) operation to obtain the latest instance type list.

 |
|RegionId|String|Yes|cn-hangzhou| The region ID of the instance. You can call the [DescribeRegions](~~25609~~) operation to view the latest region list.

 |
|Action|String|No|ModifyPrepayInstanceSpec| The operation that you want to perform. Set the value to **ModifyPrepayInstanceSpec**.

 |
|AutoPay|Boolean|No|true| Indicates whether to enable automatic payment. When OperatorType is set to downgrade, AutoPay is ignored. Default value: true. Valid values:

 -   true: enables automatic payment. Make sure that your account has sufficient balance. Otherwise, your order becomes invalid and you have to cancel this order.
-   false: No payment is made and only an order is generated. After you change the billing method, AutoPay is set to true. Make sure that your account has sufficient balance. Otherwise, your order becomes invalid and you have to cancel this order. If your account balance is insufficient, you can set **AutoPay** to **false**. Then an order is generated. You can log on to the ECS console to pay for it.

 |
|MigrateAcrossZone|Boolean|No|false| Indicates whether to enable cross-cluster instance type upgrade. Default value: false.

 When MigrateAcrossZone is set to true and you upgrade the instance type based on the returned information, make sure that:

 Classic instances:

 -   For [phased-out instance types](~~55263~~), when a non-optimized instance is upgraded to an optimized instance, the following items are modified: private IP address, driver name, and software authorization code. For Linux instances, basic disks \(cloud\) are identified as xvda or xvdb. Ultra disks \(cloud\_efficiency\) and SSDs \(cloud\_ssd\) are identified as vda or vdb.
-   For [instance type families available on the Alibaba Cloud market](~~25378~~), the private IP is modified after instance type upgrade.

 VPC-type instances: For phased-out instance types, when a non-optimized instance is upgraded to an optimized instance, the following items are modified: driver name and software authorization code. For Linux instances, basic disks \(cloud\) are identified as xvda or xvdb. Ultra disks \(cloud\_efficiency\) and SSDs \(cloud\_ssd\) are identified as vda or vdb.

 |
|OperatorType|String|No|downgrade| The configuration change type. Default value: downgrade. Valid values:

 -   upgrade \(Default\): When `OperatorType` is set to `upgrade`, make sure that your payment account has sufficient balance or credit.
-   downgrade.

 |
|SystemDisk.Category|String|No|cloud\_efficiency| System disk change option. This parameter is valid only when you upgrade one of the [phased-out instance types](~~55263~~) to one of the [instance type families available on the Alibaba Cloud market](~~25378~~) and upgrade a non-optimized instance to an optimized instance. Valid values:

 -   cloud\_efficiency: ultra disk.
-   cloud\_ssd: SSD.

 |
|ClientToken|String|No|123e4567-e89b-12d3-a456-426655440000| The token used to ensure idempotence. You can generate the token in your client, but you must ensure that it is globally unique.**ClientToken** can contain only ASCII characters. It must be no more than 64 characters in length. For more information, see [How to ensure idempotence](~~25693~~).

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|OrderId|String|1111111111111111111111110| The ID of the order.

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The request ID.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=ModifyPrepayInstanceSpec
&RegionId=cn-hangzhou 
&InstanceId=i-xxxxx1 
&InstanceType=ecs.s1.large 
&AutoPay=true 
&OperatorType=upgrade 
&ClientToken=xxxxxxxxxxxxxx 
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<ModifyPrepayInstanceSpecResponse>
  <RequestId>04F0F334-1335-436C-A1D7-6C044FE73368</RequestId> 
  <OrderId>1011111111111111</OrderId> 
</ModifyPrepayInstanceSpecResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"OrderId":1011111111111111,
	"RequestId":"04F0F334-1335-436C-A1D7-6C044FE73368"
}
```

## Error codes { .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|400|InvalidInstanceType.ValueNotSupported|The specified InstanceType does not exist or beyond the permitted range.|The error message returned when the specified instance type is not supported.|
|500|InternalError|The request processing has failed due to some unknown error, exception or failure.|The error message returned when an unknown error occurs.|
|400|InvalidBillingMethod.ValueNotSupported|The operation is not permitted due to an invalid billing method of the instance.|The error message returned when the operation is not supported due to the invalid billing method for the instance.|
|400|InvalidInstanceId.Released|The specified instance has been released.|The error message returned when the instance has been released.|
|400|InvalidInstance.PurchaseNotFound|The specified instance has no purchase history.|The error message returned when the order record for this instance does not exist.|
|400|Account.Arrearage|Your account has an outstanding payment.|The error message returned when you have unpaid orders under your account.|
|403|InvalidUser.PassRoleForbidden|The RAM user does not have privilege to pass a role.|The error message returned when RAM users attempt to assign RAM roles.|
|400|InvalidRebootTime.MalFormed|The specified rebootTime is not valid.|The error message returned when the specified RebootTime is invalid.|
|403|ImageNotSupportInstanceType|The specified image does not support the specified InstanceType.|The error message returned when the specified instance type is not supported in the specified image.|
|403|InstanceType.Offline|%s|The error message returned when the specified instance type is unavailable.|
|400|IdempotenceParamNotMatch|Request uses a client token in a previous request but is not identical to that request.|The error message returned when ClientToken in this request is not identical to the one used in the previous request.|
|403|IncorrectInstanceStatus|The current status of the resource does not support this operation.|The error message returned when the operation is not supported while the resource is in the current state.|
|400|IdempotenceParamNotMatch|%s|The error message returned when the idempotent signatures are inconsistent.|
|400|InvalidInstanceChargeType.ValueNotSupported|%s|The error message returned when the specified billing method is not supported.|
|400|InvalidStatus.NotStopped|Instance status must be stopped.|The error message returned when the instance is not in the stopped state.|
|400|InvalidAction|%s|The error message returned when the operation is invalid.|
|400|InstanceDowngrade.QuotaExceed|Quota of instance downgrade is exceed.|The error message returned when the maximum number of instance type downgrades for the instance is reached.|
|400|InvalidInstanceType.ValueNotSupported|%s|The error message returned when the instance type attribute is incorrect.|
|403|InvalidParameter.InstanceId|%s|The error message returned when the specified InstanceId is invalid.|
|400|InvalidParameter|%s|The error message returned when the parameter format is incorrect.|
|403|ImageNotSupportInstanceType|The specified instanceType is not supported by instance with marketplace image.|The error message returned when the marketplace image does not support the instance type.|
|403|InvalidInstanceStatus|The current status of the instance does not support this operation.|The error message returned when the operation is not supported while the instance is in the current state.|
|403|InvalidInstance.PreInstanceExpired|Instance business status is not Expired|The error message returned when the instance status is incorrect.|
|403|InvalidInstance.EipNotSupport|The special instance with eip not support operate, please unassociate eip first.|The error message returned when the operation is not supported while an EIP has been bound to this instance. Unbind the EIP first.|
|403|InvalidOperation.Ipv4CountExceeded|%s|The error message returned when the maximum number of IPv4 addresses is reached.|
|403|InvalidOperation.Ipv6CountExceeded|%s|The error message returned when the maximum number of IPv6 addresses is reached.|
|403|InvalidOperation.Ipv6NotSupport|%s|The error message returned when IPv6 addresses are not supported by the instance type.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

