# TagResources {#doc_api_1057764 .reference}

Creates and attaches tags to a list of specified ECS resources.

## Limits {#description .section}

Each Alibaba Cloud account has a quota of tags that can be used. If the quota is exceeded, an error message is returned. For more information, see [Limits](~~25412~~).

## Debug {#apiExplorer .section}

Go to [API Explorer](https://api.aliyun.com/#product=Ecs&api=TagResources) for online debugging. By using API Explorer, you can easily debug APIs, automatically generate SDK code examples, and quickly search for APIs.

## Request parameters {#parameters .section}

|Parameter|Type|Required?|Example value|Description|
|---------|----|---------|-------------|-----------|
|Action|String|No|TagResources| The name of this action. Value: TagResources.

 |
|RegionId|String|Yes|cn-hangzhou| The ID of the region to which the ECS resource belongs. For more information, call [DescribeRegions](~~25609~~) to obtain the latest region list.

 |
|ResourceId.N|RepeatList|Yes|i-bp1j6qtvdm8w0z1o0XXX| The ID of the ECS resource. Value range of N: 1 to 50.

 |
|ResourceType|String|Yes|ECS\_INSTANCE\("ALIYUN::ECS::INSTANCE"\)| The type of the ECS resource. Optional values:

 -   instance
-   disk
-   snapshot
-   image
-   securitygroup
-   volume
-   eni
-   ddh
-   keypair
-   launchtemplate

 |
|OwnerAccount|String|No|ECSforCloud@Alibaba.com| The logon account of the RAM user.

 |
|Tag.N.Key|String|No|FinanceDept| The value of a tag. Value range of N: 1 to 20. The parameter cannot be a null string. The parameter must be 1 to 64 characters in length, and cannot start with aliyun, acs:, http://, or https://.

 |
|Tag.N.Value|String|No|FinanceJoshua| The value of a tag. Value range of N: 1 to 20. The parameter can be a null string. The parameter must be 1 to 128 characters in length, and cannot start with aliyun, acs:, http://, or https://.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example value|Description|
|---------|----|-------------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The request ID.

 |

## Examples {#demo .section}

Request example

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=TagResources
&RegionId=cn-hangzhou
&ResourceId.1=i-bp1j6qtvdm8w0z1o0XXX
&ResourceType=instance
&Tag.1.Key=FinanceDept
&<Common Request Parameters>            
```

Response example

`XML` format

``` {#xml_return_success_demo}
<TagResourcesResponse>
  <RequestId>C46FF5A8-C5F0-4024-8262-B16B639225A0</RequestId>
</TagResourcesResponse>            
```

`JSON` format

``` {#json_return_success_demo}
{
    "RequestId":"C46FF5A8-C5F0-4024-8262-B16B639225A0"
}
```

## Errors { .section}

|HTTP status code|Error codes|Error message|Description|
|----------------|-----------|-------------|-----------|
|404|MissingParameter.TagOwnerUid|The parameter - TagOwnerUid should not be null|The specified tag owner UID does not exist.|
|404|MissingParameter.TagOwnerBid|The parameter - TagOwnerBid should not be null|The specified tag owner BID does not exist.|
|404|MissingParameter.Tags|The parameter - Tags should not be null|The Tags parameter does not exist.|
|404|MissingParameter.RegionId|The parameter - RegionId should not be null|The specified region ID does not exist.|
|403|PermissionDenied.TagOwnerUid|The specified operator not have permission to set TagOwnerUid value.|You do not have permission to set the tag owner.|
|403|PermissionDenied.Scope|The specified operator not have permission to set Scope value.|You do not have permission to modify the scope value.|
|400|NumberExceed.ResourceIds|The ResourceIds parameter's number is exceed , Valid : 50|The number of resource IDs cannot exceed 50.|
|400|NumberExceed.Tags|The Tags parameter's number is exceed , Valid : 20|The number of tags cannot exceed 20.|
|400|Duplicate.TagKey|The Tag.N.Key contain duplicate key.|The tag key contains duplicate keys.|
|404|InvalidResourceId.NotFound|The specified ResourceIds are not found in our records.|The specified resource does not exist.|
|404|InvalidResourceType.NotFound|The ResourceType provided does not exist in our records.|The specified resource type does not exist.|
|400|InvalidTagValue.Malformed|The specified Tag.n.Value is not valid.|The specified tag value is invalid.|
|404|InvalidRegionId.NotFound|The specified RegionId does not exist.|The specified region ID does not exist. Please check if this product is available in this region.|
|400|Invalid.Scope|The specified scope is invalid.|The specified scope is invalid.|
|403|NoPermission.Tag|The operator is not permission for the tag.|You do not have permission to use this resource tag.|

For a list of error codes, visit the [API Error Center](https://error-center.aliyun.com/status/product/Ecs).

