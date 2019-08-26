# DeleteCommand {#doc_api_1030542 .reference}

Deletes a cloud assistant command.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=DeleteCommand) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|CommandId|String|Yes|c-4d34302d02424c5c8e10281e3a315a05| The ID of the command. You can call [DescribeCommands](~~64843~~) to view all available command IDs.

 |
|RegionId|String|Yes|cn-hangzhou| The ID of the region. You can call [DescribeRegions](~~25609~~) to view the latest regions of Alibaba Cloud.

 |
|Action|String|No|DeleteCommand| The operation that you want to perform. Set the value to DeleteCommand.

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=DeleteCommand
&CommandId=c-4d34302d02424c5c8e10281e3a315a05
&RegionId=cn-hangzhou 
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<DeleteCommandResponse>
  <RequestId>E69EF3CC-94CD-42E7-8926-F133B86387C0</RequestId>
</DeleteCommandResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"E69EF3CC-94CD-42E7-8926-F133B86387C0"
}
```

## Error codes {#section_13b_zeo_lj6 .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|500|InternalError.Dispatch|An error occurred when you dispatched the request.|The error message returned when an unknown error occurs.|
|403|InvalidRegionId.NotFound|Current region is not available.|The error message returned when the specified region is unavailable.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

