# InstallCloudAssistant {#doc_api_1031584 .reference}

Installs the cloud assistant client on one or more instances.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=InstallCloudAssistant) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|InstanceId.N|RepeatList|Yes|InstanceID1| The ID of the instance. Valid values of N: 1 to 20.

 |
|RegionId|String|Yes|cn-hangzhou| The ID of the region where the instance is located. You can call [DescribeRegions](~~25609~~) to view the latest regions of Alibaba Cloud.

 |
|Action|String|No|InstallCloudAssistant| The operation that you want to perform. Set the value to InstallCloudAssistant.

**Note:** After you call InstallCloudAssistant and [RebootInstance](~~25502~~) in sequence, the cloud assistant client takes effect.

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=InstallCloudAssistant
&InstanceId.1=["i-bp11f7trr4hbi1xxxxxx", "i-bp1iudwa5b1tqaxxxxxx"]
&RegionId=cn-hangzhou 
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<DeleteInstanceResponse>
  <RequestId>928E2273-5715-46B9-A730-238DC996A533</RequestId>
</DeleteInstanceResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"928E2273-5715-46B9-A730-238DC996A533"
}
```

## Error codes {#section_qgd_cno_rcb .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|500|InternalError.Dispatch|An error occurred when you dispatched the request.|The error message returned when an unknown error occurs.|
|404|InvalidInstance.NotFound|The specified instance does not exist.|The error message returned when the specified instance does not exist.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

