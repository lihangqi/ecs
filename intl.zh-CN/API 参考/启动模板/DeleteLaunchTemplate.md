# DeleteLaunchTemplate {#DeleteLaunchTemplate .reference}

删除一个实例启动模板。

## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：DeleteLaunchTemplate|
|RegionId|String|是|实例启动模板所属的地域 ID。您可以调用 [DescribeRegions](cn.zh-CN/API 参考/地域/DescribeRegions.md#) 查看最新的阿里云地域列表。|
|LaunchTemplateId|String|否|实例启动模板 ID。更多详情，请调用 [DescribeLaunchTemplates](cn.zh-CN/API 参考/启动模板/DescribeLaunchTemplates.md#)。您必须指定 `LaunchTemplateId` 或 `LaunchTemplateName` 以确定模板。|
|LaunchTemplateName|String|否|实例启动模板名称。|

## 返回参数 {#ResponseParameters .section}

全是公共返回参数。参阅 [公共参数](cn.zh-CN/API 参考/快速入门/公共参数.md#commonResponseParameters)。

## 示例 { .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=DeleteLaunchTemplate
&RegionId=cn-hangzhou
&LaunchTemplateName=lt-name1
&<公共请求参数>
```

**返回示例** 

**XML 格式**

```
<DeleteLaunchTemplateResponse>
    <RequestId>04F0F334-1335-436C-A1D7-6C044FExxxxx</RequestId>
</DeleteLaunchTemplateResponse>
```

 **JSON 格式** 

```
{
    "RequestId": "04F0F334-1335-436C-A1D7-6C044FExxxxx",
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问 [API 错误中心](https://error-center.aliyun.com/status/product/Ecs)。

|错误代码|错误信息|HTTP 状态码|说明|
|:---|:---|:-------|:-|
|MissingParameter|The input parameter “\{0\}” that is mandatory for processing this request is not supplied.|400|缺失必需参数。|
|InvalidParameter|the parameter\(s\) “\{0\}” provided is\(are\) invalid.|400|指定的参数不合法。|
|InnerServiceFailed|call inner service failed|403|服务器内部错误。|

