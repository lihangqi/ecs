# DeleteImage {#doc_api_Ecs_DeleteImage .reference}

删除一份自定义镜像。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=DeleteImage)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|ImageId|String|是|m-imageid1|镜像 ID。如果指定的自定义镜像不存在，则请求将被忽略。

 |
|RegionId|String|是|cn-hangzhou|自定义镜像所在的地域 ID。您可以调用 [DescribeRegions](~~25609~~) 查看最新的阿里云地域列表。

 |
|Action|String|否|DeleteImage|系统规定参数。取值：DeleteImage

 |
|Force|Boolean|否|false|是否执行强制删除。取值范围：

 -   true：强制删除自定义镜像，忽略当前镜像是否被其他实例使用。
-   false：正常删除自定义镜像，删除前检查当前镜像是否被其他实例使用。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

https://ecs.aliyuncs.com/?Action=DeleteImage
&ImageId=m-imageid1
&RegionId=cn-hangzhou
&Force=false
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DeleteImageResponse>
  <RequestId>CEF72CEB-54B6-4AE8-B225-F876FF7BA984</RequestId>
</DeleteImageResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"CEF72CEB-54B6-4AE8-B225-F876FF7BA984"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|403|ImageUsingByInstance|The specified image has been used to create instances.|指定的镜像已被用于创建实例，无法删除。|
|403|ImageUseShared|The specified image has been shared to others.|指定的镜像已经分享给其它用户。|
|403|OperationDenied.ImageCopying|The Image is coping.|正在复制镜像，请您稍后再试。|
|403|ImageIsCreating|The specified image is being created.|正在生成指定的镜像中。|
|403|ImageIsImporting|The specified Image is importing.|指定镜像正在导入，无法执行操作。|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Ecs)

