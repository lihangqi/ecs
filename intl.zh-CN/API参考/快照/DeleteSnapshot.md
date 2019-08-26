# DeleteSnapshot {#doc_api_999641 .reference}

删除指定的快照。如果需要取消正在创建的快照，也可以调用该接口删除快照，即取消创建快照任务。

## 描述 {#description .section}

调用该接口时，您需要注意：

-   如果指定的快照 ID 不存在，请求将被忽略。
-   如果快照已经被用于创建自定义镜像，则快照不能被删除。您需要先删除已创建的自定义镜像（[DeleteImage](~~25537~~)），才能继续删除快照。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=DeleteSnapshot)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|SnapshotId|String|是|s-snapshotid1|快照 ID。

 |
|Action|String|否|DeleteSnapshot|系统规定参数。取值：DeleteSnapshot

 |
|Force|Boolean|否|false|是否强制删除有磁盘关联的快照。

 **说明：** 删除后该磁盘无法重新初始化。

 |
|OwnerAccount|String|否|ECSforCloud@Alibaba.com|RAM用户的账号登录名称。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。无论调用接口成功与否，我们都会返回请求 ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

https://ecs.aliyuncs.com/?Action=DeleteSnapshot
&SnapshotId=s-snapshotid1
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DeleteSnapshotResponse>
  <RequestId>CEF72CEB-54B6-4AE8-B225-F876FF7BA984</RequestId>
</DeleteSnapshotResponse>

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
|403|SnapshotCreatedImage|The snapshot has been used to create user defined image\(s\).|指定快照已经创建了自定义镜像，删除快照需要先删除关联的镜像。可以强行删除快照，但是会导致其绑定镜像不可用。|
|403|SnapshotCreatedDisk|The snapshot has been used to create disk\(s\).|指定的快照已经创建了磁盘，请不要重复创建。|
|400|MissingParameter|The input parameter SnapshotId that is mandatory for processing this request is not supplied.|参数 SnapshotId 不得为空。|
|404|InvalidSnapshotId.NotFound|The specified snapshot is not found|指定快照不存在。|
|403|Operation.Conflict|The operation may conflicts with others, please retry later.|操作冲突。|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Ecs)

