# DescribeTaskAttribute {#doc_api_1006031 .reference}

查询异步任务的详细信息。目前，可以查询的异步任务有导入镜像（ImportImage）和导出镜像（ExportImage）两种。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=DescribeTaskAttribute)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|RegionId|String|是|cn-hangzhou|地域 ID。您可以调用 [DescribeRegions](~~25609~~) 查看最新的阿里云地域列表。

 |
|TaskId|String|是|t-taskid|任务 ID。您可以调用 DescribeTasks 查看任务 ID。

 |
|Action|String|否|DescribeTaskAttribute|系统规定参数。取值：DescribeTaskAttribute

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|CreationTime|String|2015-11-23T02:13Z|任务创建时间。

 |
|FailedCount|Integer|0|失败任务数

 |
|FinishedTime|String|2015-11-23T02:19Z|任务完成时间。

 |
|OperationProgressSet| | |返回任务包含的信息，其中包括每一个子任务的状态和相关信息。

 |
|└ErrorCode|String|ParameterInvalid|错误代码

 |
|└ErrorMsg|String|The specified RegionId parameter is invalid.|错误信息

 |
|└OperationStatus|String|Success|操作状态

 |
|└RelatedItemSet| | |资源信息类型

 |
|└Name|String|OSSObject|相关项名称

 |
|└Value|String|MYOSSPRE\_m-23f8tcp8y\_t-23ym6mvro.vhd|相关项值

 |
|RegionId|String|cn-hangzhou|地域 ID。

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。

 |
|SuccessCount|Integer|1|成功任务数。

 |
|SupportCancel|String|true|是否可以取消任务（CancelTask）。可能值：

 -   True：可以取消
-   False：无法取消

 |
|TaskAction|String|ExportImage|任务操作的接口名称。

 |
|TaskId|String|t-taskid|任务ID

 |
|TaskProcess|String|100%|任务进程。

 |
|TaskStatus|String|Finished|任务状态。

 |
|TotalCount|Integer|1|任务总数。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

https://ecs.aliyuncs.com/?Action=DescribeTaskAttribute
&RegionId=cn-hangzhou
&TaskId=t-taskid
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeTaskAttributeResponse>
  <CreationTime>2015-11-23T02:13Z</CreationTime>
  <OperationProgressSet>
    <OperationProgress>
      <RelatedItemSet>
        <RelatedItem>
          <Name>OSSBucket</Name>
          <Value>image-temp</Value>
        </RelatedItem>
        <RelatedItem>
          <Name>OSSObject</Name>
          <Value>MYOSSPRE_m-23f8tcp8y_t-23ym6mvro.vhd</Value>
        </RelatedItem>
        <RelatedItem>
          <Name>ImageFormat</Name>
          <Value>vhd</Value>
        </RelatedItem>
      </RelatedItemSet>
      <ErrorMsg/>
      <ErrorCode/>
      <OperationStatus>Success</OperationStatus>
    </OperationProgress>
  </OperationProgressSet>
  <FinishedTime>2015-11-23T02:19Z</FinishedTime>
  <FailedCount>0</FailedCount>
  <SupportCancel>true</SupportCancel>
  <TotalCount>1</TotalCount>
  <SuccessCount>1</SuccessCount>
  <RequestId>EF0C5969-279B-49C8-AD83-BACCC74DD38C</RequestId>
  <RegionId>cn-hangzhou</RegionId>
  <TaskAction>ExportImage</TaskAction>
  <TaskStatus>Finished</TaskStatus>
  <TaskProcess>100%</TaskProcess>
  <TaskId>t-23ym6mvro</TaskId>
</DescribeTaskAttributeResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"OperationProgressSet":{
		"OperationProgress":[
			{
				"RelatedItemSet":{
					"RelatedItem":[
						{
							"Name":"OSSBucket",
							"Value":"image-temp"
						},
						{
							"Name":"OSSObject",
							"Value":"MYOSSPRE_m-23f8tcp8y_t-23ym6mvro.vhd"
						},
						{
							"Name":"ImageFormat",
							"Value":"vhd"
						}
					]
				},
				"ErrorMsg":"",
				"ErrorCode":"",
				"OperationStatus":"Success"
			}
		]
	},
	"FailedCount":0,
	"SupportCancel":true,
	"TotalCount":1,
	"TaskAction":"ExportImage",
	"TaskProcess":"100%",
	"TaskId":"t-23ym6mvro",
	"CreationTime":"2015-11-23T02:13Z",
	"FinishedTime":"2015-11-23T02:19Z",
	"SuccessCount":1,
	"RequestId":"4BE2C7FE-C7A4-4675-A153-174E032AABFB",
	"RegionId":"cn-hangzhou",
	"TaskStatus":"Finished"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InvalidRegionId.NotFound|The specified RegionId does not exist.|指定的 RegionId 不存在，请您检查此产品在该地域是否可用。|
|400|MissingParameter|An input parameter "RegionId" that is mandatory for processing the request is not supplied.|参数 RegionId 不得为空。|
|400|MissingParameter|An input parameter "TaskId" that is mandatory for processing the request is not supplied.|参数 TaskId 不得为空。|
|400|InvalidTaskId.NotFound|The specified "TaskId" is not found.|指定的 TaskId 不存在。|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Ecs)

