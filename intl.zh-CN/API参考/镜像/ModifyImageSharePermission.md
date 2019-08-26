# ModifyImageSharePermission {#doc_api_1006139 .reference}

管理镜像共享权限。您可以将自己的自定义镜像共享给其他阿里云用户，该用户可以使用共享的自定义镜像创建 ECS 实例（RunInstances）或者更换实例的系统盘（ReplaceSystemDisk）。

## 描述 {#description .section}

调用该接口时，您需要注意：

-   您只能共享自己的自定义镜像给其他阿里云用户。
-   每份自定义镜像一次最多共享给 10 个阿里云账号。所以，参数 AddAccount.n 或者参数 RemoveAccount.n 单次最多可以传入 10 个阿里云账号，超过 10 个账号系统会忽略该参数。
-   每份自定义镜像最多可以共享给 50 个阿里云账号。您可以 [提交工单](https://workorder-intl.console.aliyun.com/#/ticket/createIndex) 申请共享给更多的用户。
-   使用共享镜像创建 ECS 实例（[RunInstances](~~63440~~)）后，一旦自定义镜像拥有者解除了镜像共享关系，或者删除了自定义镜像（[DeleteImage](~~25537~~)），该实例将无法初始化系统盘（[ReInitDisk](~~25519~~)）。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=ModifyImageSharePermission)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|ImageId|String|是|m-imageid1|被共享的自定义镜像 ID。

 |
|RegionId|String|是|cn-hangzhou|自定义镜像所属的地域 ID。您可以调用 [DescribeRegions](~~25609~~) 查看最新的阿里云地域列表。

 |
|Action|String|否|ModifyImageSharePermission|系统规定参数。取值：ModifyImageSharePermission

 |
|AddAccount.N|RepeatList|否|155780923771|授权共享镜像的阿里云账号 ID。n 的取值范围：1~10，超过 10 系统会忽略该参数。

 |
|OwnerAccount|String|否|ECSforCloud@Alibaba.com|RAM用户的账号登录名称。

 |
|RemoveAccount.N|RepeatList|否|155780923772|删除镜像共享的阿里云账号 ID。n 的取值范围：1~10，超过 10 系统会忽略该参数。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

https://ecs.aliyuncs.com/?Action=ModifyImageSharePermission
&ImageId=m-imageid1
&RegionId=cn-hangzhou
&AddAccount.1=155780923771
&RemoveAccount.1=155780923772
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ModifyImageSharePermissionResponse>
  <RequestId>C8B26B44-0189-443E-9816-D951F59623A9</RequestId>
</ModifyImageSharePermissionResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"C8B26B44-0189-443E-9816-D951F59623A9"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|MissingParameter|The input parameter "RegionId" that is mandatory for processing this request is not supplied.|区域ID不得为空。|
|404|InvalidImageId.NotFound|The specified ImageId does not exist.|指定的镜像在该用户账号下不存在，请您检查镜像id是否正确。|
|404|InvalidAccount.Forbbiden|The specified Account does not yourself.|不能把镜像共享给自己。|
|403|QuotaExceed.ShareImageUser|The shared Image user Quota exceeds.|已经超过单个镜像共享给用户数量的配额限制。|
|400|InvalidGroup.Malformed|The specified Group is wrongly formed.|指定的组不存在.。|
|403|OperationDeined.EncryptedSnapshot|The image contains encrypted snapshots, which do not support share.|不支持共享含有加密快照的镜像。|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Ecs)

