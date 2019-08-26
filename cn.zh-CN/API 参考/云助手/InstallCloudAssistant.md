# InstallCloudAssistant {#reference_k2y_51c_n2b .reference}

为一台或多台实例安装云助手客户端。调用 InstallCloudAssistant后再调用 RebootInstance，云助手客户端即可生效。

## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：InstallCloudAssistant|
|RegionId|String|是|实例所在地域ID。您可以调用[DescribeRegions](cn.zh-CN/API 参考/地域/DescribeRegions.md#)查看最新的阿里云地域列表。|
|InstanceIds|Array|是|实例ID列表。以Python SDK为例，您可以取值为\[InstanceID1, InstanceID2, InstanceID3…\]，单次请求最多支持20台实例。|

## 返回参数 {#ResponseParameter .section}

全是公共返回参数。参阅 [公共返回参数](cn.zh-CN/API 参考/快速入门/公共参数.md#commonResponseParameters)。

## 示例 { .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=InstallCloudAssistant
&RegionId=cn-hangzhou
&InstanceIds=["i-bp11f7trr4hbi1xxxxxx", "i-bp1iudwa5b1tqaxxxxxx"]
&<公共请求参数>
```

**返回示例** 

**XML 格式**

```
<DeleteInstanceResponse>
    <RequestId>928E2273-5715-46B9-A730-238DC996A533</RequestId>
</DeleteInstanceResponse>
```

**JSON 格式** 

```
{
    "RequestId": "928E2273-5715-46B9-A730-238DC996A533"
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问 [API 错误中心](https://error-center.aliyun.com/status/product/Ecs)。

|错误代码|错误信息|HTTP 状态码|说明|
|:---|:---|:-------|:-|
|MissingParameter.RegionId|The input parameter “RegionId” that is mandatory for processing this request is not supplied.|400|`RegionId`为必需参数。或者您暂时无法使用该地域里的资源。|
|MissingParameter.InstanceIds|The input parameter “InstanceIds” that is mandatory for processing this request is not supplied.|400|`InstanceIds`为必需参数。|
|InvalidInstance.NotFound|The specified instances do not exist.|404|指定的`InstanceId`不存在。|
|InvalidRegionId.NotFound|The RegionId provided does not exist inour items.|404|指定的`RegionId`不存在。|

