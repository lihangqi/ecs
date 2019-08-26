# ExportImage {#ExportImage .reference}

导出您的自定义镜像到与该自定义镜像同一地域的 OSS Bucket 里。

## 描述 {#section_aqg_jcz_xdb .section}

-   不支持导出使用市场镜像的系统盘快照创建的自定义镜像。
-   支持导出镜像中包括数据盘快照的信息的自定义镜像，其中数据盘数不能超过 4 块，单块数据盘容量最大不能超过 500 GB。
-   您需要 [提交工单](https://workorder-intl.console.aliyun.com/#/ticket/createIndex) 联系阿里云，为您开启导出镜像功能。

-   需要通过 RAM 授权云服务器 ECS 官方服务账号写入 OSS 的权限：
    1.  创建角色：`AliyunECSImageExportDefaultRole`（其他任何角色名称无效），为该角色设置以下角色策略：

        ```
         {
           "Statement": [
             {
               "Action": "sts:AssumeRole",
               "Effect": "Allow",
               "Principal": {
                 "Service": [
                   "ecs.aliyuncs.com"
                 ]
               }
             }
           ],
           "Version": "1"
         }
        ```

    2.  在角色 `AliyunECSImageExportDefaultRole` 下加入默认的系统权限策略：`AliyunECSImageExportRolePolicy`，该策略是云服务器 ECS 提供导出镜像的默认策略。用户也可以创建自定义策略，权限需要包含：

        ```
         {
           "Version": "1",
           "Statement": [
             {
               "Action": [
                 "oss:GetObject",
                 "oss:PutObject",
                 "oss:DeleteObject",
                 "oss:GetBucketLocation",
                 "oss:AbortMultipartUpload",
                 "oss:ListMultipartUploads",
                 "oss:ListParts"
               ],
               "Resource": "*",
               "Effect": "Allow"
             }
           ]
         }
        ```


## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：ExportImage|
|RegionId|String|是|自定义镜像的地域 ID。您可以调用 [DescribeRegions](intl.zh-CN/API参考/地域/DescribeRegions.md#) 查看最新的阿里云地域列表。|
|ImageId|String|是|自定义镜像 ID。|
|OssBucket|String|是|保存导出镜像的 OSS bucket。|
|OssPrefix|String|否|用户的 OSS 的 Object 的前缀。可以由数字或者字母组成，字符长度为 \[1, 30\]。|
|ClientToken|String|否|用于保证请求的幂等性。由客户端生成该参数值，要保证在不同请求间唯一。只支持 ASCII 字符，且不能超过 64 个字符。更多详情，请参阅 [如何保证幂等性](intl.zh-CN/API参考/附录/如何保证幂等性.md#)。|

## 返回参数 {#ResponseParameter .section}

|名称|类型|描述|
|:-|:-|:-|
|RegionId|String|地域 ID|
|ExportTaskId|String|导出镜像任务 ID|

## 示例 { .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=ExportImage
&RegionId=cn-hangzhou
&ImageId=m-231234567
&OssBucket=testexportImage
&<公共请求参数>
```

**返回示例** 

**XML 格式**

```
<ExportImageResponse>
    <RequestId>C8B26B44-0189-443E-9816-D951F59623A9</RequestId>
    <ExportTaskId>tsk-231234567</ExportTaskId>
    <RegionId>cn-hangzhou</RegionId>
</ExportImageResponse>
```

 **JSON 格式** 

```
{
    "RequestId": "C8B26B44-0189-443E-9816-D951F59623A9",
    "RegionId": "cn-hangzhou",
    "ExportTaskId": "tsk-231234567"
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问 [API 错误中心](https://error-center.alibabacloud.com/status/product/Ecs)。

|错误代码|错误信息|HTTP 状态码|说明|
|:---|:---|:-------|:-|
|Forbidden|User is not authorized to operate on the specified image.|400|用户没有权限导出镜像。|
|IncorrectImageStatus|The image is not available.|400|指定的镜像暂不可用。|
|MissingParameter|An input parameter RegionId that is mandatory for processing the request is not supplied.|400|缺少 `RegionId` 值。|
|MissingParameter|An input parameter ImageId that is mandatory for processing the request is not supplied.|400|缺少 `ImageId` 值。|
|MissingParameter|An input parameter OssBucket that is mandatory for processing the request is not supplied.|400|缺少 `OssBucket` 值。|
|OssBucket.NotFound|The specified OssBucket does not exist.|400|指定的 OSS bucket 在当前地域下不存在。|
|OssPrefix.Malformed|The specified OssPrefix format is incorrect.|400|指定的 OSS 的 Object 的前缀格式不合法。|
|RegionId.NotFound|The specified RegionId does not exist.|400|指定的镜像的 `RegionId` 不存在。|
|ExportImageFailed|Failed to export image.|403|导出镜像失败。|
|ImageId.NotFound|The image does not exist.|403|指定的镜像 ID 不存在。|
|ImageNotSupported|The specified image is from the image market and does not support export.|403|指定的镜像来自镜像市场，不支持导出。|
|InvalidRegion.NotSupport|The specified region does not support image import or export.|403|指定的地域暂时不支持导入或导出镜像。|
|OperationDenied.ImageExporting|The specified image is being exported.|403|正在导出指定的镜像。|

