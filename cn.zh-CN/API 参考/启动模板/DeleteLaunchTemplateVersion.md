# DeleteLaunchTemplateVersion {#DeleteLaunchTemplateVersion .reference}

删除指定实例启动模板的一个版本。不支持删除默认版本，您需要通过 [DeleteLaunchTemplate](cn.zh-CN/API 参考/启动模板/DeleteLaunchTemplate.md#) 删除整个实例启动模板才能删除默认版本。

## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：DeleteLaunchTemplateVersion|
|RegionId|String|是|模板所属的地域 ID。您可以调用 [DescribeRegions](cn.zh-CN/API 参考/地域/DescribeRegions.md#) 查看最新的阿里云地域列表。|
|DeleteVersion.n|Long|是|模板版本号，`n` 的取值范围 \[1, 29\]。您可以调用 [DescribeLaunchTemplateVersions](cn.zh-CN/API 参考/启动模板/DescribeLaunchTemplateVersions.md#) 查询启动模板版本号列表。|
|LaunchTemplateId|String|否|模板 ID。您必须指定 `LaunchTemplateId` 或 `LaunchTemplateName` 以确定模板。|
|LaunchTemplateName|String|否|模板名称。|

## 返回参数 {#ResponseParameter .section}

全是公共返回参数。参阅 [公共参数](cn.zh-CN/API 参考/快速入门/公共参数.md#commonResponseParameters)。

## 示例 { .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=DeleteLaunchTemplateVersion
&RegionId=cn-hangzhou
&LaunchTemplateName=lt-name1
&DeleteVersion.1=1
&<公共请求参数>
```

**返回示例** 

**XML 格式**

```
<DeleteLaunchTemplateVersionResponse>
    <RequestId>04F0F334-1335-436C-A1D7-6C044FExxxxx</RequestId>
</DeleteLaunchTemplateVersionResponse>
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
|InvalidOperation.DeleteDefaultVersion|Delete default version from template is not allowed.|403|不支持删除模板默认版本。|

