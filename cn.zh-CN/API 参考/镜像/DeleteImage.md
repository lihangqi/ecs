# DeleteImage {#DeleteImage .reference}

删除一份自定义镜像。

## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：DeleteImage|
|RegionId|String|是|自定义镜像所在的地域 ID。您可以调用 [DescribeRegions](intl.zh-CN/API参考/地域/DescribeRegions.md#) 查看最新的阿里云地域列表。|
|ImageId|String|是|镜像 ID。如果指定的自定义镜像不存在，则请求将被忽略。|
|Force|String|否|是否执行强制删除。取值范围：-   true：强制删除自定义镜像，忽略当前镜像是否被其他实例使用。
-   false：正常删除自定义镜像，删除前检查当前镜像是否被其他实例使用。

|

## 返回参数 {#section_jlg_ggz_xdb .section}

全是公共返回参数。参阅 [公共参数](intl.zh-CN/API参考/调用方式/公共参数.md#commonResponseParameters)

## 示例 { .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=DeleteImage
&RegionId=cn-hangzhou
&ImageId=m-63DFD5FB2
&<公共请求参数>
```

**返回示例** 

**XML 格式**

```
<DeleteImageResponse>
     <RequestId>CEF72CEB-54B6-4AE8-B225-F876FF7BA984</RequestId>
</DeleteImageResponse>
```

 **JSON 格式** 

```
{
    "RequestId": "CEF72CEB-54B6-4AE8-B225-F876FF7BA984"
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问 [API 错误中心](https://error-center.alibabacloud.com/status/product/Ecs)。

|错误代码|错误信息|HTTP 状态码|说明|
|:---|:---|:-------|:-|
|ImageUsingByInstance|The specified image has been used to create instances.|403|指定的镜像 ID 被其他实例使用，暂时无法删除。|
|ImageIsCreating|The specified image is being created.|403|指定的自定义镜像正在创建中，请稍后再试。|
|ImageUseShared|The specified image has been shared to others.|403|您共享了该自定义镜像给其他用户，暂时无法删除。|
|OperationDenied.ImageCopying|The specified image is being copied.|403|指定的自定义镜像正在被复制中，请稍后再试。|
|InvalidRegionId.NotFound|The specified region does not exist.|404|指定的 `RegionId` 不存在。|

