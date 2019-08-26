# DescribeCloudAssistantStatus {#doc_api_1032107 .reference}

Views whether the cloud assistant client is installed on one or more instances.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=DescribeCloudAssistantStatus) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|InstanceId.N|RepeatList|Yes|i-bp1iudwa5b1tqaxxxxxx| The list of instance IDs. You can query up to 50 instances in each request. Valid values of N: 1 to 50.

 |
|RegionId|String|Yes|cn-hangzhou| The ID of the region where the instance is located. You can call [DescribeRegions](~~25609~~) to view the latest regions of Alibaba Cloud.

 |
|Action|String|No|DescribeCloudAssistantStatus| The operation that you want to perform. Set the value to DescribeCloudAssistantStatus.

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|InstanceCloudAssistantStatusSet| | | A set of installation statuses of the cloud assistant clients on the instances.

 |
|└ CloudAssistantStatus|String|true| Indicates whether the cloud assistant client is installed on the instance.

 |
|└InstanceId|String|i-bp1iudwa5b1tqaxxxxxx| The ID of the instance.

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=DescribeCloudAssistantStatus
&InstanceId. 1=i-bp1iudwa5b1tqaxxxxxx
&RegionId=cn-hangzhou 
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<DescribeCloudAssistantStatusResponse> 
  <InstanceCloudAssitantStatus>
    <InstanceCloudAssitantStatusSet>
      <InstanceId>i-bp11f7trr4hbi1xxxxxx</InstanceId>
      <CloudAssitantStatus>True</CloudAssitantStatus>
    </InstanceCloudAssitantStatusSet>
    <InstanceCloudAssitantStatusSet>
      <InstanceId>i-bp1iudwa5b1tqaxxxxxx</InstanceId>
      <CloudAssitantStatus>True</CloudAssitantStatus>
    </InstanceCloudAssitantStatusSet>
  </InstanceCloudAssitantStatus>
</DescribeCloudAssistantStatusResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"InstanceCloudAssitantStatus":{
		"InstanceCloudAssitantStatusSet":[
			{
				"InstanceId":"i-bp11f7trr4hbi1xxxxxx",
				"CloudAssitantStatus":"True"
			},
			{
				"InstanceId":"i-bp1iudwa5b1tqaxxxxxx",
				"CloudAssitantStatus":"True"
			}
		]
	}
}
```

## Error codes {#section_8xg_zcp_kpy .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|500|InternalError.Dispatch|An error occurs when you dispatched the request.|The error message returned when an unknown error occurs.|
|404|InvalidInstance.NotFound|The specified instance does not exist.|The error message returned when the specified instance does not exist.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

