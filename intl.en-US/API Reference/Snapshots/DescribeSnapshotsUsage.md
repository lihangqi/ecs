# DescribeSnapshotsUsage {#doc_api_999637 .reference}

Queries the number of snapshots stored in a region as well as their total size. If you want to view the snapshot usage information for each disk in a region, we recommend that you call the DescribeSnapshotLinks operation to query snapshot chain information.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=DescribeSnapshotsUsage) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|RegionId|String|Yes|cn-hangzhou| The ID of the region to which the snapshot belongs. You can call [DescribeRegions](~~25609~~) to view the latest regions of Alibaba Cloud.

 |
|Action|String|No|DescribeSnapshotsUsage| The operation that you want to perform. Set the value to DescribeSnapshotsUsage.

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request.

 |
|SnapshotCount|Integer|5| The number of snapshots stored in the current region.

 |
|SnapshotSize|Long|122| The total size of snapshots stored in the current region. Unit: Byte.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=DescribeSnapshotsUsage
&RegionId=cn-hangzhou
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<DescribeSnapshotsUsageResponse>
  <SnapshotCount>5</SnapshotCount>
  <SnapshotSize>122</SnapshotSize>
  <RequestId>ED5CF6DD-71CA-462C-9C94-A61A78A01479</RequestId>
</DescribeSnapshotsUsageResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"SnapshotSize":"122",
	"RequestId":"ACD9BBB0-A9D1-46D7-9630-B7A69889E110",
	"SnapshotCount":"5"
}
```

## Error codes {#section_fsi_pre_b14 .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|403|InvalidParam. RegionId|The specified region does not exist.|The error message returned when the specified region does not exist.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

