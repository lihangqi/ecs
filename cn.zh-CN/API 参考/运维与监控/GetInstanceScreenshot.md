# GetInstanceScreenshot {#GetInstanceScreenshot .reference}

获取实例的截屏信息。

## 描述 {#BestPractice .section}

我们返回Base64编码后的JPG图像格式的实例截屏，您需要自行解码。您可以在排查故障时调用该接口，并请注意：

-   实例必须处于**运行中**（`Running`）状态。
-   [已停售的实例规格](https://help.aliyun.com/document_detail/55263.html)无法获取截屏信息。

## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：GetInstanceScreenshot|
|RegionId|String|是|实例所在地域ID。您可以调用[DescribeRegions](../cn.zh-CN/API 参考/地域/DescribeRegions.md#)查看最新的阿里云地域列表。|
|InstanceId|String|是|实例ID。|
|Wakeup|Boolean|否|是否唤醒处于休眠状态的实例。默认值：false

|

## 返回参数 {#ResponseParameter .section}

|名称|类型|描述|
|:-|:-|:-|
|InstanceId|String|实例ID|
|Screenshot|String|JPG图像格式的实例截屏，返回Base64编码后的图像|

## 示例 { .section}

**请求示例**

```
http://ecs-cn-hangzhou.example.com/?Action=GetInstanceScreenshot
&RegionId=cn-shenzhen
&InstanceId=i-j5e42sbbthlokka11eci
&Wakeup=False
&<公共请求参数>
```

**正常返回示例**

**XML格式**

```
<GetInstanceScreenshotResponse>
    <RequestId>22A1933F-AD02-4560-A6A7-53CF2231D942</RequestId>
    <InstanceId>i-j5e42sbbthlokka11ech</InstanceId>
    <Screenshot>iVBORw0KGgoA...AAABJRU5ErkJggg==</Screenshot>
</GetInstanceScreenshotResponse>
```

**JSON格式**

```
{
    "RequestId": "22A1933F-AD02-4560-A6A7-53CF2231D942",
    "InstanceId": "i-j5e42sbbthlokka11ech",
    "Screenshot": "iVBORw0KGgoA...AAABJRU5ErkJggg=="
}
```

**异常返回示例**

**XML格式**

```
<Error>
    <RequestId>C38E0D94-C18B-44F3-8C05-6E35BE334088</RequestId>
    <HostId>ecs.aliyuncs.com</HostId>
    <Code>NotSupported</Code>
    <Message>The operation is not supported for "i-j5e42sbbthlokkaXXXXX".</Message>
</Error>
```

**JSON格式**

```
{
    "RequestId": "C38E0D94-C18B-44F3-8C05-6E35BE334088",
    "HostId": "ecs.aliyuncs.com",
    "Code": "NotSupported",
    "Message": "The operation is not supported for "i-j5e42sbbthlokkaXXXXX"."
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问[API错误中心](https://error-center.aliyun.com/status/product/Ecs)。

|错误代码|错误信息|HTTP状态码|说明|
|:---|:---|:------|:-|
|MissingParameter|The input parameter “instanceId” that is mandatory for processing this request is not supplied.|400|您必须指定参数InstanceId。|
|InvalidParameter|The “instanceId” provided is not valid.|404|指定的InstanceId不存在。|
|IncorrectInstanceStatus|The instance status “\{status\}” is not applicable|405|实例必须处于**运行中**（`Running`）状态。|
|NotSupported|The operation is not supported for “\{instanceId\}”|405|[已停售的实例规格](https://help.aliyun.com/document_detail/55263.html)无法获取截屏信息。|
|Throttling|Request was denied due to request throttling.|429|系统流控期间，请稍后再试。|

