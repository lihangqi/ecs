# DescribeDisks {#doc_api_1032129 .reference}

Queries the list of disks.

## Description {#description .section}

-   Request parameters such as RegionId, ZoneId, DiskIds, and InstanceId act as filtering conditions and have a Boolean AND relationship with each other.
-   The DiskIds value is a JSON-formatted array. If the parameter is not specified, the filtering conditions are not applied. If the DiskIds parameter is an empty array, the filtering condition is applied and a blank result will be returned.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=DescribeDisks) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|RegionId|String|Yes|cn-hangzhou| The ID of the region to which the disk belongs. You can call [DescribeRegions](~~25609~~) to view the latest regions of Alibaba Cloud.

 |
|Action|String|No|DescribeDisks| The operation that you want to perform. Set the value to DescribeDisks.

 |
|AdditionalAttributes.N|RepeatList|No|null| Other attribute values.

 **Note:** This parameter will be removed in the future. We recommend that you use other parameters to ensure compatibility.

 |
|AutoSnapshotPolicyId|String|No|auto\_20140724\_2| The ID of the automatic snapshot policy.

 |
|Category|String|No|all| The category of the disk. Valid values:

 -   all: all disks
-   cloud: basic disk
-   cloud\_efficiency: ultra disk
-   cloud\_ssd: SSD
-   ephemeral: local I/O-intensive disk
-   local\_hdd\_pro: local throughput-intensive disk
-   local\_ssd\_pro: local disk
-   ephemeral\_ssd: local SSD
-   cloud\_essd: ESSD

 Default value: all.

 |
|DeleteAutoSnapshot|Boolean|No|false| Indicates whether the automatic snapshot is deleted when the disk is released. Valid values:

 -   true: The automatic snapshot is deleted when the disk is released.
-   False: The automatic snapshot is retained when the disk is released.

 Default value: false.

 |
|DeleteWithInstance|Boolean|No|false| Indicates whether the disk is released together with the instance. Valid values:

 -   true: When the instance is deleted, the disk will be released together with it.
-   false: When the instance is released, the disk will be retained.

 Default value: false.

 |
|DiskChargeType|String|No|PostPaid| The billing method of the disk. Valid values:

 -   PrePaid: Subscription
-   PostPaid: Pay-As-You-Go

 |
|DiskIds|String|No|\["d-xxxxxxxxx", "d-yyyyyyyyy", … "d-zzzzzzzzz"\]| The IDs of the disks. The parameter value is an array of disk IDs separated with commas \(,\). You can specify a maximum of 100 disk IDs at a time.

 |
|DiskName|String|No|JoshuaFinance| The name of the disk.

 |
|DiskType|String|No|all| The type of the disk. Valid values:

 -   all: queries both the system disk and data disks
-   system: queries the system disk only
-   data: queries data disks only

 Default value: all.

 |
|DryRun|Boolean|No|false| Indicates whether the system performs a permission check only.

 -   true: Sends a permission check request, without querying resource status. The system checks whether your AccessKey is valid, whether RAM users are authorized, and whether the required parameters are set. For a failed check, corresponding error message is returned. For a successful check, the `DryRunOperation` error code is returned.
-   false: Sends a normal request, returns the 2XX HTTP status code after the check, and queries the resource status directly.

 Default value: false.

 |
|EnableAutoSnapshot|Boolean|No|false| Indicates whether an automatic snapshot policy is applied to the disk. Your automatic snapshot policy must be enabled.

 Default value: false.

 |
|EnableAutomatedSnapshotPolicy|Boolean|No|false| Indicates whether an automatic snapshot policy is configured for the disk.

 **Note:** This parameter will be removed in the future. We recommend that you use other parameters to ensure compatibility.

 |
|EnableShared|Boolean|No|false| Indicates whether the disk is a shared block storage.

 |
|Encrypted|Boolean|No|false| Indicates whether encrypted disks are queried. Valid values:

 -   true: Only encrypted disks are queried.
-   false: Encrypted disks are not queried.

 Default value: false.

 |
|InstanceId|String|No|i-instance1| The ID of the instance.

 |
|KMSKeyId|String|No|0e478b7a-4262-4802-b8cb-00d3fb40826X| The ID of the KMS key corresponding to the data disk.

 |
|LockReason|String|No|recycling| The reason why the disk is locked. Valid values:

 -   financial: The disk is locked due to overdue payments.
-   security: The disk is locked for security reasons.
-   recycling: The preemptible instance is locked and is pending for release.
-   dedicatedhostfinancial: The ECS instance is locked because of overdue payments on the Dedicated Host.

 |
|PageNumber|Integer|No|1| The page number that you query in the disk status list. Starting value: 1.

 Default value: 1.

 |
|PageSize|Integer|No|10| The number of entries per page. Maximum value: 100.

 Default value: 10.

 |
|Portable|Boolean|No|true| Indicates whether the disk is detachable. This attribute cannot be modified. Valid values:

 -   true: The disk can be attached to or detached from instances within the same zone.
-   false: The disk cannot be detached, and is created or released together with the instance it is attached to.

 Disks whose Portable attribute is `true` can be attached or detached, except the following disks:

 -   Local disks
-   Local SSDs
-   System disks of the basic, ultra, ESSD, and SSD disk categories
-   Subscription-based disks of the basic, ultra, ESSD, and SSD categories

 The Portable attribute of the preceding disks is `false`.

 |
|ResourceGroupId|String|No|rg-resourcegroupid1| The ID of the resource group to which the disk belongs.

 |
|SnapshotId|String|No|s-snapshotid1| The ID of the snapshot used to create the disk.

 |
|Status|String|No|all| The status of the disk. For more information, see [Basic disk statuses](~~25689~~). Valid values:

 -   In\_use
-   Available
-   Attaching
-   Detaching
-   Creating
-   ReIniting
-   All

 Default value: All.

 |
|Tag.N.Key|String|No|FinanceJoshua| The tag key of the disk.

 |
|Tag.N.Value|String|No|FinanceDept| The tag value of the disk.

 |
|ZoneId|String|No|cn-hangzhou-g| The ID of the zone.

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|Disks| | | The disk information.

 |
|└AttachedTime|String|2018-01-01T01:04:22Z| The time when the disk is detached. The time follows the ISO 8601 standard and uses UTC time. The format is YYYY-MM-DDThh:mmZ. This parameter is valid only when the disk is in the Available state.

 |
|└AutoSnapshotPolicyId|String|s-23f2i9s4t| The ID of the automatic snapshot policy applied to the disk.

 |
|└Category|String|cloud\_ssd| The category of the disk. Valid values:

 -   cloud: basic disk
-   cloud\_efficiency: ultra disk
-   cloud\_ssd: SSD
-   ephemeral\_ssd: local SSD
-   ephemeral: local disk
-   cloud\_essd: ESSD

 |
|└CreationTime|String|2018-01-01T01:01:22Z| The creation time of the disk.

 |
|└DeleteAutoSnapshot|Boolean|false| Indicates whether the automatic snapshot is deleted when the disk is released.

 Snapshots created using [CreateSnapshot](~~25524~~) or on the console are retained permanently and not affected by this attribute.

 |
|└DeleteWithInstance|Boolean|true| Indicates whether the disk is released together with the instance. Valid values:

 -   true: When the instance is deleted, the disk will be released together with it.
-   false: When the instance is released, the disk will be retained.

 |
|└Description|String|FinanceDept| The description of the disk.

 |
|└DetachedTime|String|2018-01-08T01:01:22Z| The time when the disk is detached. This parameter is valid only when the disk is in the Available state.

 |
|└Device|String|/dev/xvdb| The device name of the instance that the disk is attached to, such as /dev/xvdb. It is null unless the disk is in the In\_use state.

 **Note:** This parameter is currently undergoing beta testing and has not yet been officially launched. We recommend that you do not use this parameter for the time being.

 |
|└DiskChargeType|String|PostPaid| The billing method of the disk. Valid values:

 -   PrePaid: Subscription
-   PostPaid: Pay-As-You-Go

 |
|└DiskId|String|d-23jbf2v5m| The ID of the disk.

 |
|└DiskName|String|FinanceDeptJoshua| The name of the disk.

 |
|└EnableAutoSnapshot|Boolean|false| Indicates whether an automatic snapshot policy is applied to the disk.

 Default value: false.

 |
|└EnableAutomatedSnapshotPolicy|Boolean|false| Indicates whether an automatic snapshot policy is applied to the disk.

 |
|└Encrypted|Boolean|false| Indicates whether the disk is encrypted.

 |
|└ExpiredTime|String|2018-01-10T01:01:22Z| The time when the subscription-based disk expires.

 |
|└IOPS|Integer|4000| The number of input/output operations per second. Unit: times/s.

 |
|└IOPSRead|Integer|2000| The number of I/O reads. Unit: times/s.

 |
|└IOPSWrite|Integer|2000| The number of I/O writes. Unit: times/s.

 |
|└ImageId|String|m-bp13aqm171qynt3udgd| The ID of the image from which the disk is created. It is null unless the disk is created from an image. The value of this parameter will remain unchanged throughout the lifecycle of the disk.

 |
|└InstanceId|String|i-instanceid1| The ID of the instance that the disk is attached to. It is null unless the disk is in the In\_use state.

 |
|└KMSKeyId|String|0e478b7a-4262-4802-b8cb-00d3fb40826X| The ID of the KMS key corresponding to the data disk.

 |
|└MountInstanceNum|Integer|1| The number of instances that a shared block storage can be attached to.

 |
|└MountInstances| | | The information about instance attachment.

 |
|└AttachedTime|String|2017-12-05T2340:00Z| The time when the disk is attached. The time follows the [ISO 8601](~~25696~~) standard and uses UTC time. The format is yyyy-MM-ddTHH:mm:ssZ.

 |
|└Device|String|/dev/xvda| The mount point of the disk.

 **Note:** This parameter is currently undergoing beta testing and has not yet been officially launched. We recommend that you do not use this parameter for the time being.

 |
|└InstanceId|String|i-instanceid1| The ID of the instance that the disk is attached to.

 |
|└OperationLocks| | | The reason why the disk is locked.

 |
|└LockReason|String|security| The reason why the disk is locked.

 |
|└PerformanceLevel|String|PL2| The performance level you select for an ESSD cloud disk. Valid values:

 -   PL1: The maximum random read/write IOPS of a single disk is 50,000.
-   PL2: The maximum random read/write IOPS of a single disk is 100,000.
-   PL3: The maximum random read/write IOPS of a single disk is 1,000,000.

 |
|└Portable|Boolean|false| Indicates whether the disk is detachable. Valid values:

 -   true: The disk is an independent basic disk. This type of disk can be attached to or detached from instances within the same zone.
-   false: The disk is not an independent basic disk. This type of disk is created or released together with the instance it is attached to.

 Disks whose Portable attribute is true can be attached \([AttachDisk](~~25515~~)\) or detached \([DetachDisk](~~25516~~)\). The Portable attribute of the following disks is false: system disks of the local, local SSD, basic, and SSD disk categories, and subscription-based basic disks. The Portable attribute of these disks cannot be modified.

 |
|└ProductCode|String|jxsc000204| The product code in Alibaba Cloud Marketplace.

 |
|└RegionId|String|cn-hangzhou| The ID of the region to which the disk belongs.

 |
|└ResourceGroupId|String|rg-resourcegroupid1| The ID of the resource group to which the disk belongs.

 |
|└Size|Integer|2000| The size of the disk. Unit: GiB.

 |
|└SourceSnapshotId|String|s-snapshotid1| The ID of the snapshot used to create the disk. It is null if no snapshot is used to create the disk. The value of this parameter will remain unchanged throughout the lifecycle of the disk.

 |
|└Status|String|Available| The status of the disk. Valid values:

 -   In\_use
-   Available
-   Attaching
-   Detaching
-   Creating
-   ReIniting

 |
|└Tags| | | A set of disk tags.

 |
|└TagKey|String|FinanceJoshua| The tag key of the disk.

 |
|└TagValue|String|FinanceDept| The tag value of the disk.

 |
|└Type|String|data| The type of the disk. Valid values:

 -   system: system disk
-   data: data disk

 |
|└ZoneId|String|cn-hangzhou-g| The ID of the zone to which the disk belongs.

 |
|PageNumber|Integer|1| The page number that you query in the disk list.

 |
|PageSize|Integer|10| The number of entries per page.

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request.

 |
|TotalCount|Integer|1| The total number of disks.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=DescribeDisks
&RegionId=cn-hangzhou 
&ZoneId=cn-hangzhou-g
&DiskIds=["d-disk1"]
&InstanceId=i-instance1 
&DiskType=all
&Category=all
&Status=all
&SnapshotId=s-snapshotid1
&Portable=true
&DeleteWithInstance=false
&DeleteAutoSnapshot=false
&PageNumber=1 
&PageSize=10 
&DiskName=JoshuaFinance
&AutoSnapshotPolicyId=auto_20140724_2
&EnableAutoSnapshot=false
&Encrypted=false
&DryRun=false
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<DescribeDisksResponse>
  <Disks>
    <Disk>
      <DeleteAutoSnapshot>true</DeleteAutoSnapshot>
      <DeleteWithInstance>false</DeleteWithInstance>
      <EnableAutoSnapshot>false</EnableAutoSnapshot>
      <Category>cloud</Category> 
      <Description/> 
      <DiskName/>
      <Size>5</Size>
      <Type>data</Type>
      <InstanceId/>
      <CreationTime>2014-07-23T02:44:07Z</CreationTime>
      <ImageId/>
      <ZoneId>cn-qingdao-b</ZoneId>
      <AttachedTime>2014-07-23T07:47:35Z</AttachedTime>
      <DetachedTime>2014-07-23T08:28:48Z</DetachedTime>
      <Device/>
      <OperationLocks/>
      <Portable>true</Portable>
      <ProductCode/>
      <RegionId>cn-qingdao</RegionId> 
      <DiskId>d-28m5zbua0</DiskId>
      <SourceSnapshotId/>
      <Status>Available</Status> 
    </Disk>
    <Disk>
      <DeleteAutoSnapshot>true</DeleteAutoSnapshot>
      <DeleteWithInstance>false</DeleteWithInstance>
      <EnableAutoSnapshot>false</EnableAutoSnapshot> 
      <Category>cloud</Category> 
      <Description/> 
      <DiskName/>
      <Size>5</Size> 
      <Type>data</Type>
      <InstanceId/>
      <CreationTime>2014-07-23T02:44:06Z</CreationTime>
      <ImageId/>
      <ZoneId>cn-qingdao-b</ZoneId>
      <AttachedTime/>
      <DetachedTime/>
      <Device/>
      <OperationLocks/>
      <Portable>true</Portable>
      <ProductCode/>
      <RegionId>cn-qingdao</RegionId> 
      <DiskId>d-28zfrmo13</DiskId>
      <SourceSnapshotId/>
      <Status>Available</Status> 
    </Disk>
  </Disks>
  <PageNumber>1</PageNumber> 
  <PageSize>2</PageSize>
  <TotalCount>9</TotalCount>
  <RequestId>ED5CF6DD-71CA-462C-9C94-A61A78A01479</RequestId> 
</DescribeDisksResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"PageNumber":1,
	"TotalCount":9,
	"PageSize":2,
	"RequestId":"ACD9BBB0-A9D1-46D7-9630-B7A69889E110",
	"Disks":{
		"Disk":[
			{
				"ImageId":"",
				"Description":"",
				"Device":"",
				"ProductCode":"",
				"Portable":true,
				"DetachedTime":"2014-07-23T08:28:48Z",
				"Type":"data",
				"InstanceId":"",
				"ZoneId":"cn-qingdao-b",
				"EnableAutoSnapshot":false,
				"DiskName":"",
				"AttachedTime":"2014-07-23T07:47:35Z",
				"SourceSnapshotId":"",
				"CreationTime":"2014-07-23T02:44:07Z",
				"Status":"Available",
				"DeleteAutoSnapshot":true,
				"Category":"cloud",
				"RegionId":"cn-qingdao",
				"DeleteWithInstance":false,
				"OperationLocks":{
					"OperationLock":[]
				},
				"DiskId":"d-28m5zbua0",
				"Size":5
			},
			{
				"ImageId":"",
				"Description":"",
				"Device":"",
				"ProductCode":"",
				"Portable":true,
				"DetachedTime":"",
				"Type":"data",
				"InstanceId":"",
				"ZoneId":"cn-qingdao-b",
				"EnableAutoSnapshot":false,
				"DiskName":"",
				"AttachedTime":"",
				"SourceSnapshotId":"",
				"CreationTime":"2014-07-23T02:44:06Z",
				"Status":"Available",
				"DeleteAutoSnapshot":true,
				"Category":"cloud",
				"RegionId":"cn-qingdao",
				"DeleteWithInstance":false,
				"OperationLocks":{
					"OperationLock":[]
				},
				"DiskId":"d-28zfrmo13",
				"Size":5
			}
		]
	}
}
```

## Errors {#section_zc3_g5k_73f .section}

|HTTP status code|Error code|Error message|Meaning|
|----------------|----------|-------------|-------|
|403|InvalidDiskIds.Malformed|The amount of specified disk Ids exceeds the limit.|The error message returned when the specified value of the DiskIds parameter is invalid.|
|404|InvalidDiskChargeType.NotFound|The DiskChargeType does not exist in our records|The error message returned when the specified disk type does not exist.|
|400|InvalidTag.Mismatch|The specified Tag.n.Key and Tag.n.Value are not match.|The error message returned when the specified Tag.n.Key parameter does not correspond to the specified Tag.n.Value parameter.|
|400|InvalidRegion.NotFound|The specified parameter RegionId is not valid.|The error message returned when the specified RegionId parameter is invalid.|
|400|InvalidZoneId.NotFound|The zoneId provided does not exist in our records.|The error message returned when the specified zone ID does not exist.|
|400|InvalidParamter|Some parameters are invalid in this request.|The error message returned when the request contains invalid parameter values.|
|400|InvalidSnapshot.NotFound|The specified parameter SnapshotId is not valid.|The error message returned when the specified value of the SnapshotId parameter is invalid.|
|404|InvalidDiskIds.ValueNotSupported|The specified parameter DiskIds is not supported.|The error message returned when the specified value of the DiskIds parameter is invalid.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

