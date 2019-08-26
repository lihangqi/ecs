# ModifyImageSharePermission {#ModifyImageSharePermission .reference}

管理镜像共享权限。您可以将自己的自定义镜像共享给其他阿里云用户，该用户可以使用共享的自定义镜像创建 ECS 实例（[RunInstances](intl.zh-CN/API参考/实例/RunInstances.md#)）或者更换实例的系统盘（[ReplaceSystemDisk](intl.zh-CN/API参考/磁盘/ReplaceSystemDisk.md#)）。

## 描述 {#section_xlx_bjz_xdb .section}

调用该接口时，您需要注意：

-   您只能共享自己的自定义镜像给其他阿里云用户。

-   每份自定义镜像一次最多共享给 10 个阿里云账号。所以，参数 `AddAccount.n` 或者参数 `RemoveAccount.n` 单次最多可以传入 10 个阿里云账号，超过 10 个账号系统会忽略该参数。

-   每份自定义镜像最多可以共享给 50 个阿里云账号。您可以 [提交工单](https://workorder-intl.console.aliyun.com/#/ticket/createIndex) 申请共享给更多的用户。

-   使用共享镜像创建 ECS 实例（[RunInstances](intl.zh-CN/API参考/实例/RunInstances.md#)）后，一旦自定义镜像拥有者解除了镜像共享关系，或者删除了自定义镜像（[DeleteImage](intl.zh-CN/API参考/镜像/DeleteImage.md#)），该实例将无法初始化系统盘（[ReInitDisk](intl.zh-CN/API参考/磁盘/ReInitDisk.md#)）。


## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：ModifyImageSharePermission|
|RegionId|String|是|自定义镜像所属的地域 ID。您可以调用 [DescribeRegions](intl.zh-CN/API参考/地域/DescribeRegions.md#) 查看最新的阿里云地域列表。|
|ImageId|String|是|被共享的自定义镜像 ID。|
|AddAccount.n|String|否|授权共享镜像的阿里云账号 ID。n 的取值范围：\[1, 10\] 超过 10 系统会忽略该参数。

|
|RemoveAccount.n|String|否|删除镜像共享的阿里云账号 ID。n 的取值范围：\[1, 10\] 超过 10 系统会忽略该参数。

|

## 返回参数 {#section_hmx_bjz_xdb .section}

全是公共返回参数。参阅 [公共参数](intl.zh-CN/API参考/调用方式/公共参数.md#commonResponseParameters)

## 示例 { .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=ModifyImageSharePermission
&RegionId=cn-hangzhou
&ImageId=m-281234567
&AddAccount.1=23412345234
&<公共请求参数>
```

**返回示例** 

**XML 格式**

```
<ModifyImageSharePermissionResponse>
    <RequestId>C8B26B44-0189-443E-9816-D951F59623A9</RequestId>
</ModifyImageSharePermissionResponse>
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
|IncorrectImageStatus|The image is not available.|400|指定的自定义镜像不可用。|
|InvalidRegionId.NotFound|The specified region does not exist.|400|指定的 `RegionId` 不存在。|
|MissingParameter|An input parameter RegionId that is mandatory for processing the request is not supplied.|400|您必须指定参数 `RegionId`。|
|MissingParameter|An input parameter ImageId that is mandatory for processing the request is not supplied.|400|您必须指定参数 `ImageId`。|
|OperationDeined.EncryptedSnapshot|The image contains encrypted snapshots, which do not support share.|403|该镜像包含加密快照，不支持共享。|
|InvalidImageId.NotFound|The specified ImageId does not exist.|403|指定的 `ImageId` 不存在。|
|QuotaExceed.ShareImageUser|The shared image user quota exceeds.|403|您最多可以将该自定义镜像共享给 50 个阿里云账号。|
|InvalidAccount.Forbbiden|The specified account does not yourself.|404|您不能共享自定义镜像给自己。|
|InvalidAccount.NotFound|The specified parameter AddAccount.n or RemoveAccount.n does not exist.|404|参数 `AddAccount.n`或者 `RemoveAccount.n` 中有不存在的账号 ID。|

