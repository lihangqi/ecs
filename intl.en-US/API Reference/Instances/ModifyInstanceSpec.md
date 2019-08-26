# ModifyInstanceSpec {#doc_api_1161587 .reference}

Changes the instance type or public bandwidth of a Pay-As-You-Go instance.

## Description {#description .section}

Before you call this operation, make sure that you have fully understood the billing methods and pricing schedule of [ECS](../../../../reseller.en-US/Pricing/Pricing overview.md#). For more information about instance configuration change types, see [Query available resources for configuration changes](../../../../reseller.en-US/SDK Reference/Use API to run ECS/Query available resources for configuration changes.md#).

When you call this operation, note that:

-   The instance must has no overdue payment.
-   You can change the public bandwidth only when the instance is in the **running** \(`Running`\) or **stopped** \(`Stopped`\) state.
-   Before changing the Pay-As-You-Go instance type, you can call the [DescribeResourcesModification](~~66187~~) operation to query the instance types you can change to.
-   You can change the instance type only when the instance is in the **stopped** \(`Stopped`\) state.
-   You can only change either the instance type or the public bandwidth each time.
-   After a successful downgrade, you must wait five minutes before you can initiate another instance type downgrade.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=ModifyInstanceSpec) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|InstanceId|String|Yes|i-instanceid1| The ID of the instance.

 |
|Action|String|No|ModifyInstanceSpec| The operation that you want to perform. Set the value to **ModifyInstanceSpec**.

 |
|AllowMigrateAcrossZone|Boolean|No|false| Indicates whether to enable cross-cluster instance type upgrade. Default value: **false**

 When **AllowMigrateAcrossZone** is set to **true** and you upgrade the instance type based on the returned information, make sure that:

 Classic instances:

 -   For [phased-out instance types](~~55263~~), when a non-optimized instance is upgraded to an optimized instance, the following items are modified: private IP address, driver name, and software authorization code. For Linux instances, basic disks \(**cloud**\) are identified as **xvda** or **xvdb**. Ultra disks \(**cloud\_efficiency**\) and SSDs \(**cloud\_ssd**\) are identified as **vda** or **vdb**.
-   For [instance type families available on the Alibaba Cloud market](~~25378~~), the private IP is modified after instance type upgrade.

 VPC-type instances: For [phased-out instance types](~~55263~~), when a non-optimized instance is upgraded to an optimized instance, the following items are modified: driver name and software authorization code. For Linux instances, basic disks \(**cloud**\) are identified as **xvda** or **xvdb**. Ultra disks \(**cloud\_efficiency**\) and SSDs \(`cloud_ssd`\) are identified as **vda** or **vdb**.

 |
|Async|Boolean|No|false| Indicates whether to submit an asynchronous request.

 Default value: false.

 |
|InstanceType|String|No|ecs.g5.large| The new instance type. For more information, see [Instance type families](~~25378~~), or call the [DescribeInstanceTypes](~~25620~~) operation to obtain the latest instance type list.

 |
|InternetMaxBandwidthIn|Integer|No|200| The maximum inbound bandwidth for the public network. Unit: Mbit/s. Valid values: 1 to 200.

 |
|InternetMaxBandwidthOut|Integer|No|10| The maximum outbound bandwidth for the public network. Unit: Mbit/s. Valid values: 0 to 100.

 |
|SystemDisk.Category|String|No|cloud\_ssd| System disk change option. This parameter is only valid when you upgrade one of the [phased-out instance types](~~55263~~) to one of the [instance type families available on the Alibaba Cloud market](~~25378~~) and upgrade a non-optimized instance to an optimized instance. Valid values:

 -   cloud\_efficiency: ultra disk.
-   cloud\_ssd: SSD.

 |
|Temporary.EndTime|String|No|2017-12-05T22:40:00Z| The end time of the temporary bandwidth upgrade. The time follows the [ISO 8601](~~25696~~) standard and is in UTC time. Format: yyyy-MM-ddTHH:mm:ssZ.

 **Note:** This parameter will be removed in the future. We recommend that you use other parameters to ensure compatibility.

 |
|Temporary.InternetMaxBandwidthOut|Integer|No|50| The maximum outbound bandwidth for the public network after temporary bandwidth upgrade. Valid values: 1 to 100.

 **Note:** This parameter will be removed in the future. We recommend that you use other parameters to ensure compatibility.

 |
|Temporary.StartTime|String|No|2017-12-05T22:40:00Z| The start time of the temporary bandwidth upgrade. The time follows the [ISO 8601](~~25696~~) standard and is in UTC time. Format: yyyy-MM-ddTHH:mm:ssZ.

 **Note:** This parameter will be removed in the future. We recommend that you use other parameters to ensure compatibility.

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
https://ecs.aliyuncs.com/?Action=ModifyInstanceSpec
&InstanceId=i-xxxxx1 
&InstanceType=ecs.s1.large 
&InternetMaxBandwidthOut=10 
&InternetMaxBandwidthIn=100 
&ClientToken=xxxxxxxxx 
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<ModifyInstanceSpecResponse> 
  <RequestId>04F0F334-1335-436C-A1D7-6C044FE73368</RequestId> 
</ModifyInstanceSpecResponse> 
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
|400|InvalidInternetChargeType.ValueNotSupported|The specified InternetChargeType is not valid.|The error message returned when the specified instance type does not exist.|
|400|InvalidInstanceType.ValueUnauthorized|The specified InstanceType does not exist or beyond the permitted range.|The error message returned when the specified instance type is not supported.|
|400|InvalidInstanceType.ValueNotSupported|The specified InstanceType does not exist or beyond the permitted range.|The error message returned when the specified instance type is not supported.|
|400|InvalidParameter.Mismatch|Too many parameters in one request.|The error message returned when the request contains too many parameters.|
|403|CategoryViolation|The specified instance does not support this operation because of its disk category.|The error message returned when configurations are changed for instances with local disks attached.|
|403|InvalidStatus.ValueNotSupported|The current status of the resource does not support this operation.|The error message returned when the operation is not supported while the resource is in the current state.|
|500|InternalError|The request processing has failed due to some unknown error, exception or failure.|The error message returned when an unknown error occurs.|
|403|InvalidAccountStatus.NotEnoughBalance|Your account does not have enough balance.|The error message returned when your account has insufficient balance.|
|403|ChargeTypeViolation|The operation is not permitted due to charge type of the instance.|The error message returned when this operation is not supported while this billing method is selected.|
|400|BandwidthUpgradeDenied.EipBoundInstance|The specified VPC instance has bound EIP, temporary bandwidth upgrade is denied.|The error message returned when temporary bandwidth upgrade is not supported while an EIP has been bound to this instance.|
|404|MissingTemporary.StartTime|Temporary.StartTime is not specified.|The error message returned when the start time of the temporary bandwidth upgrade is not specified.|
|404|MissingTemporary.EndTime|Temporary.EndTime is not specified.|The error message returned when the end time of the temporary bandwidth upgrade is not specified.|
|400|InvalidTemporary.StartTime|The specifed Temporary.StartTime is not valid.|The error message returned when the start time of the temporary bandwidth upgrade is invalid.|
|400|InvalidTemporary.EndTime|The specifed Temporary.EndTime is not valid.|The error message returned when the end time of the temporary bandwidth upgrade is invalid.|
|400|Downgrade.NotSupported|Downgrade operation is not supported.|The error message returned when configuration downgrade is not supported.|
|400|DependencyViolation.InstanceType|The current InstanceType cannot be changed to the specified InstanceType.|The error message returned when the instance cannot be changed to the specified instance type.|
|403|InvalidInstanceType.ValueNotSupported|The specified zone does not offer the specified instancetype.|The error message returned when the specified instance type is not supported.|
|400|Account.Arrearage|Your account has an outstanding payment.|The error message returned when you have unpaid orders under your account.|
|400|InvalidParameter.AllowMigrateAcrossZone|The specified parameter CanMigrateAcrossZone is not valid.|The error message returned when the specified CanMigrateAcrossZone is invalid.|
|400|InvalidParam.SystemDiskCategory|The specified param SystemDisk.Category is not valid.|The error message returned when the specified SystemDisk.Category is invalid.|
|403|InstanceType.Offline|The specified InstanceType has been offline|The error message returned when the instance type is unavailable on the Alibaba Cloud market.|
|400|IdempotenceParamNotMatch|There is a idempotence signature mismatch between this and last request.|The error message returned when the idempotent signatures are inconsistent.|
|403|InvalidParameter.NotMatch|%s|The error message returned when the parameter is in conflict with another parameter.|
|403|InvalidInstance.EipNotSupport|The specified instance with eip is not supported, please unassociate eip first.|The error message returned when the operation is not supported while an EIP has been bound to this instance. Unbind the EIP first.|
|400|InvalidAction.NotSupport|The ecs on dedicatedHost not support modify instanceType.|The error message returned when the instance on the DDH does not support instance type change.|
|403|InvalidOperation.Ipv4CountExceeded|%s|The error message returned when the maximum number of IPv4 addresses is reached.|
|403|InvalidOperation.Ipv6CountExceeded|%s|The error message returned when the maximum number of IPv6 addresses is reached.|
|403|InvalidOperation.Ipv6NotSupport|%s|The error message returned when IPv6 addresses are not supported by the instance type.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

