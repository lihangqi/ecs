# ModifyImageAttribute {#doc_api_999579 .reference}

Modifies the name and description of a custom image.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=ModifyImageAttribute) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|ImageId|String|Yes|m-imageid1| The ID of the custom image.

 |
|RegionId|String|Yes|cn-hangzhou| The ID of the region to which the custom image belongs. You can call [DescribeRegions](~~25609~~) to view the latest regions of Alibaba Cloud.

 |
|Action|String|No|ModifyImageAttribute| The operation that you want to perform. Set the value to ModifyImageAttribute.

 |
|Description|String|No|FinanceDept| The description of the custom image.

 -   The description must be 0 to 256 characters in length.
-   It cannot start with http:// or https://.
-   If not specified, this parameter is null. Default value: null.

 |
|ImageName|String|No|FinanceJoshua| The name of the custom image.

 -   The name must be 2 to 128 characters in length.
-   It must start with a letter and can contain letters, digits, colons \(:\), underscores \(\_\), and hyphens \(-\).
-   It cannot start with http:// or https://.

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=ModifyImageAttribute
&ImageId=m-imageid1
&RegionId=cn-hangzhou 
&ImageName=FinanceJoshua
&Description=FinanceDept
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<ModifyImageAttributeResponse>
  <RequestId>C8B26B44-0189-443E-9816-D951F59623A9</RequestId>
</ModifyImageAttributeResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"C8B26B44-0189-443E-9816-D951F59623A9"
}
```

## Error codes {#section_4mf_j2s_w9r .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|400|MissingParameter|The input parameter RegionId that is mandatory for processing this request is not supplied.|The error message returned when the required RegionId parameter is not specified.|
|400|InvalidImageName.Duplicated|The specified Image name has already bean used.|The error message returned when the specified image name is already in use.|
|400|InvalidDescription.Malformed|The specified description is wrongly formed.|The error message returned when the specified description is invalid. The description must be 2 to 256 characters in length and cannot start with http:// or https://.|
|404|InvalidImageId.NotFound|The specified ImageId does not exist.|The error message returned when the specified image does not exist under this account. Check whether the image ID is correct.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

