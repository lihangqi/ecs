# ConvertNatPublicIpToEip {#doc_api_1030609 .reference}

Converts the public IP address of a VPC-connected ECS instance to an Elastic IP \(EIP\) address.

## Description {#description .section}

When you call this operation, note that:

-   The network type of the instance must be VPC.
-   The ECS instance must be in either Stopped or Running state.
-   The operation fails if no public IP address is assigned to the ECS instance.
-   The operation fails if the ECS instance is bound to an EIP.
-   The operation fails if the ECS instance has any inactivated specification changes.
-   The operation fails if the instance expires in 24 hours.
-   After you convert the public IP address to an EIP address, EIP is billed separately.
-   The operation fails if the [public network bandwidth](~~25411~~) of the [subscription-based](~~56220~~) ECS instance is billed by bandwidth.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=ConvertNatPublicIpToEip) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|InstanceId|String|Yes|i-test| The ID of the instance for which you want to convert its public IP address to an EIP address.

 |
|RegionId|String|Yes|cn-hangzhou| The ID of the region where the instance resides. You can call [DescribeRegions](~~25609~~) to view the latest regions of Alibaba Cloud.

 |
|Action|String|No|ConvertNatPublicIpToEip| The operation that you want to perform. Set the value to ConvertNatPublicIpToEip.

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=ConvertNatPublicIpToEip
&RegionId=cn-hangzhou 
&InstanceId=i-test
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<ConvertNatPublicIpToEipResponse>
  <RequestId>B154D309-F3E1-4AB7-BA94-FEFCA8B89001</RequestId>
</ConvertNatPublicIpToEipResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"B154D309-F3E1-4AB7-BA94-FEFCA8B89001"
}
```

## Error codes {#section_43n_4f2_u99 .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|403|InvalidInstanceId.PlanedChange|%s|The error message returned when the instance has incomplete changes.|
|403|InvalidInstanceStatus.Released|%s|The error message returned when the specified instance state is invalid.|
|403|IncorrectInstanceStatus|%s|The error message returned when the specified resource is in a state that does not support the current operation.|
|404|InvalidInstanceId.NotFound|%s|The error message returned when the specified instance does not exist.|
|403|InvalidInternetChargeType.ValueNotSupported|%s|The error message returned when the InternetChargeType parameter is invalid.|
|403|MaxEIPQuotaExceeded|The number of EIP exceeds the limit per region.|The error message returned when the number of EIPs exceeds the limit in the region.|
|403|InvalidInstance.OverduePayment|%s|The error message returned when an account has overdue payments. You need to top up your account before proceeding.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

