# CancelCopyImage {#CancelCopyImage .reference}

取消正在进行中的复制镜像（[CopyImage](intl.zh-CN/API参考/镜像/CopyImage.md#)）任务。

## 描述 {#section_qxx_22z_xdb .section}

调用该接口时，您需要注意：

-   取消复制镜像后，目标地域中的新建的镜像会被自动删除，源镜像保持不变。

-   若复制镜像已完成，则操作失败并返回错误提示。


## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：CancelCopyImage|
|RegionId|String|是|目标镜像所属的地域 ID。您可以调用 [DescribeRegions](intl.zh-CN/API参考/地域/DescribeRegions.md#) 查看最新的阿里云地域列表。|
|ImageId|String|是|正在被复制的镜像 ID。|

## 返回参数 {#section_wxx_22z_xdb .section}

全是公共返回参数。参阅 [公共参数](intl.zh-CN/API参考/调用方式/公共参数.md#commonResponseParameters)

## 示例 { .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=CancelCopyImage
&RegionId=cn-hangzhou
&ImageId=img-2012-12-01-1300
&<公共请求参数>
```

**返回示例** 

**XML 格式**

```
<CancelCopyImageResponse>
    <RequestId>C8B26B44-0189-443E-9816-D951F59623A9</RequestId>
</CancelCopyImageResponse>
```

 **JSON 格式** 

```
{
    "RequestId": "C8B26B44-0189-443E-9816-D951F59623A9"
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问 [API 错误中心](https://error-center.alibabacloud.com/status/product/Ecs)。

|错误代码|错误信息|HTTP 状态码|说明|
|:---|:---|:-------|:-|
|ImageCreatedNotFromCopy|The specified image is not the target image of a copy action.|400|指定的镜像 `ImageId`没有复制镜像进程。|
|IncorrectImageStatus|The image has completed copy.|400|指定的镜像 `ImageId`已经复制完成，取消复制失败。|
|IncorrectImageStatus|The image is copied finished.|400|指定的镜像状态不对。|
|IncorrectImageStatus|The specified snapshot is not coping.|400|指定的镜像状态不对。|
|IncorrectImageStatus|The specified image is not coping.|400|指定的镜像状态不对。|
|IncorrectImageStatus|The Image copy has been failed.|400|指定的镜像状态不对。|
|InvalidImageId.NotFound|The specified ImageId does not exist.|404|指定的镜像不存在。|
|InvalidRegionId.NotFound|The specified region does not exist.|404|指定的 `RegionId` 不存在。|

