# DeleteDisk {#doc_api_1030731 .reference}

Releases a Pay-As-You-Go data disk. You can release a basic disk, an ultra disk, or an SSD.

## Description {#description .section}

When you call this operation, note that:

-   This operation does not delete manual snapshots of your disk.
-   You can call [ModifyDiskAttribute](~~25517~~) to configure whether automatic snapshots are retained or released together with the disk. We recommend that you delete unnecessary snapshots to ensure enough snapshot data storage for periodical automatic snapshot policies.
-   When you release a disk, the disk must be in the Available state.
-   If no disk with the specified ID exists, the request will be ignored.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=DeleteDisk) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|DiskId|String|Yes|d-23jbf2v5m| The ID of the disk to be released.

 |
|Action|String|No|DeleteDisk| The operation that you want to perform. Set the value to DeleteDisk.

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=DeleteDisk
&DiskId=d-23jbf2v5m
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<DeleteDiskResponse>
  <RequestId>CEF72CEB-54B6-4AE8-B225-F876FF7BA984</RequestId>
</DeleteDiskResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":" CEF72CEB-54B6-4AE8-B225-F876FF7BA984"
}
```

## Error codes {#section_4f5_t0k_022 .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|403|DiskCreatingSnapshot|The operation is denied due to a snapshot of the specified disk is|The error message returned when a snapshot of the specified disk is currently being created.|
|403|DiskStillAttached|The disk is still attached to the disk.|The error message returned when the disk to be released is still attached to the disk.|
|403|UserNotInTheWhiteList|The user is not in disk white list.|The error message returned when you are not authorized to use the specified disk.|
|400|InvalidRegionId.MalFormed|The specified parameter RegionId is not valid.|The error message returned when the specified value of the RegionId parameter is invalid.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

