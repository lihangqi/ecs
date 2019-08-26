# ModifyDiskAttribute {#doc_api_999555 .reference}

Modifie the attributes of a disk.

## Description {#description .section}

If an instance is locked for security reasons \(the OperationLocks parameter is "LockReason": "security"\), the DeleteWithInstance attribute will be ignored and the disk will be released together with the instance.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=ModifyDiskAttribute) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|DiskId|String|Yes|d-diskid1| The ID of the disk to be modified.

 |
|Action|String|No|ModifyDiskAttribute| The operation that you want to perform. Set the value to ModifyDiskAttribute.

 |
|DeleteAutoSnapshot|Boolean|No|false| Indicates whether the automatic snapshot is deleted when the disk is released. Default value: null, indicating that the parameter value remains unchanged.

 |
|DeleteWithInstance|Boolean|No|false| Indicates whether the disk is released together with the instance: Default value: null, indicating that the parameter value remains unchanged.

 An error will be returned if you set the DeleteWithInstance attribute to false in the following cases:

 -   When the Category attribute of a disk is set to ephemeral.
-   When the Category attribute of a disk is set to cloud and the Portable attribute is set to false.

 |
|Description|String|No|FinanceDeptJoshua| The description of the disk. The description must be 2 to 256 characters in length and cannot start with http:// or https://.

 |
|DiskName|String|No|FinanceJoshua| The name of the disk. The name must be 2 to 128 characters in length. It must start with a letter and cannot start with http:// or https://. It can contain letters, digits, colons \(:\), underscores \(\_\), and hyphens \(-\).

 |
|EnableAutoSnapshot|Boolean|No|true| Indicates whether to apply a created automatic snapshot policy to the disk. Default value: null, indicating that the parameter value remains unchanged.

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=ModifyDiskAttribute
&DiskId=d-23jbf2v5m
&DiskName=MyDiskName 
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<ModifyDiskAttributeResponse>
  <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId> 
</ModifyDiskAttributeResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E"
}
```

## Error codes {#section_qa6_nwl_9ca .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|404|InvalidDescription.Malformed|The specified description is wrongly formed.|The error message returned when the specified description is invalid. The description must be 2 to 256 characters in length and cannot start with http:// or https://.|
|403|QuotaExceed.Snapshot|The snapshot quota exceeds.|The error message returned when the snapshot quota has been exhausted. To store new snapshots, you can delete existing snapshots without affecting your business.|
|400|IncompleteParamter|Some fields can not be null in this request.|The error message returned when a required parameter is not specified.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

