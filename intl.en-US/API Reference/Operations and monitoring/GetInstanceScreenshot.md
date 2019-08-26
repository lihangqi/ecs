# GetInstanceScreenshot {#doc_api_999429 .reference}

Obtains screenshot information of an instance.

## Description {#description .section}

The system returns an instance screenshot in JPG format, encoded in Base64. However, you must decode the screenshot yourself. We recommend that you use this operation for troubleshooting and diagnosis, and take note of the following points:

-   The instance must be in the Running state.
-   For [phased-out instance types](~~55263~~), you cannot obtain screenshot information.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=GetInstanceScreenshot) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|InstanceId|String|Yes|i-myInstance| The ID of the instance.

 |
|RegionId|String|Yes|cn-shenzhen| The ID of the region where the instance is located. You can call [DescribeRegions](~~25609~~) to view the latest regions of Alibaba Cloud.

 |
|Action|String|No|GetInstanceScreenshot| The operation that you want to perform. Set the value to GetInstanceScreenshot.

 |
|WakeUp|Boolean|No|false| Indicates whether to wake up instances in sleep mode.

 Default value: false.

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|InstanceId|String|i-myInstance| The ID of the instance.

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request.

 |
|Screenshot|String|iVBORw0KGgoA... AAABJRU5ErkJggg==| The JPG format instance screenshot, which is encoded in Base64.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
http://ecs-cn-hangzhou.example.com/?Action=GetInstanceScreenshot
&InstanceId=i-myInstance
&RegionId=cn-shenzhen
&WakeUp=false
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<GetInstanceScreenshotResponse>
  <RequestId>22A1933F-AD02-4560-A6A7-53CF2231D942</RequestId>
  <InstanceId>i-j5e42sbbthlokka11ech</InstanceId>
  <Screenshot>iVBORw0KGgoA... AAABJRU5ErkJggg==</Screenshot>
</GetInstanceScreenshotResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"Screenshot":"iVBORw0KGgoA... AAABJRU5ErkJggg==",
	"InstanceId":"i-j5e42sbbthlokka11ech",
	"RequestId":"22A1933F-AD02-4560-A6A7-53CF2231D942"
}
```

## Error codes {#section_o24_hy0_k69 .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|400|MissingParameter|%s|The error message returned when a required parameter is not specified.|
|404|InvalidParameter|%s|The error message returned when the parameter format is invalid.|
|405|IncorrectInstanceStatus|%s|The error message returned when the specified resource is in a state that does not support the current operation.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

