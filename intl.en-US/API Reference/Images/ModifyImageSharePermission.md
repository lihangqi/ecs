# ModifyImageSharePermission {#doc_api_1006139 .reference}

Manages which accounts a custom image is shared to. After you share a custom image to other Alibaba Cloud accounts, these accounts can use the shared image to create ECS instances \(RunInstances\) and replace system disks \(ReplaceSystemDisk\).

## Description {#description .section}

When you call this operation, note that:

-   You can share only your own custom images to other Alibaba Cloud accounts.
-   A single request can contain a maximum of 10 accounts to share a custom image to. You can specify a maximum of 10 values for the AddAccount.n or RemoveAccount.n parameter at a time. If you specify more than 10 values, the parameter will be ignored.
-   One image can be shared to a maximum of 50 Alibaba Cloud accounts. You can [submit a ticket](https://workorder-intl.console.aliyun.com/#/ticket/createIndex) to increase the number of users that you can share an image with.
-   If an instance is created \([RunInstances](~~63440~~)\) by using a shared image, after the image owner stops sharing or deletes the custom image \([DeleteImage](~~25537~~)\), the specified instance cannot be reinitialized \([ReInitDisk](~~25519~~)\).

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=ModifyImageSharePermission) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|ImageId|String|Yes|m-imageid1| The ID of the custom image to be shared.

 |
|RegionId|String|Yes|cn-hangzhou| The ID of the region to which the custom image belongs. You can call [DescribeRegions](~~25609~~) to view the latest regions of Alibaba Cloud.

 |
|Action|String|No|ModifyImageSharePermission| The operation that you want to perform. Set the value to ModifyImageSharePermission.

 |
|AddAccount.N|RepeatList|No|155780923771| The IDs of the Alibaba Cloud accounts to which the image is shared. Valid values of N: 1 to 10. If the value of N is greater than 10, this parameter will be ignored.

 |
|RemoveAccount.N|RepeatList|No|155780923772| The IDs of the Alibaba Cloud accounts to which the image is no longer to be shared. Valid values of N: 1 to 10. If the value of N is greater than 10, this parameter will be ignored.

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=ModifyImageSharePermission
&ImageId=m-imageid1
&RegionId=cn-hangzhou 
&AddAccount.1=155780923771
&RemoveAccount.1=155780923772
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<ModifyImageSharePermissionResponse>
  <RequestId>C8B26B44-0189-443E-9816-D951F59623A9</RequestId>
</ModifyImageSharePermissionResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"C8B26B44-0189-443E-9816-D951F59623A9"
}
```

## Error codes {#section_202_4qi_7yo .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|400|MissingParameter|The input parameter RegionId that is mandatory for processing this request is not supplied.|The error message returned when the required RegionId parameter is not specified.|
|404|InvalidImageId.NotFound|The specified ImageId does not exist.|The error message returned when the specified image does not exist under this account. Check whether the image ID is correct.|
|404|InvalidAccount.Forbidden|The specified Account does not yourself.|The error message returned when you are trying to share the image to your own account.|
|403|QuotaExceed.ShareImageUser|The shared Image user Quota exceeds.|The error message returned when the number of accounts to which one image can be shared has reached the upper limit.|
|400|InvalidGroup.Malformed|The specified Group is wrongly formed.|The error message returned when the specified group does not exist.|
|403|OperationDeined.EncryptedSnapshot|The image contains encrypted snapshots, which do not support share.|The error message returned when the specified image contains encrypted snapshots.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

