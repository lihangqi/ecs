# DescribeAutoSnapshotPolicyEX {#doc_api_1022313 .reference}

查询您已创建的自动快照策略。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=DescribeAutoSnapshotPolicyEx)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|否|DescribeAutoSnapshotPolicyEx|系统规定参数。取值：DescribeAutoSnapshotPolicyEx

 |
|AutoSnapshotPolicyId|String|否|p-233e6ylv0|自动快照策略 ID。

 |
|OwnerAccount|String|否|ECSforCloud@Alibaba.com|RAM用户的账号登录名称。

 |
|PageNumber|Integer|否|1|自动快照策略返回结果分多页展示。 起始值：1

 默认值：1

 |
|PageSize|Integer|否|10|分页展示返回的自动快照策略时的每页行数。 最大值：50

 默认值：10

 |
|RegionId|String|否|cn-hangzhou|要查询的自动快照策略所在的地域 ID。您可以调用 [DescribeRegions](~~25609~~) 查看最新的阿里云地域列表。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|AutoSnapshotPolicies| | |自动快照策略详情 AutoSnapshotPolicyType 组成的集合

 |
|└AutoSnapshotPolicyId|String|FinanceJoshua|自动快照策略ID。

 |
|└AutoSnapshotPolicyName|String|p-23f2i9s4t|自动快照策略的名称。

 |
|└CreationTime|String|2014-04-21T12:08:52Z|创建时间。按照 [ISO8601](~~25696~~) 标准表示，并需要使用UTC时间，格式为yyyy-MM-ddTHH:mm:ssZ。

 |
|└DiskNums|Integer|2|启用该策略的磁盘数量。

 |
|└RegionId|String|cn-hangzhou|自动快照策略所属的地域 ID。

 |
|└RepeatWeekdays|String|\["6"\]|指定自动快照的重复日期。选定周一到周日中需要创建快照的日期，参数为1~7 的数字，如：1 表示周一。允许选择多个日期。

 |
|└RetentionDays|Integer|30|指定自动快照的保留时间，单位为天。

 -   -1：永久保存
-   1~65536：指定保存天数

 |
|└Status|String|Available|自动快照策略状态，取值：

 -   Creating
-   Available

 |
|└TimePoints|String|\["4", "19"\]|指定自动快照的创建时间点。最小单位为小时，从 00:00~23:00 共 24 个时间点可选，参数为 0~23 的数字，如：1 代表在 01:00 时间点。可以选定多个时间点。 传递参数为一个带有格式的 Json Array："0", "1", ... "23"，最多 24 个时间点，用半角逗号字符隔开。

 |
|└VolumeNums|Integer|2|启用该策略的拓展卷数量。

 |
|PageNumber|Integer|1|自动快照策略列表的页码

 |
|PageSize|Integer|10|分页展示返回的自动快照策略时的每页行数

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID

 |
|TotalCount|Integer|2|自动快照策略的总个数

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

https://ecs.aliyuncs.com/?Action=DescribeAutoSnapshotPolicyEx
&RegionId=cn-hangzhou
&AutoSnapshotPolicyId=p-233e6ylv0
&PageNumber=1
&PageSize=10
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeAutoSnapshotPolicyResponse>
  <AutoSnapshotPolicies>
    <AntoSnapshotPolicy>
      <CreationTime>2014-04-21T12:08:52Z</CreationTime>
      <AutoSnapshotPolicyId>p-23f2i9s4t</AutoSnapshotPolicyId>
      <SettingTimePoints>[“2”, “9”]</SettingTimePoints>
      <SettingRepeatWeekdays>[“3” , “4” , “5” , “7”]</SettingRepeatWeekdays>
      <RetentionDays>-1</RetentionDays>
    </AntoSnapshotPolicy>
    <AntoSnapshotPolicy>
      <CreationTime>2014-07-24T13:00:52Z</CreationTime>
      <AutoSnapshotPolicyId>p-23f2i9s4t</AutoSnapshotPolicyId>
      <SettingTimePoints>[“0”, “1”]</SettingTimePoints>
      <SettingRepeatWeekdays>[“1”, “7”]</SettingRepeatWeekdays>
      <RetentionDays>30</RetentionDays>
    </AntoSnapshotPolicy>
  </AutoSnapshotPolicies>
  <PageNumber>1</PageNumber>
  <PageSize>2</PageSize>
  <TotalCount>2</TotalCount>
  <RequestId>F3CD6886-D8D0-4FEE-B93E-1B73239673DE</RequestId>
</DescribeAutoSnapshotPolicyResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"PageNumber":1,
	"TotalCount":2,
	"AutoSnapshotPolicies":{
		" AutoSnapshotPolicy":[
			{
				"CreationTime":"2014-07-24T13:00:52Z",
				"SettingRepeatWeekdays":"[“1”, “7”]",
				"RetentionDays":"30",
				"AutoSnapshotPolicyId":"p-23f2i9s4t",
				"SettingTimePoints":"[“0”, “1”]"
			},
			{
				"CreationTime":"2014-04-21T12:08:52Z",
				"SettingRepeatWeekdays":"[“3” , “4” , “5” , “7”]",
				"RetentionDays":"-1",
				"AutoSnapshotPolicyId":"p-a1fd3g5s1",
				"SettingTimePoints":"[“2”, “9”]"
			}
		]
	},
	"PageSize":2,
	"RequestId":"659F91C6-1949-43B0-90C4-B6342CA757D5"
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/Ecs)

