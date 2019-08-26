# DescribeInstanceAutoRenewAttribute {#doc_api_1161575 .reference}

Queries the automatic renewal status of one or more subscription instances.

## Description {#description .section}

Before setting automatic or manual renewal, you can query the automatic renewal status of instances.

This operation is only supported on [subscription](~~56220~~) instances. An error is returned if you call this operation on [Pay-As-You-Go](~~40653~~) instances.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=DescribeInstanceAutoRenewAttribute) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|RegionId|String|Yes|cn-hangzhou| The region ID of the instance. You can call the [DescribeRegions](~~25609~~) operation to view the latest region list.

 |
|Action|String|No|DescribeInstanceAutoRenewAttribute| The operation that you want to perform. Set the value to **DescribeInstanceAutoRenewAttribute**.

 |
|InstanceId|String|No|i-instance1,i-instance2| The ID of the instance. A maximum of 100 subscription instance IDs can be entered at a time. Separate multiple instance IDs with commas \(,\).

 |
|PageNumber|String|No|1| The page number.

 This value starts from 1.

 Default value: 1.

 |
|PageSize|String|No|10| The number of rows per page.

 Maximum value: 100.

 Default value: 10.

 |
|RenewalStatus|String|No|AutoRenewal| The automatic renewal status of the instance. Valid values:

 -   AutoRenewal: enables automatic renewal.
-   Normal: disables automatic renewal.
-   NotRenewal: No renewal is used. The system no longer sends an expiration reminder, but sends only a non-renewal reminder three days before the expiration date. For an instance for which no renewal is used, you can call the [ModifyInstanceAutoRenewAttribute](~~52843~~) operation to change its automatic renewal status to `Normal`. Then you can manually renew it or set it to automatic renewal.

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|InstanceRenewAttributes| | | The renewal attribute set.

 |
|└AutoRenewEnabled|Boolean|false| Indicates whether automatic renewal is enabled.

 |
|└Duration|Integer|1| The automatic renewal period.

 |
|└InstanceId|String|i-instanceid1| The ID of the instance.

 |
|└PeriodUnit|String|week| The unit of the automatic renewal period.

 |
|└RenewalStatus|String|Normal| The automatic renewal status of the instance. Valid values:

 -   AutoRenewal: enables automatic renewal.
-   Normal: disables automatic renewal.
-   NotRenewal: No renewal is used. The system no longer sends an expiration reminder, but sends only a non-renewal reminder three days before the expiration date. For an instance for which no renewal is used, you can call the [ModifyInstanceAutoRenewAttribute](~~52843~~) operation to change its automatic renewal status to `Normal`. Then you can manually renew it or set it to automatic renewal.

 |
|PageNumber|Integer|1| The page number.

 This value starts from 1.

 Default value: 1.

 |
|PageSize|Integer|10| The number of rows per page.

 Maximum value: 100.

 Default value: 10.

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The request ID. The system returns a unique RequestId for each API request, regardless of whether the API operation is successful.

 |
|TotalCount|Integer|6| The total number of instances.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=DescribeInstanceAutoRenewAttribute
&RegionId=cn-hangzhou 
&InstanceId=i-instance1,i-instance2 
&PageNumber=1 
&PageSize=10 
&RenewalStatus=AutoRenewal
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<DescribeInstanceAutoRenewAttributeResponse>
  <RequestId>04F0F334-1335-436C-A1D7-6C044FE73368</RequestId> 
  <InstanceRenewAttributes>
    <InstanceRenewAttribute>
      <Instance> 
        <InstanceId>i-instance1</InstanceId>
        <Duration>0</Duration> 
        <AutoRenewEnalbed>false</AutoRenewEnalbed> 
        <RenewalStatus>Normal</RenewalStatus>
      </Instance> 
      <Instance> 
        <InstanceId>i-instance2</InstanceId>
        <Duration>1</Duration> 
        <AutoRenewEnalbed>true</AutoRenewEnalbed> 
        <RenewalStatus>AutoRenewal</RenewalStatus> 
      </Instance> 
    </InstanceRenewAttribute>
  </InstanceRenewAttributes>
</DescribeInstanceAutoRenewAttributeResponse>

```

`JSON` format

``` {#json_return_success_demo}
{
	"InstanceRenewAttributes":{
		"InstanceRenewAttribute":[
			{
				"RenewalStatus":"Normal",
				"InstanceId":"i-instance1",
				"Duration":0,
				"AutoRenewEnabled":false
			},
			{
				"RenewalStatus":"AutoRenewal",
				"InstanceId":"i-instance2",
				"Duration":1,
				"AutoRenewEnabled":true
			}
		]
	},
	"RequestId":"04F0F334-1335-436C-A1D7-6C044FE73368"
}
```

## Error codes { .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|403|MissingParameter.InstanceId|InstanceId should not be null.|The error message returned when InstanceId is not specified.|
|403|InvalidParameter.InvalidInstanceId|%s|The error message returned when InstanceId is invalid.|
|403|IncorrectInstanceStatus|The current status of the resource does not support this operation.|The error message returned when the operation is not supported while the resource is in the current state.|
|403|InvalidParameter.RenewalStatus|The specified parameter RenewalStatus is not valid.|The error message returned when the specified RenewalStatus is invalid.|
|403|InvalidParameter.RenewalStatusInstanceId|The parameter RenewalStatus and InstanceId cannot be both empty.|The error message returned when both RenewalStatus and InstanceId are not specified.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

