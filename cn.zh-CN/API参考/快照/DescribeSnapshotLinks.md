# DescribeSnapshotLinks {#doc_api_Ecs_DescribeSnapshotLinks .reference}

调用DescribeSnapshotLinks查询云盘快照链。快照链是一块云盘所有快照组成的关系链，一块云盘对应一条快照链。

## 接口说明 {#description .section}

调用该接口时，您需要注意：

-   请求参数 `RegionId`、`DiskIds` 和 `InstanceId` 等充当过滤器功能，参数间是逻辑与关系。
-   如果不指定任何参数，则过滤器不起作用。当 `DiskIds` 和 `SnapshotLinkIds` 都为空数组时，同样视该过滤器有效，但是返回结果为空。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=DescribeSnapshotLinks)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|RegionId|String|是|cn-hangzhou|云盘所属于的地域 ID。您可以调用 [DescribeRegions](~~25609~~) 查看最新的阿里云地域列表。

 |
|Action|String|否|DescribeSnapshotLinks|系统规定参数。取值：DescribeSnapshotLinks

 |
|DiskIds|String|否|\["d-xxxxxxxxx", "d-yyyyyyyyy", … "d-zzzzzzzzz"\]|云盘 ID。一次最多指定 100 个云盘 ID。DiskIds 参数取值格式为 JSON 数组，ID 之间用半角逗号（,）隔开。

 |
|InstanceId|String|否|i-instanceid1|实例 ID。

 |
|PageNumber|Integer|否|1|云盘状态列表的页码。起始值：1

 默认值：1

 |
|PageSize|Integer|否|10|分页查询时设置的每页行数。取值范围：1~50。

 默认值：10

 |
|SnapshotLinkIds|String|否|\["sl-xxxxxxxxx", "sl-yyyyyyyyy", … "sl-zzzzzzzzz"\]|快照链 ID。一次最多指定 100 个快照 ID。SnapshotLinkIds参数取值格式为 JSON 数组，ID 之间用半角逗号（,）隔开。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|PageNumber|Integer|1|快照链列表的页码

 |
|PageSize|Integer|10|输入时设置的每页行数

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID

 |
|SnapshotLinks| | |快照链信息组成的集合

 |
|InstanceId|String|i-instanceid1|实例ID

 |
|InstanceName|String|FinanceJoshua|实例名称

 |
|RegionId|String|cn-hangzhou|快照链源磁盘所属地域 ID

 |
|SnapshotLinkId|String|sl-2ze0y1jwzpb1geqxk\*\*\*|快照链 ID

 |
|SourceDiskId|String|d-diskid1|源磁盘 ID，如果快照的源磁盘已经被删除，该字段仍旧保留

 |
|SourceDiskName|String|FinanceJoshua|源磁盘的名称

 |
|SourceDiskSize|Integer|40|源磁盘容量，单位为 GiB

 |
|SourceDiskType|String|cloud\_ssd|源磁盘的类型。取值范围：

 -   cloud：普通云盘
-   cloud\_efficiency：高效云盘
-   cloud\_ssd：SSD 云盘
-   ephemeral\_ssd：本地 SSD 盘
-   cloud\_essd：ESSD 云盘。

 |
|TotalCount|Integer|1|快照总个数

 |
|TotalSize|Integer|2097152|快照链中所有快照的大小，单位为 Byte

 |
|TotalCount|Integer|9|快照链总个数

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

https://ecs.aliyuncs.com/?Action=DescribeSnapshotLinks
&RegionId=cn-hangzhou
&InstanceId=i-instanceid1
&DiskIds=["d-xxxxxxxxx", "d-yyyyyyyyy", … "d-zzzzzzzzz"]
&SnapshotLinkIds=["sl-xxxxxxxxx", "sl-yyyyyyyyy", … "sl-zzzzzzzzz"]
&PageNumber=1
&PageSize=10
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeSnapshotLinksResponse>
  <SnapshotLinks>
    <SnapshotLink>
      <SnapshotLinkId>sl-25okbh2**</SnapshotLinkId>
      <SourceDiskId>d-25okbh2**</SourceDiskId>
      <SourceDiskType>data</SourceDiskType>
      <SourceDiskSize>20</SourceDiskSize>
      <RegionId> cn-beijing-btc-a01</RegionId>
      <TotalCount>1</TotalCount>
      <TotalSize>2097152</TotalSize>
    </SnapshotLink>
    <SnapshotLink>
      <SnapshotLinkId>sl-2ze0y1j**</SnapshotLinkId>
      <SourceDiskId>d-2ze0y1j**</SourceDiskId>
      <SourceDiskType>system</SourceDiskType>
      <SourceDiskSize>40</SourceDiskSize>
      <RegionId> cn-beijing-btc-a01</RegionId>
      <TotalCount>1</TotalCount>
      <TotalSize>2097152</TotalSize>
    </SnapshotLink>
  </SnapshotLinks>
  <PageNumber>1</PageNumber>
  <PageSize>2</PageSize>
  <TotalCount>9</TotalCount>
  <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</DescribeSnapshotLinksResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"PageNumber":1,
	"TotalCount":9,
	"PageSize":2,
	"RequestId":"473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E",
	"SnapshotLinks":{
		"SnapshotLink":[
			{
				"TotalCount":1,
				"SourceDiskType":"data",
				"SourceDiskId":"d-25okbh2**",
				"RegionId":"cn-beijing-btc-a01",
				"SourceDiskSize":20,
				"SnapshotLinkId":"sl-25okbh2**",
				"TotalSize":2097152
			},
			{
				"TotalCount":1,
				"SourceDiskType":"data",
				"SourceDiskId":"d-2ze0y1**",
				"RegionId":"cn-beijing-btc-a01",
				"SourceDiskSize":40,
				"SnapshotLinkId":"sl-2ze0y1j**",
				"TotalSize":2097152
			}
		]
	}
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InvalidRegionId|The specified regionId is invalid.|指定的 RegionId 不合法。|
|400|InvalidSnapshotLinkIds|The specified snapshotLinkIds is invalid.|指定的 SnapshotLinkId 不合法。|
|400|InvalidDiskIds|The specified diskIds is invalid.|指定的磁盘无效。|
|500|InternalError|The request processing has failed due to some unknown error.|内部错误，请重试。如果多次尝试失败，请提交工单|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

