# ImportImage {#ImportImage .reference}

导入您已有的镜像文件到云服务器ECS，并作为自定义镜像出现在相应地域中。

## 描述 {#section_zj2_5wy_xdb .section}

导入自定义镜像后，您可以使用创建的自定义镜像创建ECS实例（[RunInstances](intl.zh-CN/API 参考/实例/RunInstances.md#)）或者更换实例的系统盘（[ReplaceSystemDisk](intl.zh-CN/API 参考/磁盘/ReplaceSystemDisk.md#)）。调用该接口时，您需要注意：

-   您必须提前 [上传镜像文件到对象存储OSS](../../../../../intl.zh-CN/快速入门/上传文件.md#)。
-   导入镜像的地域必须跟镜像文件上传的OSS Bucket的地域相同。
-   参数`DiskDeviceMapping.n`中n的取值范围为\[1, 17\]。n为1时表示系统盘，n为\[2, 17\]时表示数据盘。
-   不能删除正在导入的镜像，只能取消导入镜像任务（[CancelTask](intl.zh-CN/API 参考/其他接口/CancelTask.md#)）。
-   您需要预先通过 [访问控制RAM](../../../../../intl.zh-CN/产品简介/什么是RAM？.md#) 服务为您授权ECS访问OSS。参阅以下步骤：
    1.  创建角色 `AliyunECSImageImportDefaultRole`。**必须是这个名称**，否则导入镜像会失败。角色的策略为：

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

    2.  在该角色下，添加权限策略`AliyunECSImageImportRolePolicy`。这个策略是ECS导入镜像功能的默认策略，或者您也可以创建自定义策略，权限需要包含：

        ```
        {
        "Version": "1",
        "Statement": [
        {
        "Action": [
         "oss:GetObject",
         "oss:GetBucketLocation"
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
|Action|String|是|系统规定参数。取值：ImportImage|
|RegionId|String|是|源自定义镜像的地域ID。您可以调用[DescribeRegions](../intl.zh-CN/API 参考/地域/DescribeRegions.md#)查看最新的阿里云地域列表。|
|ImageName|String|否|镜像名称。-   长度为\[2, 128\]个大小写英文或中文字符，必须以大小字母或中文开头，可包含数字、点号（.）、半角冒号（:）、下划线（\_）或连字符（-）。
-   不能以http://和https://开头。

|
|Description|String|否|镜像的描述信息。-   长度为\[0, 256\]个大小写英文或中文字符。
-   不能以http://和https://开头。

|
|Architecture|String|否|系统架构。取值范围：-   i386
-   x86\_64

默认值：x86\_64|
|OSType|String|否|操作系统平台类型。取值范围：-   windows
-   linux

默认值：linux|
|Platform|String|否|操作系统发行版。取值范围：-   CentOS
-   Ubuntu
-   SUSE
-   OpenSUSE
-   Debian
-   CoreOS
-   Aliyun
-   Windows Server 2003
-   Windows Server 2008
-   Windows Server 2012
-   Others Linux
-   Customized Linux

默认值：Others Linux|
|DiskDeviceMapping.n.Format|String|否|镜像格式。取值范围：-   RAW
-   VHD
-   qcow2

导入镜像时，系统自动检测镜像格式，以检测格式为准。|
|DiskDeviceMapping.n.OSSBucket|String|是|镜像文件所在的OSS Bucket。|
|DiskDeviceMapping.n.OSSObject|String|是|镜像文件所在的OSS Object的文件名称（key）。|
|DiskDeviceMapping.n.DiskImageSize|String|否|镜像大小。必须确保系统盘空间≥文件系统空间。取值范围：-   n = 1 时，即系统盘：\[5, 500\] GiB
-   = \[2, 17\] 时，即数据盘：\[5, 1000\] GiB

导入镜像时，系统自动检测镜像大小，以检测结果为准。|

## 返回参数 {#ResponseParameter .section}

|名称|类型|描述|
|:-|:-|:-|
|RegionId|String|地域ID|
|ImageId|String|镜像ID|
|ImportTaskId|String|导入镜像任务ID|

## 示例 { .section}

**请求示例**

```
https://ecs.aliyuncs.com/?Action=ImportImage
&RegionId=cn-hangzhou
&DiskDeviceMapping.1.OSSBucket=ecsimageos
&DiskDeviceMapping.1.OSSObject=CentOS_5.4_32.raw
&<公共请求参数>
```

**返回示例**

**XML格式**

```
<ImportImageResponse>
    <RequestId>C8B26B44-0189-443E-9816-D951F59623A9</RequestId>
    <ImageId>Img-231234567</ImageId>
    <ImportTaskId>123-345-2332-22323</ImportTaskId>
</ImportImageResponse>
```

**JSON格式**

```
{
    "RequestId": "C8B26B44-0189-443E-9816-D951F59623A9",
    "ImageId": "Img-231234567"，
    "ImportTaskId":"123-345-2332-22323"
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问 [API错误中心](https://error-center.alibabacloud.com/status/product/Ecs)。

|错误代码|错误信息|HTTP状态码|说明|
|:---|:---|:------|:-|
|Forbbiden|User not authorized to operate on the specified resource|400|您暂时无法导入镜像。请[提交工单](https://workorder-intl.console.aliyun.com/#/ticket/createIndex)联系阿里云，为您开启导入镜像功能。

|
|IncorrectImageStatus|The specified image is not available.|400|指定的镜像状态不正确。|
|InvalidArchitecture.Malformed|The specified Architecture is wrongly formed.|400|指定的参数`Architecture`不合法。|
|InvalidDescription.Malformed|The specified destination image description is wrongly formed.|400|指定的参数`Description`不合法。|
|InvalidFormat.Malformed|The specified Image format is wrongly formed.|400|指定的镜像文件格式不合法。|
|InvalidImageName.Duplicated|The destination image is exist.|400|镜像名称已经重复。|
|InvalidImageName.Malformed|The specified destination Image name is wrongly formed.|400|指定的参数`ImageName`格式有误。|
|InvalidImageSize|The specified “DiskDeviceMapping.n.DiskImageSize” should be not less than system device size.|400|指定的参数`DiskDeviceMapping.n.DiskImageSize`取值必须大于实际的磁盘大小。|
|InvalidOSType.Malformed|The specified OSType is wrongly formed.|400|指定的参数`OSType`不合法。|
|InvalidPlatform.Malformed|The specified Platform is wrongly formed.|400|指定的参数`Platform`不合法。|
|MissingParameter|An input parameter “RegionId” that is mandatory for processing the request is not supplied.|400|您需要指定必需参数`RegionId`。|
|MissingParameter|An input parameter “DiskDeviceMapping.n.OSSBucket” that is mandatory for processing the request is not supplied.|400|您需要指定必需参数`OSSBucket`。|
|MissingParameter|An input parameter “DiskDeviceMapping.n.OSSObject” that is mandatory for processing the request is not supplied.|400|您需要指定必需参数`OSSObject`。|
|RegionId.NotFound|The specified region is not found.|400|指定的`RegionId`不存在。|
|ImageIsImporting|The specified Image is importing.|403|指定的镜像正在被复制中。请稍后再试。|
|InvalidRegion.NotSupport|The specified region does not support image import or export.|403|指定的地域暂时不支持导入镜像功能。|
|QuotaExceed.Image|The Image Quota exceeds.|403|您的自定义镜像数已超出最高限制，不能再导入镜像。|
|QuotaExceed.Snapshot|The maximum number of snapshots is exceeded.|403|您的快照数已超出最高限制，不能再导入镜像。|

