# DeleteDisk {#doc_api_1030731 .reference}

释放一块按量付费数据盘。磁盘类型包括普通云盘、高效云盘和SSD云盘。

## 接口说明 {#description .section}

调用该接口时，您需要注意：

-   您的磁盘手动快照会被保留。
-   您可以通过 [ModifyDiskAttribute](~~25517~~) 设置是否保留或者同时释放自动快照。建议您及时删除不必要的快照，以保持足够的快照额度完成周期性的自动快照策略。
-   释放磁盘时，云盘的状态必须为 待挂载（Available）。
-   如果指定 ID 的磁盘不存在，请求将被忽略。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=DeleteDisk)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|DiskId|String|是|d-23jbf2v5m|需要释放的云盘设备 ID。

 |
|Action|String|否|DeleteDisk|系统规定参数。取值：DeleteDisk

 |
|OwnerAccount|String|否|ECSforCloud@Alibaba.com|RAM 用户的账号登录名称。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

https://ecs.aliyuncs.com/?Action=DeleteDisk
&DiskId=d-23jbf2v5m
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DeleteDiskResponse>
  <RequestId>CEF72CEB-54B6-4AE8-B225-F876FF7BA984</RequestId>
</DeleteDiskResponse>

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
|403|DiskCreatingSnapshot|The operation is denied due to a snapshot of the specified disk is not completed yet.|指定的磁盘正在创建快照。|
|403|DiskStillAttached|The disk is still attached to the disk.|磁盘仍然挂载在实例上。|
|403|UserNotInTheWhiteList|The user is not in disk white list.|您暂时不能使用该磁盘服务。|
|400|InvalidRegionId.MalFormed|The specified parameter RegionId is not valid.|指定的 RegionId 不合法。|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Ecs)

