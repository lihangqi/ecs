# AddTags {#doc_api_1023339 .reference}

Adds or overwrites one or more tags on your ECS resource. You can add tags to ECS resources such as instances, disks, snapshots, images, and security groups to manage resources easier.

## Description {#description .section}

When you call this operation, note that:

-   Up to 20 tags can be added to each ECS resource.
-   The tag key \(`Tag.n.Key`\) must match the tag value \(`Tag.n.Value`\).
-   If the tag key \(`Tag.n.Key`\) already exists on the specified resource, the new tag value \(`Tag.n.Value`\) automatically overwrites the old one.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=AddTags) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|RegionId|String|Yes|cn-hangzhou| The ID of the region to which the ECS resource belongs. You can call [DescribeRegions](~~25609~~) to view the latest regions of Alibaba Cloud.

 |
|ResourceId|String|Yes|i-instanceid1| The ID of the resource to which you want to bind the tags. When the resources are instances, this parameter can be interpreted as InstanceId.

 |
|ResourceType|String|Yes|instance| The type of the resource. Valid values:

 -   disk
-   instance
-   image
-   securitygroup
-   snapshot

 All values must be lowercase.

 |
|Action|String|No|AddTags| The operation that you want to perform. Set the value to AddTags.

 |
|Tag.N.Key|String|No|Finance| The tag key of the resource. Valid values of N: 1 to 20. It cannot be a null string. It can be a maximum of 64 characters in length. It cannot start with aliyun, acs:, http://, or https://.

 |
|Tag.N.Value|String|No|FinanceJoshua| The tag value of the resource. Valid values of N: 1 to 20. It can be a null string. It can be a maximum of 128 characters in length. It cannot start with aliyun or acs:. It cannot contain http:// or https://.

 |
|Tag.N.key|String|No|Finance| The tag key of the resource.

 **Note:** This parameter will be removed in the future. We recommend that you use the Tag.N.Key parameter to ensure compatibility.

 |
|Tag.N.value|String|No|FinanceJoshua| The tag value of the resource.

 **Note:** This parameter will be removed in the future. We recommend that you use the Tag.N.Value parameter to ensure compatibility.

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=AddTags
&RegionId=cn-hangzhou 
&ResourceId=i-instanceid1
&ResourceType=instance
&Tag.1.Key=Finance
&Tag.1.Value=FinanceJoshua
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<AddTagsResponse> 
  <RequestId>C46FF5A8-C5F0-4024-8262-B16B639225A0</RequestId>
</AddTagsResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"C46FF5A8-C5F0-4024-8262-B16B639225A0"
}
```

## Error codes {#section_her_l8w_rdi .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|404|InvalidRegionId.NotFound|The specified RegionId does not exist.|The error message returned when the specified Region ID does not exist. Check whether the service is available in this region.|
|404|InvalidResourceType.NotFound|The ResourceType provided does not exist in our records.|The error message returned when the specified resource type does not exist.|
|400|InvalidTag.Mismatch|The specified Tag.n.Key and Tag.n.Value are not match.|The error message returned when the specified tag key does not match the tag value.|
|400|InvalidTagCount|The specified tags are beyond the permitted range.|The error message returned when the specified tags are outside of the valid range.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

