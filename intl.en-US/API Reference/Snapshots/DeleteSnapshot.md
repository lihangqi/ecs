# DeleteSnapshot {#doc_api_999641 .reference}

Deletes a snapshot. Snapshots that are currently being created can also be deleted by calling this operation.

## Description {#description .section}

When you call this operation, note that:

-   If the specified snapshot does not exist, the request will be ignored.
-   A snapshot that has already been used to create custom images cannot be deleted. A snapshot can be deleted only after the created custom images have been deleted \([DeleteImage](~~25537~~)\).

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=DeleteSnapshot) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|SnapshotId|String|Yes|s-snapshotid1| The ID of the snapshot.

 |
|Action|String|No|DeleteSnapshot| The operation that you want to perform. Set the value to DeleteSnapshot.

 |
|Force|Boolean|No|false| Indicates whether to force delete snapshots associated with the disk.

 **Note:** A disk cannot be reinitialized after its associated snapshots are deleted.

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=DeleteSnapshot
&SnapshotId=s-snapshotid1
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<DeleteSnapshotResponse>
  <RequestId>CEF72CEB-54B6-4AE8-B225-F876FF7BA984</RequestId>
</DeleteSnapshotResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":" CEF72CEB-54B6-4AE8-B225-F876FF7BA984"
}
```

## Error codes {#section_pcc_pli_wzn .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|403|SnapshotCreatedImage|The snapshot has been used to create user defined image\(s\).|The error message returned when the specified snapshot has been used to create custom images. You must delete the associated images before deleting the snapshot. If you force delete the snapshot, the images associated with the snapshot will become unavailable.|
|403|SnapshotCreatedDisk|The snapshot has been used to create disk\(s\).|The error message returned when the specified snapshot has been used to create disks.|
|400|MissingParameter|The input parameter SnapshotId that is mandatory for processing this request is not supplied.|The error message returned when the required SnapshotId parameter is not specified.|
|404|InvalidSnapshotId.NotFound|The specified snapshot is not found|The error message returned when the specified snapshot does not exist.|
|403|Operation.Conflict|The operation may conflicts with others, please retry later.|The error message returned when the current operation conflicts with other operations.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

