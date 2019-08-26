# CopyImage {#CopyImage .reference}

复制一个地域下的自定义镜像到其他地域。您可以在其他地域可以使用复制后的镜像 创建 ECS 实例（[RunInstances](intl.zh-CN/API参考/实例/RunInstances.md#)）或者更换实例的系统盘（[ReplaceSystemDisk](intl.zh-CN/API参考/磁盘/ReplaceSystemDisk.md#)）。

## 描述 {#section_mv5_ndz_xdb .section}

调用该接口时，您需要注意：

-   自定义镜像的状态必须为 `Available`。

-   被复制的自定义镜像必须为您账号下的镜像，不能跨账号复制。

-   复制镜像的过程中无法删除镜像（[DeleteImage](intl.zh-CN/API参考/镜像/DeleteImage.md#)），但是您可以取消复制任务（[CancelCopyImage](intl.zh-CN/API参考/镜像/CancelCopyImage.md#)）。


## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：CopyImage|
|RegionId|String|是|源自定义镜像的地域 ID。您可以调用 [DescribeRegions](intl.zh-CN/API参考/地域/DescribeRegions.md#) 查看最新的阿里云地域列表。|
|ImageId|String|是|源自定义镜像的 ID。|
|DestinationRegionId|String|是|复制到目标地域的 ID。|
|DestinationImageName|String|否|复制后的镜像的名称。-   长度为 \[2, 128\] 个字符英文或中文字符，必须以大小字母或中文开头，可包含数字、半角冒号（:）、下划线（\_）或连字符（-）。
-   不能以 http:// 和 https:// 开头。

不填则为空，默认值：空。|
|DestinationDescription|String|否|目标镜像的描述信息。-   长度为 \[0, 256\] 个字符。
-   不能以 http:// 和 https:// 开头。

不填则为空，默认值：空。|

## 返回参数 {#ResponseParameter .section}

|名称|类型|描述|
|:-|:-|:-|
|ImageId|String|复制后的镜像的 ID|

## 示例 { .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=CopyImage
&DestinationRegionId=cn-hangzhou
&ImageId=m-281234567
&RegionId=cn-qingdao
&<公共请求参数>
```

**返回示例** 

**XML 格式**

```
<CopyImageResponse>
    <RequestId>C8B26B44-0189-443E-9816-D951F59623A9</RequestId>
    <ImageId>Img-231234567</ImageId>
</CopyImageResponse>
```

 **JSON 格式** 

```
{
    "RequestId": "C8B26B44-0189-443E-9816-D951F59623A9",
    "ImageId": "Img-231234567"
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问 [API 错误中心](https://error-center.alibabacloud.com/status/product/Ecs)。

|错误代码|错误信息|HTTP 状态码|说明|
|:---|:---|:-------|:-|
|DestinationRegion.NotFound|The destination region not found|400|指定的参数 `DestinationRegionId` 不存在。|
|IncorrectImageStatus|The image not available.|400|指定的镜像（`ImageId`）的状态必须为可用（`Available`）。|
|InvalidDescription.Malformed|The specified description is wrongly formed.|400|指定的参数 `DestinationDescription`格式有误。|
|InvalidImageId.NotFound|The specified ImageId does not exist.|400|指定的源镜像（`ImageId`）不存在。|
|InvalidImageName.Duplicated|The destination image is exist.|400|指定的 `DestinationImageName` 已经存在，请更改取值。|
|InvalidImageName.Malformed|The specified destination Image name is wrongly formed.|400|指定的目 `DestinationImageName` 标镜像名称不合法。|
|InvalidImageName.Malformed|The specified Image name is wrongly formed.|400|指定的 `DestinationImageName` 格式有误。|
|SourceRegion.NotFound|The source region not found|400|指定的源镜像（`RegionId`）不存在。|
|Forbidden|User not authorized to operate on the specified resource.|403|您暂时没有权限复制镜像。|
|IncorrectDestinationRegion|The destination region is not equal the target region.|403|指定的源地域（`RegionId`）和目标地域（`DestinationRegionId`）的取值不能相同|
|InvalidSnapshot.TooOld|This operation is denied because the specified snapshot is created before 2013-07-15.|403|指定源镜像（`ImageId`）所含的快照创建于 2013 年 7 月 15 日（含）之前，不能用于复制镜像。|
|OperationDeined.EncryptedSnapshot|The image contains encrypted snapshots, which do not support copying.|403|指定源镜像（`ImageId`）含有加密快照，不支持复制。|
|OperationDenied.ImageCopying|The specified image is being copied.|403|正在复制指定的源镜像（`ImageId`）中，请稍后再试。|
|QuotaExceed.Image|The Image Quota exceeds.|403|您的自定义镜像数量已经超过最大额度，无法复制镜像。|
|QuotaExceed.Snapshot|The maximum number of snapshots is exceeded.|403|已经超过快照的最大额度，无法复制镜像。|
|RegionNotSupportCopy|The region not support copy.|403|指定的目标地域（`DestinationRegionId`）不支持镜像复制。|

