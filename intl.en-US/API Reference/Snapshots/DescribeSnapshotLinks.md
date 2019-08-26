# DescribeSnapshotLinks {#doc_api_999634 .reference}

Queries the snapshot chains of one or more disks. A snapshot chain is a chain of all the snapshots of a disk, and a disk corresponds to a chain of snapshots, so the snapshot chain ID is the disk ID.

## Description {#description .section}

When you call this operation, note that:

-   Request parameters such as RegionId, DiskIds, and InstanceId act as filtering conditions and have a Boolean AND relationship.
-   If no parameters are specified, no filtering conditions are applied. If the DiskIds and SnapshotLinkIds parameters are empty JSON arrays \(\[\]\), the filtering conditions are regarded as effective and a blank result will be returned.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=DescribeSnapshotLinks) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|RegionId|String|Yes|cn-hangzhou| The ID of the region to which the disk belongs. You can call [DescribeRegions](~~25609~~) to view the latest regions of Alibaba Cloud.

 |
|Action|String|No|DescribeSnapshotLinks| The operation that you want to perform. Set the value to DescribeSnapshotLinks.

 |
|DiskIds|String|No|\["d-xxxxxxxxx", "d-yyyyyyyyy", … "d-zzzzzzzzz"\]| The IDs of the disks to be queried. You can specify a maximum of 100 disk IDs at a time. The parameter value is an array of disk IDs separated with commas \(,\).

 |
|InstanceId|String|No|i-instanceid1| The ID of the instance.

 |
|PageNumber|Integer|No|1| The page number that you query in the disk status list. Starting value: 1.

 Default value: 1.

 |
|PageSize|Integer|No|10| The number of entries per page. Valid values: 1 to 50.

 Default value: 10.

 |
|SnapshotLinkIds|String|No|\["p-xxxxxxxxx", "p-yyyyyyyyy", … "p-zzzzzzzzz"\]| The IDs of the snapshot chains to be queried. You can specify a maximum of 100 snapshot chain IDs at a time. The parameter value is an array of snapshot chain IDs separated with commas \(,\).

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|PageNumber|Integer|1| The page number that you query in the snapshot chain list.

 |
|PageSize|Integer|10| The number of entries per page.

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request.

 |
|SnapshotLinks| | | A set of snapshot chains.

 |
|└InstanceId|String|i-instanceid1| The ID of the instance.

 |
|└ InstanceName|String|FinanceJoshua| The name of the instance.

 |
|└RegionId|String|cn-hangzhou| The ID of the region to which the source disk of the snapshot chain belongs.

 |
|└ SnapshotLinkId|String|p-2ze0y1jwzpb1geqxkroq| The ID of the snapshot chain.

 |
|└ SourceDiskId|String|d-diskid1| The ID of the source disk. This parameter is retained even after the source disk of the snapshot is deleted.

 |
|└ SourceDiskName|String|FinanceJoshua| The name of the source disk.

 |
|└ SourceDiskSize|Integer|40| The size of the source disk. Unit: GiB.

 |
|└ SourceDiskType|String|cloud\_ssd| The type of the source disk. Valid values:

 -   cloud: basic disk
-   cloud\_efficiency: ultra disk
-   cloud\_ssd: SSD
-   ephemeral\_ssd: local SSD
-   cloud\_essd: ESSD

 |
|└TotalCount|Integer|1| The total number of snapshots.

 |
|└ TotalSize|Integer|2097152| The size of all snapshots in a snapshot chain. Unit: Byte.

 |
|TotalCount|Integer|9| The total number of snapshot chains.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=DescribeSnapshotLinks
&RegionId=cn-hangzhou
&InstanceId=i-instanceid1
&DiskIds=["d-xxxxxxxxx", "d-yyyyyyyyy", … "d-zzzzzzzzz"]
&SnapshotLinkIds=["p-xxxxxxxxx", "p-yyyyyyyyy", … "p-zzzzzzzzz"]
&PageNumber=1
&PageSize=10
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<DescribeSnapshotLinksResponse>
  <SnapshotLinks>
    <SnapshotLink>
      <SnapshotLinkId>d-25okbh2pj</SnapshotLinkId>
      <SourceDiskId>d-25okbh2pj</SourceDiskId>
      <SourceDiskType>data</SourceDiskType>
      <SourceDiskSize>20</SourceDiskSize>
      <RegionId> cn-beijing-btc-a01</RegionId>
      <TotalCount>1</TotalCount>
      <TotalSize>2097152</TotalSize>
    </SnapshotLink>
    <SnapshotLink>
      <SnapshotLinkId>d-2ze0y1jwzpb1geqxkroq</SnapshotLinkId>
      <SourceDiskId>d-2ze0y1jwzpb1geqxkroq</SourceDiskId>
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
  <RequestId>ED5CF6DD-71CA-462C-9C94-A61A78A01479</RequestId>
</DescribeSnapshotLinksResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"PageNumber":1,
	"TotalCount":9,
	"PageSize":2,
	"RequestId":"ACD9BBB0-A9D1-46D7-9630-B7A69889E110",
	"SnapshotLinks":{
		"SnapshotLink":[
			{
				"TotalCount":1,
				"SourceDiskType":"data",
				"SourceDiskId":"d-25okbh2pj",
				"RegionId":"cn-beijing-btc-a01",
				"SourceDiskSize":20,
				"SnapshotLinkId":"d-25okbh2pj",
				"TotalSize":2097152
			},
			{
				"TotalCount":1,
				"SourceDiskType":"data",
				"SourceDiskId":"d-2ze0y1jwzpb1geqxkroq",
				"RegionId":"cn-beijing-btc-a01",
				"SourceDiskSize":40,
				"SnapshotLinkId":"d-2ze0y1jwzpb1geqxkroq",
				"TotalSize":2097152
			}
		]
	}
}
```

## Error codes {#section_0jt_1m3_4ra .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|400|InvalidDiskIds|The specified diskIds is invalid.|The error message returned when the specified value of the DiskIds parameter is invalid.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

