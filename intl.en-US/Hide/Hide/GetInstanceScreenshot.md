# GetInstanceScreenshot {#GetInstanceScreenshot .reference}

Obtains screenshot information of an instance for troubleshooting and diagnosis.

## Description {#BestPractice .section}

We return you the instance screenshot in JPG format, encoded in Base64. However, you can decode the screenshot yourself. We recommend that you use this operation for troubleshooting and diagnosis, and consider the following:

-   The instance must be in the **Running** \(`Running`\) status.
-    [Phased-out instance types](https://www.alibabacloud.com/help/faq-detail/55263.htm) cannot obtain screenshot information.

## Request parameters  {#RequestParameter .section}

|Name|Type|Required|Description |
|:---|:---|:-------|:-----------|
|Action|String|Yes|The name of this interface. Value: GetInstanceScreenshot.|
|RegionId|String|Yes|ID of the region where the ECS instance is located. For more information, use [DescribeRegions](../intl.en-US/API Reference/Regions/DescribeRegions.md#) to obtain the latest region list.|
|InstanceId|String|Yes|Instance ID.|
|Wakeup|Boolean|No|Whether to wake up instances in sleep mode or not.Default value: false.

|

## Response parameters {#ResponseParameter .section}

|Name|Type|Description|
|:---|:---|:----------|
|InstanceId|String|Instance ID.|
|screenshot|String|The JPG format instance screenshot encoded in Base64.|

## Examples { .section}

**Request example** 

```
http://ecs-cn-hangzhou.example.com/?Action=GetInstanceScreenshot
&RegionId=cn-shenzhen
&InstanceId=i-j5e42sbbthlokka11eci
&Wakeup=False
&<Common Request Parameters>
```

**Success response example** 

**XML format**

```
<GetInstanceScreenshotResponse>
    <RequestId>22A1933F-AD02-4560-A6A7-53CF2231D942</RequestId>
    <InstanceId>i-j5e42sbbthlokka11ech</InstanceId>
    <Screenshot>iVBORw0KGgoA... AAABJRU5ErkJggg==</Screenshot>
</GetInstanceScreenshotResponse>
```

**JSON format** 

```
{
    "RequestId": "22A1933F-AD02-4560-A6A7-53CF2231D942",
    "InstanceId": "i-j5e42sbbthlokka11ech",
    "Screenshot": "iVBORw0KGgoA... AAABJRU5ErkJggg=="
}
```

**Error response example** 

**XML format**

```
<Error>
    <RequestId>C38E0D94-C18B-44F3-8C05-6E35BE334088</RequestId>
    <HostId>ecs.aliyuncs.com</HostId>
    <Code>NotSupported</Code>
    <Message>The operation is not supported for "i-j5e42sbbthlokkaXXXXX".</Message>
</Error>
```

**JSON format** 

```
{
    "RequestId": "C38E0D94-C18B-44F3-8C05-6E35BE334088",
    "HostId": "ecs.aliyuncs.com",
    "Code": "NotSupported",
    "Message": "The operation is not supported for "i-j5e42sbbthlokkaXXXXX"."
}
```

## Error codes {#ErrorCode .section}

Error codes specific to this interface are as follows. For more information, see [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

|Error code|Error message|HTTP status code|Description|
|:---------|:------------|:---------------|:----------|
|MissingParameter|The input parameter “instanceId” that is mandatory for processing this request is not supplied.|400|`InstanceId` is required.|
|InvalidParameter|The “instanceId” provided is not valid.|404|The specified `InstanceId` does not exist.|
|IncorrectInstanceStatus|The instance status “\{status\}” is not applicable|405|The instance must be in the **Running** \(`Running`\) status.|
|NotSupported|The operation is not supported for “\{instanceId\}”|405|[Phased-out instance types](https://www.alibabacloud.com/help/faq-detail/55263.htm) cannot obtain screenshot information.|
|Throttling|Request was denied due to request throttling.|400|You have made too many frequent requests in a short time.|

