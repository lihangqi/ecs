# DescribeAutoProvisioningGroupHistory {#doc_api_Ecs_DescribeAutoProvisioningGroupHistory .reference}

调用DescribeAutoProvisioningGroupHistory接口查询弹性供应组的调度任务信息。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=DescribeAutoProvisioningGroupHistory)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
| AutoProvisioningGroupId |String|是|apg-uf6jel2bbl62wh13\*\*\*\*| 弹性供应组的ID。

 |
| RegionId |String|是|cn-hangzhou| 弹性供应组所在地域的ID。

 |
| Action |String|否|DescribeAutoProvisioningGroupHistory| 系统规定参数，取值： **DescribeAutoProvisioningGroupHistory** 。

 |
| EndTime |String|否|2019-06-20T15:10:20Z| 查询调度历史的结束时间，和 **StartTime** 结合使用确定查询时段。

 |
| StartTime |String|否|2019-04-01T15:10:20Z| 查询调度历史的起始时间，和 **EndTime** 结合使用确定查询时段。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|AutoProvisioningGroupHistories| | | 所有调度任务的信息。

 |
|└ActivityDetails| | | 单次调度任务的详细信息。

 |
|└Detail|String|New ECS instances "i-instanc\*\*\*\*, i-instanc\*\*\*\*" created.| 单次调度任务一次实例创建活动的执行详情。

 |
|└Status|String|Successful| 单次调度任务一次实例创建活动的执行状态，取值范围：

 -    **Successful** ：实例创建成功。
-    **Failed** ：实例创建失败。
-    **InProgress** ：实例创建中。
-    **Warning** ：实例部分创建成功。

 |
|└LastEventTime|String|2019-04-01T15:10:20Z| 单次调度任务最后一次实例创建活动的执行时间。

 |
|└StartTime|String|2019-04-01T15:10:20Z| 开始执行单次调度任务的时间。

 |
|└Status|String|success| 单次调度任务的状态，取值范围：

 -    **prepare** ：调度任务执行中。
-    **success** ：调度任务执行成功。
-    **failed** ：调度任务执行失败。

 |
|└TaskId|String|apg-task-uf60\*\*\*\*| 单次调度任务的ID。

 |
|PageNumber|Integer|1| 实例状态列表的页码。

 |
|PageSize|Integer|10| 分页查询时设置的每页行数。

 |
|RequestId|String|B48A12CD-1295-4A38-A8F0-0E92C937\*\*\*\*| 请求ID。

 |
|TotalCount|Integer|10| 查询到的弹性供应组内调度任务的个数。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://ecs.aliyuncs.com/?Action=DescribeAutoProvisioningGroupHistory
&AutoProvisioningGroupId=apg-uf6jel2bbl62wh13****
&RegionId=cn-hangzhou
&<公共请求参数>

```

正常返回示例

 `XML` 格式

``` {#xml_return_success_demo}
<DescribeAutoProvisioningGroups>
  <PageNumber>1</PageNumber>
  <TotalCount>1</TotalCount>
  <PageSize>10</PageSize>
  <RequestId>85331AC9-82C0-4604-9A14-048865BE7603</RequestId>
  <AutoProvisioningGroupHistorys>
    <AutoProvisioningGroupHistory>
      <Status>success</Status>
      <ActivityDetails>
        <ActivityDetail/>
      </ActivityDetails>
      <LastEventTime>2019-06-17T08:48:00Z</LastEventTime>
      <StartTime>2019-06-17T08:47:52Z</StartTime>
      <TaskId>apg-task-uf66bqtabg10wcf6****</TaskId>
    </AutoProvisioningGroupHistory>
  </AutoProvisioningGroupHistorys>
</DescribeAutoProvisioningGroups>

```

 `JSON` 格式

``` {#json_return_success_demo}
{
	"PageNumber":1,
	"TotalCount":1,
	"PageSize":10,
	"RequestId":"BA55349F-6E36-4E64-964B-419515D1****",
	"AutoProvisioningGroupHistorys":{
		"AutoProvisioningGroupHistory":[
			{
				"Status":"success",
				"LastEventTime":"2019-06-17T08:48:00Z",
				"ActivityDetails":{
					"ActivityDetail":[]
				},
				"TaskId":"apg-task-uf66bqtabg10wcf6****",
				"StartTime":"2019-06-17T08:47:52Z"
			}
		]
	}
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|403|Forbidden.RAM|User not authorized to operate on the specified resource, or this API doesn't support RAM.|子账号鉴权不通过。|
|400|MissingParamter.RegionId|The regionId should not be null.|参数 RegionId 不得为空。|

 [查看本产品错误码](https://error-center.aliyun.com/status/product/Ecs) 

