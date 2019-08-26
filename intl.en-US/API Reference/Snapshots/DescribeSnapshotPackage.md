# DescribeSnapshotPackage {#doc_api_1006029 .reference}

Queries the storage plans that you have purchased within an Alibaba Cloud region. These storage plans can be used to store snapshots.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=DescribeSnapshotPackage) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|RegionId|String|Yes|cn-hangzhou| The ID of the region to which the snapshot belongs. You can call [DescribeRegions](~~25609~~) to view the latest regions of Alibaba Cloud.

 |
|Action|String|No|DescribeSnapshotPackage| The operation that you want to perform. Set the value to DescribeSnapshotPackage.

 |
|PageNumber|Integer|No|1| The page number that you query in the OSS storage plan list. Starting value: 1.

 Default value: 1.

 |
|PageSize|Integer|No|10| The number of entries per page. Maximum value: 100.

 Default value: 10.

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|PageNumber|Integer|1| The page number that you query in the OSS storage plan list.

 |
|PageSize|Integer|10| The number of entries per page.

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request.

 |
|SnapshotPackages| | | The OSS storage plan information.

 |
|└DisplayName|String|FinanceJoshua| The name of the OSS storage plan.

 |
|└EndTime|String|2018-11-30T06:32:31Z| The time when the OSS storage plan expires. The time follows the [ISO 8601](~~25696~~) standard and uses UTC time. The format is yyyy-MM-ddTHH:mm:ssZ.

 |
|└InitCapacity|Long|500| The storage space offered by the OSS storage plan.

 |
|└StartTime|String|2017-11-30T06:32:31Z| The time when the OSS storage plan was purchased. The time follows the [ISO 8601](~~25696~~) standard and uses UTC time. The format is yyyy-MM-ddTHH:mm:ssZ.

 |
|TotalCount|Integer|1| The total number of OSS storage plans.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=DescribeSnapshotPackage
&RegionId=cn-hangzhou
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<DescribeSnapshotPackageResponse>
  <TotalCount>1</TotalCount>
  <PageNumber>1</PageNumber>
  <PageSize>5</PageSize>
  <SnapshotPackages>
    <SnapshotPackage>
      <StartTime>2017-11-30T06:32:31Z</StartTime> 
      <EndTime>2018-11-30T06:32:31Z</EndTime> 
      <InitCapacity>500</InitCapacity> 
      <DisplayName>sp-snapshotpackage1</DisplayName> 
    </SnapshotPackage>
  </SnapshotPackages>
  <RequestId>ACD9BBB0-A9D1-46D7-9630-B7A69889E110</RequestId>
</DescribeSnapshotPackageResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"SnapshotPackages":{
		"SnapshotPackage":[
			{
				"InitCapacity":"500",
				"EndTime":"2018-11-30T06:32:31Z",
				"StartTime":"2017-11-30T06:32:31Z",
				"DisplayName":"sp-snapshotpackage1"
			}
		]
	},
	"PageNumber": "1",
	"TotalCount":"1",
	"PageSize":"5",
	"RequestId":"ACD9BBB0-A9D1-46D7-9630-B7A69889E110"
}
```

## Error codes {#section_l8o_spy_cqt .section}

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

