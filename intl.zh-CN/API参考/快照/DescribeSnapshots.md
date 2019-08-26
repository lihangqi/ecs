# DescribeSnapshots {#doc_api_Ecs_DescribeSnapshots .reference}

查询一台ECS实例或一块磁盘设备所有的快照列表。InstanceId、DiskId和SnapshotIds不是必需参数，但是可以构建过滤器逻辑，参数之间为逻辑与（And）关系。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=DescribeSnapshots)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|RegionId|String|是|cn-hangzhou|磁盘所属于的地域ID。您可以调用 [DescribeRegions](~~25609~~) 查看最新的阿里云地域列表。

 |
|Action|String|否|DescribeSnapshots|系统规定参数。取值：DescribeSnapshots

 |
|DiskId|String|否|d-diskid1|指定的磁盘设备ID。

 |
|DryRun|Boolean|否|false|是否只预检此次请求。

 -   true：发送检查请求，不会查询资源状况。检查项包括AccessKey是否有效、RAM用户的授权情况和是否填写了必需参数。如果检查不通过，则返回对应错误。如果检查通过，会返回错误码DryRunOperation。
-   false（默认）：发送正常请求，通过检查后返回2XX HTTP状态码并直接查询资源状况。

 |
|Encrypted|Boolean|否|false|是否过滤加密快照。默认值：false

 |
|Filter.1.Key|String|否|CreationStartTime|查询资源时的筛选键。取值必须为 CreationStartTime。

 **说明：** 该参数即将被弃用，为提高兼容性，请尽量使用其他参数。

 |
|Filter.1.Value|String|否|2017-12-05T22:40:00Z|查询资源时的筛选值。取值必须为资源创建的开始时间点（CreationStartTime）。

 **说明：** 该参数即将被弃用，为提高兼容性，请尽量使用其他参数。

 |
|Filter.2.Key|String|否|CreationEndTime|查询资源时的筛选键。取值必须为 CreationEndTime。

 **说明：** 该参数即将被弃用，为提高兼容性，请尽量使用其他参数。

 |
|Filter.2.Value|String|否|2017-12-06T22:40:00Z|查询资源时的筛选值。取值必须为资源创建的结束时间点（CreationEndTime）。

 **说明：** 该参数即将被弃用，为提高兼容性，请尽量使用其他参数。

 |
|InstanceId|String|否|i-instanceid1|指定的实例ID。

 |
|KMSKeyId|String|否|0e478b7a-4262-4802-b8cb-00d3fb40826X|数据盘对应的KMS密钥ID。

 |
|PageNumber|Integer|否|1|快照列表的页码。起始值：1

 默认值：1

 |
|PageSize|Integer|否|10|分页查询时设置的每页行数。最大值：100

 默认值：10

 |
|ResourceGroupId|String|否|rg-resourcegrouid|资源组ID。

 |
|SnapshotIds|String|否|\["s-xxxxxxxxx", "s-yyyyyyyyy", … "s-zzzzzzzzz"\]|快照标识编码。取值可以由多个快照ID组成一个JSON数组，最多支持100个ID，ID之间用半角逗号（,）隔开。

 |
|SnapshotLinkId|String|否|d-25okbh2pj|快照链ID。

 |
|SnapshotName|String|否|FinanceJoshua|快照名称。

 |
|SnapshotType|String|否|all|快照类型。取值范围：

 -   auto：自动快照
-   user：手动创建的快照
-   all（默认）：所有快照类型

 |
|SourceDiskType|String|否|Data|快照源磁盘的磁盘类型。取值范围：

 -   System：根据系统盘创建的快照
-   Data：根据数据盘创建的快照

 |
|Status|String|否|all|快照状态。取值范围：

 -   progressing：正在创建的快照
-   accomplished：创建成功的快照
-   failed：创建失败的快照
-   all（默认）：所有快照状态

 |
|Tag.N.Key|String|否|FinanceDept|快照的标签键。N 的取值范围：1~20。一旦传入该值，则不允许为空字符串。最多支持 64 个字符，不能以 aliyun 和 acs: 开头，不能包含 http:// 或者 https:// 。

 |
|Tag.N.Value|String|否|FinanceDeptJoshua|快照的标签值。N 的取值范围：1~20。一旦传入该值，可以为空字符串。最多支持 128 个字符，不能以 aliyun 和 acs: 开头，不能包含 http:// 或者 https:// 。

 |
|Usage|String|否|none|有引用关系的资源类型。取值范围：

 -   image：使用快照 [CreateImage](~~25535~~)
-   disk：使用快照 [CreateDisk](~~25513~~)
-   image\_disk：使用快照创建了数据盘和自定义镜像
-   none：暂无引用关系

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|PageNumber|Integer|1|快照列表的页码

 |
|PageSize|Integer|10|输入时设置的每页行数

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID

 |
|Snapshots| | |快照详情集合

 |
|└CreationTime|String|2014-07-24T13:00:52Z|创建时间。按照 [ISO8601](~~25696~~) 标准表示，并需要使用 UTC 时间。格式为：yyyy-MM-ddThh:mmZ

 |
|└Description|String|FinanceDept|描述信息。

 |
|└Encrypted|Boolean|false|该快照是否加密。

 |
|└KMSKeyId|String|0e478b7a-4262-4802-b8cb-00d3fb40826X|数据盘对应的KMS密钥ID。

 |
|└ProductCode|String|jxsc000204|从镜像市场继承的产品编号。

 |
|└Progress|String|100|快照创建进度，单位为百分比。

 |
|└RemainTime|Integer|38|正在创建的快照剩余完成时间，单位为秒。

 |
|└ResourceGroupId|String|rg-resourcegrouid|资源组ID。

 |
|└RetentionDays|Integer|30|自动快照保留天数。

 |
|└SnapshotId|String|s-snapshotid1|快照 ID。

 |
|└SnapshotName|String|FinanceJoshua|快照显示名称。如果创建时指定了快照显示名称，则返回。

 |
|└SourceDiskId|String|d-diskid1|源磁盘ID，如果快照的源磁盘已经被删除，该字段仍旧保留。

 |
|└SourceDiskSize|String|2000|源磁盘容量，单位：GB。

 |
|└SourceDiskType|String|Data|源磁盘属性。取值范围：System|Data

 |
|└SourceStorageType|String|disk|原磁盘类型。

 **说明：** 该参数即将被弃用，为提高兼容性，建议您尽量使用其他参数。

 |
|└Status|String|accomplished|快照状态。取值范围：

 -   progressing
-   accomplished
-   failed

 |
|└Tags| | |标签。

 |
|└TagKey|String|test|快照的标签键。

 |
|└TagValue|String|api|快照的标签值。

 |
|└Usage|String|none|有引用关系的资源类型。取值范围：

 -   image
-   disk
-   image\_disk
-   none

 |
|TotalCount|Integer|36|快照总个数。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

https://ecs.aliyuncs.com/?Action=DescribeSnapshots
&RegionId=cn-hangzhou
&InstanceId=i-instanceid1
&DiskId=d-diskid1
&SnapshotIds=["s-xxxxxxxxx", "s-yyyyyyyyy", … "s-zzzzzzzzz"]
&PageNumber=1
&PageSize=10
&SnapshotName=FinanceJoshua
&Status=all
&SnapshotType=all
&Usage=none
&SourceDiskType=Data
&Tag.1.Key=FinanceDept
&Tag.1.Value=FinanceDeptJoshua
&Encrypted=false
&DryRun=false
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeSnapshotsResponse>
  <Snapshots>
    <Snapshot>
      <CreationTime>2014-07-24T13:00:52Z</CreationTime>
      <Description/>
      <SourceDiskId>d-23x0r79qy</SourceDiskId>
      <SourceDiskType>DATA</SourceDiskType>
      <ProductCode/>
      <SnapshotName>auto_20140724_2</SnapshotName>
      <Progress>100%</Progress>
      <SourceDiskSize>50</SourceDiskSize>
      <Status>accomplished</Status>
      <SnapshotId>s-23f2i9s4t</SnapshotId>
      <Usage>none</Usage>
    </Snapshot>
    <Snapshot>
      <CreationTime>2014-07-24T13:00:42Z</CreationTime>
      <Description/>
      <SourceDiskId>101-70105379</SourceDiskId>
      <SourceDiskType>DATA</SourceDiskType>
      <ProductCode/>
      <SnapshotName>auto_20140724_2</SnapshotName>
      <Progress>100%</Progress>
      <SourceDiskSize>5</SourceDiskSize>
      <Status>accomplished</Status>
      <SnapshotId>s-23izto5qm</SnapshotId>
      <Usage>none</Usage>
    </Snapshot>
  </Snapshots>
  <PageNumber>1</PageNumber>
  <PageSize>2</PageSize>
  <TotalCount>36</TotalCount>
  <RequestId>2F409D67-329A-4405-B924-2FC28566B366</RequestId>
</DescribeSnapshotsResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"PageNumber":1,
	"TotalCount":36,
	"PageSize":2,
	"RequestId":"659F91C6-1949-43B0-90C4-B6342CA757D5",
	"Snapshots":{
		"Snapshot":[
			{
				"CreationTime":"2015-07-30T05:00:14Z",
				"Status":"accomplished",
				"SnapshotName":"auto_20150730_3",
				"SourceDiskType":"system",
				"SourceDiskId":"d-944qyqjfa",
				"SnapshotId":"s-943ypfgic",
				"SourceDiskSize":20,
				"Progress":"100%",
				"Usage":"none"
			},
			{
				"CreationTime":"2015-07-30T05:00:14Z",
				"Status":"accomplished",
				"SnapshotName":"auto_20150730_3",
				"SourceDiskType":"system",
				"SourceDiskId":"d-94j355jsq",
				"SnapshotId":"s-94osg320e",
				"SourceDiskSize":20,
				"Progress":"100%",
				"Usage":"none"
			}
		]
	}
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|403|InvalidSnapshotIds.Malformed|The amount of specified specified snapshot Ids exceeds the limit.|快照ID参数格式不正确。|
|404|InvalidFilterKey.NotFound| |指定的起始时间或到期时间参数错误。|
|404|InvalidFilterValue| |您输了的时间格式不合法。|
|404|InvalidUsage|The specifed Usage is not valid|指定有引用关系的资源类型（image、disk、image\_disk、none）不合法。|
|404|InvalidSourceDiskType|The specifed SourceDiskType is not valid|指定的快照源磁盘的磁盘类型不合法。|
|404|InvalidStatus.NotFound|The specified Status is not found|指定的资源状态不存在。|
|404|InvalidSnapshotType.NotFound|The specfied SnapshotType is not found|指定的快照类型不存在。|
|400|InvalidTag.Mismatch|The specified Tag.n.Key and Tag.n.Value are not match.|指定的 Tag.n.Key 和 Tag.n.Value 不匹配。|
|400|InvalidTagCount|The specified tags are beyond the permitted range.|指定的标记超出取值范围。|
|500|InternalError|The request processing has failed due to some unknown error.|内部错误，请重试。如果多次尝试失败，请提交工单|
|404|InvalidSnapshotLinkId.NotFound|The specified snapshot link is not found.|指定的快照链不存在。|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Ecs)

