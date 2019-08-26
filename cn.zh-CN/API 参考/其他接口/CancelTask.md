# CancelTask {#CancelTask .reference}

取消一件正在运行的任务。目前，您能取消正在运行的导入镜像任务（[ImportImage](intl.zh-CN/API参考/镜像/ImportImage.md#)）和导出镜像任务（[ExportImage](intl.zh-CN/API参考/镜像/ExportImage.md#)）。

## 请求参数 {#section_mzx_3yg_ydb .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：CancelTask|
|RegionId|String|是|地域 ID。您可以调用 [DescribeRegions](intl.zh-CN/API参考/地域/DescribeRegions.md#) 查看最新的阿里云地域列表。|
|TaskId|String|是|任务 ID。您可以调用 [DescribeTasks](intl.zh-CN/API参考/其他接口/DescribeTasks.md#) 查看任务 ID 列表。|

## 返回参数 {#section_f54_lk5_xdb .section}

全是公共返回参数。参阅 [公共参数](intl.zh-CN/API参考/调用方式/公共参数.md#commonResponseParameters)。

## 示例 { .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=CancelTask
&RegionId=cn-hangzhou
&TaskId=t-23ym6mvro
&<公共请求参数>
```

**返回示例** 

**XML 格式**

```
<CancelTaskResponse>
    <RequestId>4BE2C7FE-C7A4-4675-A153-174E032AABFB</RequestId>
</CancelTaskResponse>
```

 **JSON 格式** 

```
{
    "RequestId": "4BE2C7FE-C7A4-4675-A153-174E032AABFB"
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问 [API 错误中心](https://error-center.alibabacloud.com/status/product/Ecs)。

|错误代码|错误信息|HTTP 状态码|说明|
|:---|:---|:-------|:-|
|MissingParameter|An input parameter “RegionId” that is mandatory for processing the request is not supplied.|400|您需要指定参数 `RegionId`。|
|MissingParameter|An input parameter “TaskId” that is mandatory for processing the request is not supplied.|400|您需要指定参数 `TaskId`。|
|InvalidRegionId.NotFound|The specified region not found.|400|指定的 `RegionId` 不存在。|
|InvalidTaskId.NotFound|The specified “TaskId” is not found.|400|指定的 `TaskId` 不存在。|
|CancelTaskFailed|The task is failed to cancel, Please contact the administrator.|403|取消任务失败，请 [提交工单](https://workorder-intl.console.aliyun.com/#/ticket/createIndex) 联系我们。|
|InvalidTaskId.IncorrectTaskStatus|The specified task status is not invalid.|403|指定的任务必须处于 **运行中** 状态。|
|InvalidTaskId.TaskActionNotSupport|The specified task action not support.|403|无法取消指定的任务。|

