# ListTagResources {#doc_api_Ecs_ListTagResources .reference}

Queries a list of tags that are attached to one or more ECS resources.

## Description {#description .section}

-   To determine the search object, a request should include the parameter `ResourceId.N` or `Tag.N` \(that is, `Tag.N.Key` and `Tag.N.Value`\).
-   `Tag.N` is a resource tag and consists of a key-value pair. When only `Tag.N.Key` is specified, all tag values associated with the tag key are returned. When only `Tag.N.Value` is specified, the error `InvalidParameter.TagValue` is reported.
-   If you specify `Tag.N` and `Resource.N` simultaneously,`ResourceId.N` must match all the tag key-value inputs.
-   If you specify multiple tag key-value pairs at the same time, the returned results are the resources that contain the specified multiple key-value pairs.

## Debug {#apiExplorer .section}

By using API Explorer, you can easily debug APIs, automatically generate SDK code examples, and quickly search for APIs.

## Request parameters {#parameters .section}

|Parameter|Type|Required?|Example value|Description|
|---------|----|---------|-------------|-----------|
|RegionId|String|Yes|cn-hangzhou| The ID of the region to which the ECS resource belongs. For more information, call [DescribeRegions](https://www.alibabacloud.com/help/doc-detail/25609.htm) to obtain the latest region list.

 |
|ResourceType|String|Yes|instance| The type of the ECS resource. Valid values:

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
|Action|String|No|ListTagResources| The name of this action. Value: ListTagResources.

 |
|NextToken|String|No|caeba0bbb2be03f84eb48b699f0a4883| The token for the next query.

 |
|ResourceId.N|RepeatList|No|i-instanceid1| The ID of the ECS resource. Value range of N: 1 to 50.

 |
|Tag.N.Key|String|No|FinanceDept| The value of a tag. Value range of N: 1 to 20. The parameter cannot be a null string. The parameter must be 1 to 64 characters in length. It can neither start with aliyun or acs:, nor contain http:// or https://.

 |
|Tag.N.Value|String|No|FinanceJoshua| The value of a tag. Value range of N: 1 to 20. The parameter can be a null string. The parameter must be 1 to 128 characters in length. It can neither start with aliyun or acs:, nor contain http://, or https://.

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example value|Description|
|---------|----|-------------|-----------|
|NextToken|String|caeba0bbb2be03f84eb48b699f0a4883| The token for the next query.

 |
|RequestId|String|DE65F6B7-7566-4802-9007-96F2494AC5XX| The request ID.

 |
|TagResources| | | A collection of resources and their tags that contain information such as resource IDs, resource types, and tag keys.

 |
|└ResourceId|String|i-bp1j6qtvdm8w0z1o0XXX| The resource ID.

 |
|└ResourceType|String|instance| The resource type.

 |
|└TagKey|String|FinanceDept| The tag key.

 |
|└TagValue|String|FinanceJoshua| The tag value.

 |

## Examples {#demo .section}

Request example

``` {#request_demo}

https://ecs.aliyuncs.com/?Action=ListTagResources
&RegionId=cn-hangzhou
&ResourceType=instance
&ResourceId.1=i-bp1j6qtvdm8w0z1o0XXX
&<Common Request Parameters>

```

Response example

`XML` format

``` {#xml_return_success_demo}
<ListTagResourcesResponse>
  <TagResources>
    <TagResource>
      <ResourceType>instance</ResourceType>
      <TagValue>FinanceJoshua</TagValue>
      <ResourceId>i-bp1j6qtvdm8w0z1o0XXX</ResourceId>
      <TagKey>FinanceDept</TagKey>
    </TagResource>
  </TagResources>
  <RequestId>DE65F6B7-7566-4802-9007-96F2494AC5XX</RequestId>
</ListTagResourcesResponse>

```

`JSON` format

``` {#json_return_success_demo}
{
	"TagResources":{
		"TagResource":[
			{
				"ResourceType":"instance",
				"TagValue":"FinanceJoshua",
				"ResourceId":"i-bp1j6qtvdm8w0z1o0XXX",
				"TagKey":"FinanceDept"
			}
		]
	},
	"RequestId":"DE65F6B7-7566-4802-9007-96F2494AC512"
}
```

## Errors {#section_140_ios_32z .section}

|HTTP status code|Error codes|Error message|Description|
|----------------|-----------|-------------|-----------|
|404|MissingParameter.TagOwnerUid|The parameter - TagOwnerUid should not be null|The tag owner UID is not specified.|
|404|MissingParameter.TagOwnerBid|The parameter - TagOwnerBid should not be null|The tag owner BID is not specified.|
|404|MissingParameter.ResourceType|The parameter - ResourceType should not be null|The resource type is not specified.|
|404|MissingParameter.Tags|The parameter - Tags should not be null|The tag is not specified.|
|404|MissingParameter.RegionId|The parameter - RegionId should not be null|The region ID is not specified.|
|403|PermissionDenied.TagOwnerUid|The specified operator not have permission to set TagOwnerUid value.|You do not have permission to set the tag owner.|
|403|PermissionDenied.Scope|The specified operator not have permission to set Scope value.|You do not have permission to modify the scope value.|
|400|NumberExceed.ResourceIds|The ResourceIds parameter's number is exceed , Valid : 50|The number of resource IDs cannot exceed 50.|
|400|NumberExceed.Tags|The Tags parameter's number is exceed , Valid : 20|The number of tags cannot exceed 20.|
|400|Duplicate.TagKey|The Tag.N.Key contain duplicate key.|Duplicate tag keys exist.|
|404|InvalidResourceId.NotFound|The specified ResourceIds are not found in our records.|The specified resource does not exist.|
|404|InvalidResourceType.NotFound|The ResourceType provided does not exist in our records.|The specified resource type does not exist.|
|400|InvalidTagKey.Malformed|The specified Tag.n.Key is not valid.|The specified tag key is invalid.|
|400|InvalidTagValue.Malformed|The specified Tag.n.Value is not valid.|The specified tag value is invalid.|
|400|OperationDenied.QuotaExceed|The quota of tags on resource is beyond permitted range.|The quota of resource tags is reached.|
|403|InvalidResourceId.NotSupported|The specified ResourceId does not support tagging.|Tags are not supported by the specified resource ID.|
|400|InvalidTag.Mismatch|The specified Tag.n.Key and Tag.n.Value are not match.|The specified Tag.n.Key and Tag.n.Value do not match.|
|400|InvalidTagCount|The specified tags are beyond the permitted range.|The specified number of tags exceeds the quota.|
|404|InvalidRegionId.NotFound|The specified RegionId does not exist.|The specified region ID does not exist. Please check if this product is available in this region.|
|400|Invalid.Scope|The specified scope is invalid.|The specified scope is invalid.|
|403|NoPermission.Tag|The operator is not permission for the tag.|You do not have permission to use this resource tag.|

For a list of error codes, visit the [API Error Center](https://error-center.aliyun.com/status/product/Ecs).

