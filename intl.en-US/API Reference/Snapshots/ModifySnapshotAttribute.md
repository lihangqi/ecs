# ModifySnapshotAttribute {#doc_api_Ecs_ModifySnapshotAttribute .reference}

You can call the ModifySnapshotAttribute operation to modify the name or description of a snapshot.

## Debugging {#api_explorer .section}

[Alibaba Cloud provides OpenAPI Explorer to simplify API usage. You can use OpenAPI Explorer to search for APIs, call APIs, and dynamically generate SDK example code.](https://api.aliyun.com/#product=Ecs&api=ModifySnapshotAttribute&type=RPC&version=2014-05-26)

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description |
|---------|----|--------|-------|------------|
|SnapshotId|String|Yes|s-923FE2B\*\*|The ID of the snapshot to be modified.

 |
|Action|String|No|ModifySnapshotAttribute|The operation that you want to perform. For API requests using the HTTP and HTTPS methods, `Action` is required. Set this parameter to ModifySnapshotAttribute.

 |
|Description|String|No|NewSnapshotDescription-EcsGuideTest|The description of the snapshot. It must be 2 to 256 characters in length and cannot start with http:// or https://.

 |
|SnapshotName|String|No|NewSnapshotName-EcsGuideTest|The name of the snapshot. It must be 2 to 128 characters in length. It must start with a letter but cannot start with http:// or https://. It can contain letters, digits, colons \(:\), underscores \(\_\), and hyphens \(-\).

 It cannot start with auto because a name that starts with auto may conflict with the name of an automatic snapshot.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request.

 |

## Examples {#demo .section}

Sample request

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=ModifySnapshotAttribute
&SnapshotName=NewSnapshotName-EcsGuideTest
&Description=NewSnapshotDescription-EcsGuideTest
&<Common request parameters>
```

Sample success response

`XML` format

``` {#xml_return_success_demo}
<ModifySnapshotAttributeResponse>
            <RequestId>C8B26B44-0189-443E-9816-D951F59623A9</RequestId>
</ModifySnapshotAttributeResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"C8B26B44-0189-443E-9816-D951F59623A9"
}
```

## Error codes { .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|404|InvalidDescription.Malformed|The specified description is wrongly formed.|The error message returned because the specified resource description is invalid. The description must be 2 to 256 characters in length and cannot start with http:// or https://.|
|400|InvalidSnapshotName.Malformed|The specified SnapshotName is wrongly formed.|The error message returned because the specified snapshot name is invalid. The name must be 2 to 128 characters in length and contain letters, digits, periods \(,\), underscores \(\_\), and hyphens \(-\). It must start with a letter but cannot start with http:// or https://.|
|400|NoAttributeToModify|No attribute to be modified in this request.|The error message returned because no properties of the specified snapshot are modified.|
|404|InvalidSnapshotId.NotFound|The specified SnapshotId does not exist.|The error message returned because the specified snapshot does not exist. Check whether the snapshot ID is correct.|

