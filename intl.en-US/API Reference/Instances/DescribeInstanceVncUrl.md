# DescribeInstanceVncUrl {#doc_api_Ecs_DescribeInstanceVncUrl .reference}

You can call this operation to query the Web management terminal URL of an ECS instance.

## Description {#description .section}

When you call this operation, note that:

-   A management terminal URL is only valid for 15 seconds. If a connection is not established within 15 seconds after a successful query, the URL expires and you must query it again.
-   The **KeepAlive** time of a management terminal connection is 60 seconds. If you do not interact with the management terminal within 60 seconds, the management terminal will be automatically disconnected.
-   When the management terminal is disconnected, you can only reconnect to the management terminal up to 30 times a minute.
-   At the end of [https://g.alicdn.com/aliyun/ecs-console-vnc2/0.0.5/index.html?](https://g.alicdn.com/aliyun/ecs-console-vnc2/0.0.5/index.html?), add `vncUrl=xxxx`, `instanceId=xxx`, `isWindows=True`, `isWindows=False`, and `password=XXXXXX`. Connect these parameters with `&`. Where:
    -   `vncUrl`: The value of `VncUrl` is returned after a successful query.
    -   `instanceId`: the ID of instance to be queried.
    -   `isWindows`: specifies whether the operating system of the instance is Windows. The value of `true` indicates the Windows system. The value of `false` indicates that the Windows system is not used.
    -   `password`: Optional. The password to establish a remote connection from the instance. It must be six characters in length and can contain digits and uppercase and lowercase letters. This parameter eliminates the need to enter a password on the management terminal when a connection is being established.

        Example:

        ```
        
               https://g.alicdn.com/aliyun/ecs-console-vnc2/0.0.5/index.html?vncUrl=ws%3A%2F%xxx&instanceId=i-wz9hhwq5a6tmxxxxxxx&isWindows=true
               
        ```

        or

        ```
        
               https://g.alicdn.com/aliyun/ecs-console-vnc2/0.0.5/index.html?vncUrl=ws%3A%2F%xxx&instanceId=i-wz9hhwq5a6tmxxxxxxx&isWindows=true&password=111111
               
        ```


## Debugging {#apiExplorer .section}

Alibaba Cloud provides [OpenAPI Explorer](https://api.aliyun.com/#product=Ecs&api=DescribeInstanceVncUrl) to simplify API usage. You can use OpenAPI Explorer to search for APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|InstanceId|String|Yes|i-AY121018033933eaxxxxxxx|The ID of the instance to be queried.

 |
|RegionId|String|Yes|cn-hangzhou|The region ID of the instance. You can call the [DescribeRegions](~~25609~~) operation to query the latest region list.

 |
|Action|String|No|DescribeInstanceVncUrl|The operation that you want to perform. Set the value to DescribeInstanceVncUrl.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request.

 |
|VncUrl|String|ws%3A%2F%2Fhz01-vncproxy.aliyun.com%2Fwebsockify%2F%3Fs%3DDvh%252FIA%252BYc73gWO48cBx2gBxUDVzaAnSKr74pq30mzqUYgeUMcB%252FbkNixDxdEA996|The management terminal URL.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=DescribeInstanceVncUrl
&InstanceId=i-AY121018033933eaxxxxxxx
&RegionId=cn-hangzhou
&<Common request parameters>
```

Sample success responses

`XML` format

``` {#xml_return_success_demo}
<DescribeInstanceVncUrlResponse>
  <RequestId>1450F2D7-5435-4420-BBC9-49C5xxxxxxxx</RequestId>
  <VncUrl>ws%3A%2F%2Fhz01-vncproxy.aliyun.com%2Fwebsockify%2F%3Fs%3DDvh%252FIA%252BYc73gWO48cBx2gBxUDVzaAnSKr74pq30mzqUYgeUMcB%252FbkNixDxdEA996</VncUrl>
</DescribeInstanceVncUrlResponse>

```

`JSON` format

``` {#json_return_success_demo}
{
	"VncUrl":"ws%3A%2F%2Fhz01-vncproxy.aliyun.com%2Fwebsockify%2F%3Fs%3DDvh%252FIA%252BYc73gWO48cBx2gBxUDVzaAnSKr74pq30mzqUYgeUMcB%252FbkNixDxdEA996",
	"RequestId":"1450F2D7-5435-4420-BBC9-49C5xxxxxxxx"
}
```

## Error codes { .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|404|InvalidRegionId.NotFound|The specified RegionId does not exist.|The error message returned because the specified RegionId parameter does not exist.|
|404|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|The error message returned because the specified InstanceId parameter does not exist.|
|403|IncorrectInstanceStatus|The current status of the resource does not support this operation.|The error message returned because the operation is not supported while the resource is in the current state.|
|500|InternalError|The request processing has failed due to some unknown error.|The error message returned because an internal error has occurred. Try again later. If the problem persists, submit a ticket.|
|403|InstanceNotReady|The specified instance is not ready for use|The error message returned because the operation is not supported while the resource is in the current state. Retry the operation after a few minutes.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

