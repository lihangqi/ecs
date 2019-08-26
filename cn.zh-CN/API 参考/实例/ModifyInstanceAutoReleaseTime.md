# ModifyInstanceAutoReleaseTime {#ModifyInstanceAutoReleaseTime .reference}

为一台按量付费 实例设定自动释放时间。设置自动释放时请谨慎操作，配置的时间到期后将自动释放 ECS 实例。

## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：ModifyInstanceAutoReleaseTime|
|InstanceId|String|是|需要自动释放的 ECS 实例 ID。|
|AutoReleaseTime|String|否|自动释放时间。按照 [ISO8601](intl.zh-CN/API参考/附录/时间格式.md#) 标准表示，并需要使用 UTC 时间。格式为：yyyy-MM-ddTHH:mm:ssZ。-   如果秒（`ss`）取值不是 `00`，则自动取为当前分钟（`mm`）开始时。
-   最短释放时间为当前时间半小时之后。
-   最长释放时间不能超过当前时间三年。

如果不传入参数 `AutoReleaseTime`，表示自动释放功能已取消，ECS 实例不再自动释放。|

## 返回参数 {#section_rjz_l25_xdb .section}

全是公共返回参数。参阅 [公共参数](intl.zh-CN/API参考/调用方式/公共参数.md#commonResponseParameters)

## 示例 { .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=ModifyInstanceAutoReleaseTime
&InstanceId=i-instance1
&<公共请求参数>
```

**返回示例** 

**XML 格式**

```
<ModifyInstanceAutoReleaseTimeResponse>
    <RequestId>04F0F334-1335-436C-A1D7-6C044FE73368</RequestId>
</ModifyInstanceAutoReleaseTimeResponse>
```

 **JSON 格式** 

```
{ 
    "RequestId": "C0003E8B-B930-4F59-ADC0-0E209A9012A8"
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问 [API 错误中心](https://error-center.alibabacloud.com/status/product/Ecs)。

|错误代码|错误信息|HTTP 状态码|说明|
|:---|:---|:-------|:-|
|InvalidAutoReleaseTime.Malformed|The specified paramter autoReleaseTime is not valid.|400|指定的参数 `AutoReleaseTime` 不合法。|
|MissingParamter.InstanceId|InstanceId should not be null.|400|您需要传入参数 `InstanceId`。|
|UnsupportedParameter|The parameters is unsupported.|400|不支持指定的参数。|
|ChargeTypeViolation|The operation is not permitted due to charge type of the instance.|403|仅支持自动释放按量付费实例。|
|NoSuchResource|The specified resource is not found.|404|指定的资源不存在。|
|InternalError|The request processing has failed due to some unknown error,exception or failure.|500|内部错误。|

