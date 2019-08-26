# DescribeTags {#doc_api_1006035 .reference}

Queries available tags. You can query the tags by specifying the ECS resource types, resource IDs, tag keys, or tag values. The system uses the Boolean operator AND \(&&\) between theses specified filtering conditions and returns a specific list of results from the operation.

## Description {#description .section}

When a tag key is specified and no tag value is specified, all tags related to the tag key are queried. When both the tag key and tag value are specified, tags that exactly match the key-value are queried.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=DescribeTags) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|RegionId|String|Yes|cn-hangzhou| The ID of the region. You can call [DescribeRegions](~~25609~~) to view the latest regions of Alibaba Cloud.

 |
|Action|String|No|DescribeTags| The operation that you want to perform. Set the value to DescribeTags.

 |
|PageNumber|Integer|No|1| The page number of the tag list. Starting value: 1.

 Default value: 1.

 |
|PageSize|Integer|No|50| The number of entries per page. Maximum value: 100.

 Default value: 50.

 |
|ResourceId|String|No|s-946ntx4wr| The ID of the resource to which the tag is bound. When the retrieved resources are instances, this parameter can be interpreted as InstanceId.

 |
|ResourceType|String|No|snapshot| The type of the resource. Valid values:

 -   disk
-   instance
-   image
-   securitygroup
-   snapshot

 All values must be lowercase.

 |
|Tag.N.Key|String|No|Finance| The tag key of the resource. Valid values of N: 1 to 20.

 |
|Tag.N.Value|String|No|Finance| The tag value of the resource. Valid values of N: 1 to 20.

 |
|Tag.N.key|String|No|Finance| The tag key of the resource.

 **Note:** This parameter will be removed in the future. We recommend that you use the Tag.N.Key parameter to ensure compatibility.

 |
|Tag.N.value|String|No|Finance| The tag value of the resource.

 **Note:** This parameter will be removed in the future. We recommend that you use the Tag.N.Value parameter to ensure compatibility.

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|PageNumber|Integer|1| The page number of the tag list.

 |
|PageSize|Integer|50| The number of entries per page.

 |
|RequestId|String|B04B8CF3-4489-432D-83BA-6F128E4F2295| The ID of the request.

 |
|Tags| | | The tags that match all the criteria.

 |
|└ResourceTypeCount| | | The number of resource types.

 |
|└Ddh|Integer|1| The number of dedicated hosts to which the tag is bound.

 |
|└Disk|Integer|15| The number of disks to which the tag is bound.

 |
|└Eni|Integer|5| The number of ENIs to which the tag is bound.

 |
|└Image|Integer|6| The number of images to which the tag is bound.

 |
|└Instance|Integer|45| The number of instances to which the tag is bound.

 |
|└KeyPair|Integer|17| The number of key pairs to which the tag is bound.

 |
|└LaunchTemplate|Integer|6| The number of launch templates to which the tag is bound.

 |
|└Securitygroup|Integer|4| The number of security groups to which the tag is bound.

 |
|└Snapshot|Integer|15| The number of snapshots to which the tag is bound.

 |
|└Volume|Integer|6| The number of extended volumes to which the tag is bound.

 |
|└TagKey|String|test| The key of the tag.

 |
|└TagValue|String|api| The value of the tag.

 |
|TotalCount|Integer|1| The total number of tags.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=DescribeTags
&RegionId=cn-hangzhou 
&PageSize=50 
&PageNumber=1 
&ResourceType=snapshot 
&ResourceId=s-946ntx4wr 
&Tag.1.Key=Finance
&Tag.1.Value=Finance
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<DescribeTagsResponse> 
  <RequestId>B04B8CF3-4489-432D-83BA-6F128E4F2295</RequestId>
  <PageNumber>1</PageNumber> 
  <PageSize>50</PageSize> 
  <Tags> 
    <Tag>
      <TagKey>test</TagKey> 
      <TagValue>api</TagValue> 
    </Tag>
  </Tags> 
  <TotalCount>1</TotalCount>
</DescribeTagsResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"Tags":{
		"Tag":[
			{
				"TagValue":"api",
				"TagKey":"test"
			}
		]
	},
	"PageNumber":1,
	"TotalCount":1,
	"PageSize":50,
	"RequestId":"B04B8CF3-4489-432D-83BA-6F128E4F2295"
}
```

## Error codes {#section_ggx_15e_5iz .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|404|InvalidRegionId.NotFound|The specified RegionId does not exist.|The error message returned when the specified Region ID does not exist. Check whether the service is available in this region.|
|404|InvalidResourceType.NotFound|The ResourceType provided does not exist in our records.|The error message returned when the specified resource does not exist.|
|400|InvalidTagCount|The specified tags are beyond the permitted range.|The error message returned when the specified tags are outside of the valid range.|
|400|InvalidTagKey.Malformed|The parameter Tag.n.Key is illegal.|The error message returned when the Tag.n.Key parameter is invalid.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

