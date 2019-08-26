# CopyImage {#doc_api_Ecs_CopyImage .reference}

调用CopyImage复制一个地域下的自定义镜像到其他地域。您在其他地域可以使用复制后的镜像创建ECS实例（RunInstances）或者更换实例的系统盘（ReplaceSystemDisk）。

## 接口说明 {#description .section}

调用该接口时，您需要注意：

-   自定义镜像的状态必须为可用（`Available`）。
-   被复制的自定义镜像必须为您账号下的镜像，不能跨账号复制。
-   复制镜像的过程中无法删除镜像（[DeleteImage](~~25537~~)），但是您可以取消复制任务（[CancelCopyImage](~~25539~~)）。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=CopyImage&type=RPC&version=2014-05-26)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|ImageId|String|是|m-imageid1|源自定义镜像的ID。

 |
|RegionId|String|是|cn-hangzhou|源自定义镜像的地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。

 |
|Action|String|否|CopyImage|系统规定参数。取值：CopyImage

 |
|DestinationDescription|String|否|FinanceDept|目标镜像的描述信息。长度为2~256个英文或中文字符，不能以http://和https://开头。

 默认值：空。

 |
|DestinationImageName|String|否|FinanceJoshua|复制后的镜像的名称。长度为2~128个英文或中文字符。必须以大小字母或中文开头，不能以http://和https:// 开头。可以包含数字、半角冒号（:）、下划线（\_）或者连字符（-）。

 默认值：空。

 |
|DestinationRegionId|String|否|cn-shanghai|复制到目标地域的ID。

 |
|Encrypted|Boolean|否|false|是否加密镜像。

 |
|Tag.N.Key|String|否|FinanceJoshua|自定义镜像的标签键。

 |
|Tag.N.Value|String|否|FinanceDept|自定义镜像的标签值。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|ImageId|String|m-imageid2|复制后的镜像的ID。

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=CopyImage
&ImageId=m-imageid1
&RegionId=cn-hangzhou
&<公共请求参数>
```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<CopyImageResponse>
      <RequestId>C8B26B44-0189-443E-9816-D951F59623A9</RequestId>
      <ImageId>Img-231234***</ImageId>
</CopyImageResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"ImageId":"Img-231234***",
	"RequestId":"C8B26B44-0189-443E-9816-D951F59623A9"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|401|InvalidAliUid.IsNull|The aliUid must not be null|参数 aliUid 不得为空。|
|400|InvalidImageName.Malformed|The specified Image name is wrongly formed.|镜像名称不合法。长度为2-128个字符，以英文字母或中文开头，可包含数字，"."，"\_"或"-"。 不能以 http:// 和 https:// 开头。|
|403|Forbbiden|User not authorized to operate on the specified resource.|用户未被授权操作指定的资源。|
|400|InvalidImageName.Malformed|The specified destination Image name is wrongly formed.|镜像名称不合法。长度为2-128个字符，以英文字母或中文开头，可包含数字，"."，"\_"或"-"。 不能以 http:// 和 https:// 开头。|
|400|InvalidDescription.Malformed|The specified destination description is wrongly formed.|指定的资源描述格式不合法。长度为2-256个字符，不能以 http:// 和 https:// 开头。|
|400|InvalidDescription.Malformed|The specified description is wrongly formed.|指定的资源描述格式不合法。长度为2-256个字符，不能以 http:// 和 https:// 开头。|
|400|SourceRegion.NotFound|The source region not found|指定的源镜像的地域不存在。|
|400|DestinationRegion.NotFound|The destination region not found|指定的源镜像的地域不存在。|
|404|InvalidImageId.NotFound|The specified ImageId does not exist.|指定的镜像在该用户账号下不存在，请您检查镜像id是否正确。|
|400|IncorrectImageStatus|The image not available.|指定的镜像不可用。|
|400|InvalidSnapshotId.NotFound|The specified SnapshotId does not exist.|指定的快照不存在，请您检查快照是否正确。|
|400|InvalidImageName.Duplicated|The destination image is exist.|指定的镜像名已存在。|
|403|QuotaExceed.Image|The Image Quota exceeds.|自定义镜像额度已用完。|
|403|QuotaExceed.Snapshot|The snapshot quota exceeds.|快照额度超过限制，若要存储新快照，在不影响业务的情况下，请您删除已有的老快照。|
|403|OperationDenied.ImageCopying|The Image are coping.|正在复制镜像，请您稍后再试。|
|403|RegionNotSupportCopy|The region not support copy.|指定的目标镜像地域或者源镜像所在地域暂时不支持镜像复制。|
|403|InvalidSnapshot.TooOld|This operation is denied because the specified snapshot is created before 2013-07-15.|该操作被拒绝。因为指定的快照创建于 2013-07-15 之前。|
|403|OperationDenied|The specified snapshot is not allowed to create image.|指定快照不允许创建镜像。|
|403|IncorrectDestinationRegion|The destination region is not equal the target region.|复制镜像的源地域不能等于目标地域。|
|403|SizeExceed.Image|The image exceeds the maximum size. Please open a ticket to add the account to the white list.|指定的镜像容量过大，请提交工单联系阿里云。|
|403|OperationDeined.EncryptedSnapshot|The image contains encrypted snapshots, which do not support copying.|指定的镜像含有加密快照，不支持复制镜像。|
|403|InternalError|The request processing has failed due to some unknown error.|内部错误，请重试。如果多次尝试失败，请提交工单|
|403|OperationDenied.SameRegionOnly|The image shared from others can not be copied to another region directly.|无法复制共享镜像。|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

