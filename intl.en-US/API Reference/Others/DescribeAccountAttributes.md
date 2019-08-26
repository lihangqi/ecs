# DescribeAccountAttributes {#doc_api_Ecs_DescribeAccountAttributes .reference}

You can call this operation to query the upper limit of ECS resources that you can create in a region. You can query the maximum number of security groups, ENIs, pay-as-you-go instance vCPUs, preemptible instance vCPUs, and Dedicated Hosts \(DDHs\). You can also obtain information such as network types available in the region and whether an account has passed real-name authentication.

## Description {#description .section}

After [registering](https://account.alibabacloud.com/register/intl_register.htm) for an Alibaba Cloud account, you can create a certain number of ECS resources in different regions. For more information, see [Limits](~~25412~~).

You can also [submit a ticket](https://workorder-intl.console.aliyun.com/#/ticket/createIndex) to raise the resource usage limit.

## Debugging {#apiExplorer .section}

Alibaba Cloud provides [OpenAPI Explorer](https://api.aliyun.com/#product=Ecs&api=DescribeAccountAttributes) to simplify API usage. You can use OpenAPI Explorer to search for APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|RegionId|String|Yes|cn-hangzhou|The ID of the region for which to query the upper limit of ECS resources. You can call the [DescribeRegions](~~25609~~) operation to query the latest region list.

 |
|Action|String|No|DescribeAccountAttributes|The operation that you want to perform. For API requests using the HTTP and HTTPS methods, `Action` is required. Set the value to DescribeAccountAttributes.

 |
|ZoneId|String|No|cn-hangzhou-b|The ID of the zone.

 |
|AttributeName.N|RepeatList|No|max-security-groups|The types of resources whose upper limit is to be queried. Valid values of N: 1 to 8. Valid values:

 -   instance-network-type: the available network types in the current region
-   max-security-groups: the number of security groups
-   max-elastic-network-interfaces: the number of ENIs in the current region
-   max-postpaid-instance-vcpu-count: the number of vCPU cores of pay-as-you-go instances in the current region
-   max-spot-instance-vcpu-count: the number of vCPU cores of preemptible instances in the current region
-   max-dedicated-hosts: the number of DDHs in the current region
-   supported-postpaid-instance-types: the types of pay-as-you-go I/O optimized instances in the current region
-   max-axt-command-count: the number of Cloud Assistant commands in the current region
-   max-axt-invocation-daily: the number of Cloud Assistant commands that can be run per day in the current region
-   real-name-authentication: whether the account has passed real-name authentication

**Note:** You must pass real-name authentication before you can create an ECS instance.


 Default value: null.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|AccountAttributeItems| | |A set of information about account privileges in a specified region.

 |
|└AttributeName|String|max-security-groups|The returned resource types. Valid values:

 -   instance-network-type: the available network types in the current region
-   max-security-groups: the number of security groups
-   max-elastic-network-interfaces: the number of ENIs in the current region
-   max-postpaid-instance-vcpu-count: the number of vCPU cores of pay-as-you-go instances in the current region
-   max-spot-instance-vcpu-count: the number of vCPU cores of preemptible instances in the current region
-   max-dedicated-hosts: the number of DDHs in the current region
-   supported-postpaid-instance-types: the types of pay-as-you-go I/O optimized instances in the current region
-   real-name-authentication: whether the account has passed real-name authentication
-   max-axt-command-count: the number of Cloud Assistant commands in the current region
-   max-axt-invocation-daily: the number of Cloud Assistant commands that can be run per day in the current region

 |
|└AttributeValues| | |The upper limit of resources.

 |
|└Count|Integer|3|The number of resource types.

 |
|└ExpiredTime|String|2019-01-01T12:30:00Z|The time when the privileges expired. This parameter is only returned when account privileges have an expiration time. The time follows the [ISO 8601](~~25696~~) standard in the yyyy-MM-ddThh:mmZ format. The time is displayed in UTC.

 |
|└InstanceChargeType|String|PrePaid|The billing method of the instance.

 |
|└InstanceType|String|\["ecs.g5.large"\]|The instance type.

 |
|└Value|String|800|The upper limit of the resource type in the current region or all regions. Valid values:

 -   When the value of the AttributeName parameter is max-security-groups, max-elastic-network-interfaces, max-postpaid-instance-vcpu-count, max-dedicated-hosts, or max-spot-instance-vcpu-count, 0 or a positive integer is returned.
-   When the value of the AttributeName parameter is supported-postpaid-instance-types, the instance type is returned. For more information, see [Instance type families](~~25378~~).
-   When the value of the AttributeName parameter is real-name-authentications, yes, none, or unnecessary is returned.
-   When the value of the AttributeName parameter is instance-network-type, vpc or classic is returned.

 |
|└ZoneId|String|cn-hangzhou-b|The ID of the zone.

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=DescribeAccountAttributes
&RegionId=cn-hangzhou
&ZoneId=cn-hangzhou-b
&AttributeName. 1=max-security-groups
&<Common request parameters>
```

Sample success responses

`XML` format

``` {#xml_return_success_demo}
<DescribeAccountAttributesResponse>
    <AccountAttributeItems>
        <AccountAttributeItem>
            <AttributeName>max-security-groups</AttributeName>
            <AttributeValues>
                <ValueItem>
                    <Value>800</Value>
                <ValueItem>
            </AttributeValues>
        </AccountAttributeItem>
          <AccountAttributeItem>
            <AttributeName>instance-network-type</AttributeName>
            <AttributeValues>
                <ValueItem>
                    <Value>vpc</Value>
                    <Value>classic</Value>
                <ValueItem>
            </AttributeValues>
        </AccountAttributeItem>
     </AccountAttributeItems>
    <RequestId>675B6D89-A3EB-4987-BAF3-610591E0D019</RequestId>
</DescribeAccountAttributesResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"AccountAttributeItems":{
		"AccountAttributeItem":[
			{
				"AttributeValues":{
					"ValueItem":[
						{
							"Value":"100"
						}
					]
				},
				"AttributeName":"max-security-groups"
			},
			{
				"AttributeValues":{
					"ValueItem":[
						{
							"Value":"2"
						}
					]
				},
				"AttributeName":"max-dedicated-hosts"
			},
			{
				"AttributeValues":{
					"ValueItem":[
						{
							"Value":"1000"
						}
					]
				},
				"AttributeName":"max-postpaid-instance-vcpu-count"
			},
			{
				"AttributeValues":{
					"ValueItem":[
						{
							"Value":"1000"
						}
					]
				},
				"AttributeName":"max-spot-instance-vcpu-count"
			},
			{
				"AttributeValues":{
					"ValueItem":[
						{
							"Value":"5000"
						}
					]
				},
				"AttributeName":"max-elastic-network-interfaces"
			},
			{
				"AttributeValues":{
					"ValueItem":[
						{
							"Value":"yes"
						}
					]
				},
				"AttributeName":"real-name-authentication"
			},
			{
				"AttributeValues":{
					"ValueItem":[
						{
							"Value":"vpc"
						}
					]
				},
				"AttributeName":"instance-network-type"
			},
			{
				"AttributeValues":{
					"ValueItem":[
						{
							"Value":"ecs.f3-c16f1.4xlarge"
						},
						{
							"Value":"ecs.g5.2xlarge"
						}
					]
				},
				"AttributeName":"supported-postpaid-instance-types"
			}
		]
	},
	"RequestId":"8CE45CD5-31FB-47C2-959D-CA8144CE9F42"
}
```

## Error codes { .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|403|Invalid.Parameter|The required parameter regionId must be not null.|The error message returned because a required parameter is not specified.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

