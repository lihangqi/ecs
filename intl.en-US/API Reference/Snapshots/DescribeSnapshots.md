# DescribeSnapshots {#doc_api_1023709 .reference}

Queries all the snapshots of an ECS instance or a disk. Request parameters such as InstanceId, DiskId, and SnapshotIds act as filtering conditions and have a Boolean AND relationship.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=DescribeSnapshots) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|RegionId|String|Yes|cn-hangzhou| The ID of the region to which the disk belongs. You can call [DescribeRegions](~~25609~~) to view the latest regions of Alibaba Cloud.

 |
|Action|String|No|DescribeSnapshots| The operation that you want to perform. Set the value to DescribeSnapshots.

 |
|DiskId|String|No|d-diskid1| The ID of the disk.

 |
|DryRun|Boolean|No|false| Indicates whether the system performs a permission check only.

 -   true: Sends a permission check request, without querying resource status. The system checks whether your AccessKey is valid, whether RAM users are authorized, and whether the required parameters are set. For a failed check, the corresponding error message is returned. For a successful check, the DryRunOperation error code is returned.
-   False \(default\): Sends a normal request, returns the 2XX HTTP status code after the check and queries the resource status directly.

 |
|Encrypted|Boolean|No|false| Indicates whether to filter an encrypted snapshot. Default value: false.

 |
|Filter.1.Key|String|No|CreationStartTime| The filter key used to query resources. The parameter value must be the start time when the resource was created \(CreationStartTime\).

 **Note:** This parameter will be removed in the future. We recommend that you use other parameters to ensure compatibility.

 |
|Filter.1.Value|String|No|2017-12-05T22:40:00Z| The filter value used to query resources. The parameter value must be the start time when the resource was created \(CreationStartTime\).

 **Note:** This parameter will be removed in the future. We recommend that you use other parameters to ensure compatibility.

 |
|Filter.2.Key|String|No|CreationEndTime| The filter key used to query resources. The parameter value must be the end time when the resource was created \(CreationEndTime\).

 **Note:** This parameter will be removed in the future. We recommend that you use other parameters to ensure compatibility.

 |
|Filter.2.Value|String|No|2017-12-06T22:40:00Z| The filter value used to query resources. The parameter value must be the end time when the resource was created \(CreationEndTime\).

 **Note:** This parameter will be removed in the future. We recommend that you use other parameters to ensure compatibility.

 |
|InstanceId|String|No|i-instanceid1| The ID of the instance.

 |
|KMSKeyId|String|No|0e478b7a-4262-4802-b8cb-00d3fb40826X| The ID of the KMS key corresponding to the data disk.

 |
|PageNumber|Integer|No|1| The page number that you query in the snapshot list. Starting value: 1.

 Default value: 1.

 |
|PageSize|Integer|No|10| The number of entries per page. Maximum value: 100.

 Default value: 10.

 |
|ResourceGroupId|String|No|rg-resourcegrouid| The ID of the resource group.

 |
|SnapshotIds|String|No|\["s-xxxxxxxxx", "s-yyyyyyyyy", … "s-zzzzzzzzz"\]| The IDs of the snapshots. The parameter value is an array of snapshot IDs separated with commas \(,\). You can specify a maximum of 100 IDs.

 |
|SnapshotLinkId|String|No|d-25okbh2pj| The ID of the snapshot chain.

 |
|SnapshotName|String|No|FinanceJoshua| The name of the snapshot.

 |
|SnapshotType|String|No|all| The type of the snapshot. Valid values:

 -   auto: automatic snapshot
-   user: manually created snapshot
-   all \(default\): all snapshot types

 |
|SourceDiskType|String|No|Data| The type of the source disk. Valid values:

 -   System: The snapshot is created for a system disk.
-   Data: The snapshot is created for a data disk.

 |
|Status|String|No|all| The status of the snapshot. Valid values:

 -   progressing: The snapshot is being created.
-   accomplished: The snapshot is created.
-   failed: The snapshot failed to be created.
-   all \(default\): all snapshot statuses

 |
|Tag.N.Key|String|No|FinanceDept| The tag key of the snapshot. Valid values of N: 1 to 20. It cannot be a null string. It can be a maximum of 64 characters in length. It cannot start with aliyun or acs:. It cannot contain http:// or https://.

 |
|Tag.N.Value|String|No|FinanceDeptJoshua| The tag value of the snapshot. Valid values of N: 1 to 20. It can be a null string. It can be a maximum of 128 characters in length. It cannot start with aliyun or acs:. It cannot contain http:// or https://.

 |
|Tag.N.key|String|No|FinanceDept| The tag key of the snapshot.

 **Note:** This parameter will be removed in the future. We recommend that you use the Tag.N.Key parameter to ensure compatibility.

 |
|Tag.N.value|String|No|FinanceDeptJoshua| The tag value of the snapshot.

 **Note:** This parameter will be removed in the future. We recommend that you use the Tag.N.Key parameter to ensure compatibility.

 |
|Usage|String|No|none| The referenced resource type. Valid values:

 -   image: The snapshot is used to [create custom images](~~25535~~).
-   disk: The snapshot is used to [create disks](~~25513~~).
-   image\_disk: The snapshot is used to create custom images and data disks.
-   none: The snapshot is not referenced by any other resources.

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|PageNumber|Integer|1| The page number that you query in the snapshot list.

 |
|PageSize|Integer|10| The number of entries per page.

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request.

 |
|Snapshots| | | The snapshot details.

 |
|└ CreationTime|String|2014-07-24T13:00:52Z| The creation time of the snapshot. The time follows the [ISO 8601](~~25696~~) standard and uses UTC time. The format is yyyy-MM-ddThh:mmZ.

 |
|└Description|String|FinanceDept| The description of the snapshot.

 |
|└Encrypted|Boolean|false| Indicates whether the snapshot is encrypted.

 |
|└ KMSKeyId|String|0e478b7a-4262-4802-b8cb-00d3fb40826X| The ID of the KMS key corresponding to the data disk.

 |
|└ProductCode|String|jxsc000204| The product code in the image marketplace.

 |
|└Progress|String|100| The progress of snapshot creation. Unit: percent \(%\).

 |
|└ RemainTime|Integer|38| The time remaining for a snapshot creation task before it is completed. Unit: second.

 |
|└ResourceGroupId|String|rg-resourcegrouid| The ID of the resource group.

 |
|└RetentionDays|Integer|30| The number of days that an automatic snapshot retains in the console for your instance.

 |
|└ SnapshotId|String|s-snapshotid1| The ID of the snapshot.

 |
|└SnapshotName|String|FinanceJoshua| The name of the snapshot. This parameter is returned only if a snapshot name was specified during creation.

 |
|└ SourceDiskId|String|d-diskid1| The ID of the source disk. It is retained after the source disk of the snapshot is deleted.

 |
|└ SourceDiskSize|String|2000| The size of the source disk. Unit: GB.

 |
|└ SourceDiskType|String|Data| The type of the source disk. Valid values: System | Data.

 |
|└ SourceStorageType|String|disk| The type of the source disk.

 **Note:** This parameter will be removed in the future. We recommend that you use other parameters to ensure compatibility.

 |
|└Status|String|accomplished| The status of the snapshot. Valid values:

 -   progressing
-   accomplished
-   failed

 |
|└Tags| | | The tags.

 |
|└TagKey|String|test| The tag key of the snapshot.

 |
|└TagValue|String|api| The tag value of the snapshot.

 |
|└ Usage|String|none| The referenced resource type. Valid values:

 -   image
-   disk
-   image\_disk
-   none

 |
|TotalCount|Integer|36| The total number of snapshots

 |

## Examples {#demo .section}

Sample requests

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
&<Common request parameters>
```

Successful response examples

`XML` format

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

`JSON` format

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

## Error codes {#section_6kb_y9k_f0s .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|403|InvalidSnapshotIds.Malformed|The amount of specified snapshot Ids exceeds the limit.|The error message returned when the specified value of the SnapshotIds parameter is invalid.|
|404|InvalidFilterKey.NotFound| |The error message returned when the specified start time or end time is incorrect.|
|404|InvalidFilterValue| |The error message returned when the format of the specified time is invalid.|
|404|InvalidUsage|The specified Usage is not valid|The error message returned when the specified referenced resource type \(image, disk, image\_disk, or none\) is invalid.|
|404|InvalidStatus.NotFound|The specified Status is not found|The error message returned when the specified resource status does not exist.|
|404|InvalidSnapshotType.NotFound|The specified SnapshotType is not found|The error message returned when the specified snapshot type does not exist.|
|400|InvalidTag.Mismatch|The specified Tag.n.Key and Tag.n.Value are not match.|The error message returned when the specified Tag.n.Key parameter does not correspond to the specified Tag.n.Value parameter.|
|400|InvalidTagCount|The specified tags are beyond the permitted range.|The error message returned when the number of specified tags has reached the upper limit.|
|404|InvalidSnapshotLinkId.NotFound|The specified snapshot link is not found.|The error message returned when the specified snapshot chain does not exist.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

