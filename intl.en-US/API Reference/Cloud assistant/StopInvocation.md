# StopInvocation {#doc_api_1101311 .reference}

Stops the process of a running cloud assistant command on one or more ECS instances.

## Description {#description .section}

-   If you stop the process of a one-time invocation command, the invocations that have already started are not interrupted. Invocations that have not started are canceled.
-   If you stop the process of a periodic invocation command, the invocations that have already started are not interrupted. However, the invocation does not start in the next period.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=StopInvocation) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|InvokeId|String|Yes|t-7d2a745b412b4601b2d47f6a768d3a14| The invocation ID of the command process. You can call [DescribeInvocations](~~64840~~) to view all the invocation IDs.

 |
|RegionId|String|Yes|cn-hangzhou| The ID of the region. You can call [DescribeRegions](~~25609~~) to view the latest regions of Alibaba Cloud.

 |
|Action|String|No|StopInvocation| The operation that you want to perform. Set the value to StopInvocation.

 |
|InstanceId.N|RepeatList|No|i-uf614fhehhzmxdqx| The list of instances where the command needs to be stopped. You can specify up to 50 instance IDs in each request. Valid values of N: 1 to 50.

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=StopInvocation
&InvokeId=t-7d2a745b412b4601b2d47f6a768d3a14
&RegionId=cn-hangzhou 
&InstanceId.1=i-uf614fhehhzmxdqx
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<StopInvocationResponse>
  <RequestId>E69EF3CC-94CD-42E7-8926-F133B86387C0</RequestId> 
</StopInvocationResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"E69EF3CC-94CD-42E7-8926-F133B86387C0"
}
```

## Error codes {#section_hwq_j8m_i3h .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|500|InternalError.Dispatch|An error occurred when you dispatched the request.|The error message returned when an unknown error occurs.|
|404|InvalidInvokeId.NotFound|The specified invoke ID does not exist.|The error message returned when the specified InvokeId parameter does not exist.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

