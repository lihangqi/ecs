# CancelTask {#doc_api_1000174 .reference}

取消一件正在运行的任务。目前，您能取消正在运行的导入镜像任务（ImportImage）和导出镜像任务（ExportImage）。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=CancelTask)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|RegionId|String|是|cn-hangzhou|地域 ID。您可以调用 [DescribeRegions](~~25609~~) 查看最新的阿里云地域列表。

 |
|TaskId|String|是|t-23ym6mvro|任务 ID。您可以调用 [DescribeTasks](~~25622~~) 查看任务 ID 列表。

 |
|Action|String|否|CancelTask|系统规定参数。取值：CancelTask

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。无论调用接口成功与否，我们都会返回请求 ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

https://ecs.aliyuncs.com/?Action=CancelTask
&RegionId=cn-hangzhou
&TaskId=t-23ym6mvro
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<CancelTaskResponse>
  <RequestId>4BE2C7FE-C7A4-4675-A153-174E032AABFB</RequestId>
</CancelTaskResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"4BE2C7FE-C7A4-4675-A153-174E032AABFB"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|MissingParameter|An input parameter "RegionId" that is mandatory for processing the request is not supplied.|参数 RegionId 不得为空。|
|400|MissingParameter|An input parameter "TaskId" that is mandatory for processing the request is not supplied.|参数 TaskId 不得为空。|
|400|InvalidRegionId.NotFound|The specified RegionId does not exist.|指定的 RegionId 不存在，请您检查此产品在该地域是否可用。|
|400|InvalidTaskId.NotFound|The specified "TaskId" is not found.|指定的 TaskId 不存在。|
|403|CancelTaskFailed|The task is failed to cancel, Please contact the administrator.|取消任务失败，请联系系统管理员。|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Ecs)

