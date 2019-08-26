# ModifyLaunchTemplateDefaultVersion {#ModifyLaunchTemplateDefaultVersion .reference}

切换启动模板的某个版本为该模板的默认版本。如果您在创建实例（[RunInstances](intl.zh-CN/API 参考/实例/RunInstances.md#)）时不指定模板版本号，会采用默认版本。

## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：ModifyLaunchTemplateDefaultVersion|
|RegionId|String|是|模板所属的地域 ID。您可以调用 [DescribeRegions](intl.zh-CN/API 参考/地域/DescribeRegions.md#) 查看最新的阿里云地域列表。|
|DefaultVersionNumber|Long|是|设置为默认版本的启动模板版本号。|
|LaunchTemplateId|String|否|启动模板 ID。您必须指定 `LaunchTemplateId` 或 `LaunchTemplateName` 以确定模板。|
|LaunchTemplateName|String|否|启动模板名称。您必须指定 `LaunchTemplateId` 或 `LaunchTemplateName` 以确定模板。|

## 返回参数 {#ResponseParameter .section}

全是公共返回参数。参阅 [公共参数](intl.zh-CN/API 参考/快速入门/公共参数.md#commonResponseParameters)。

## 示例 { .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=ModifyLaunchTemplateDefaultVersion
&RegionId=cn-hangzhou
&LaunchTemplateName=lt-name1
&DefaultVersionNumber=2
&<公共请求参数>
```

**返回示例** 

**XML 格式**

```
<ModifyLaunchTemplateDefaultVersionResponse>
    <RequestId>04F0F334-1335-436C-A1D7-6C044FExxxxx</RequestId>
</ModifyLaunchTemplateDefaultVersionResponse>
```

 **JSON 格式** 

```
{
    "RequestId": "04F0F334-1335-436C-A1D7-6C044FExxxxx",
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问 [API 错误中心](https://error-center.alibabacloud.com/status/product/Ecs)。

|错误代码|错误信息|HTTP 状态码|说明|
|:---|:---|:-------|:-|
|InvalidLaunchTemplate.NotFound|The specified LaunchTemplateId “\{0\}” LaunchTemplateName “\{1\}” is not found.|400|指定的 `LaunchTemplateId` 或 `LaunchTemplateName`不存在。|
|InvalidLaunchTemplateVersion.NotFound|The specified LaunchTemplateId “\{0\}” Version “\{1\}” is not found.|400|指定的 `DefaultVersionNumber`不存在。|
|MissingParameter|The input parameter “\{0\}” that is mandatory for processing this request is not supplied.|400|缺失必需参数。|
|InvalidParameter|the parameter\(s\) “\{0\}” provided is\(are\) invalid.|400|指定的参数不合法。|
|InnerServiceFailed|call inner service failed|403|服务器内部错误。|

