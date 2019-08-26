# RemoveTags {#doc_api_1023333 .reference}

Unbinds one or more tags from instances, disks, snapshots, images, or security groups.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=RemoveTags) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|RegionId|String|Yes|cn-shenzhen| The ID of the region to which the ECS resource belongs. You can call [DescribeRegions](~~25609~~) to view the latest regions of Alibaba Cloud.

 |
|ResourceId|String|Yes|s-946ntx4wr| The ID of the resource from which you want to unbind the tags. When the retrieved resources are instances, this parameter can be interpreted as InstanceId.

 |
|ResourceType|String|Yes|snapshot| The type of the resource. Valid values:

 -   disk
-   instance
-   image
-   securitygroup
-   snapshot

 All values must be lowercase.

 |
|Action|String|No|RemoveTags| The operation that you want to perform. Set the value to RemoveTags.

 |
|Tag.N.Key|String|No|Finance| The tag key of the resource. Valid values of N: 1 to 20.

 |
|Tag.N.Value|String|No|FinanceJoshua| The tag value of the resource. Valid values of N: 1 to 20.

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
https://ecs.aliyuncs.com/?Action=RemoveTags
&RegionId=cn-shenzhen
&ResourceId=s-946ntx4wr 
&ResourceType=snapshot 
&Tag.1.Key=Finance
&Tag.1.Value=FinanceJoshua
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<RemoveTagsResponse>
  <RequestId>6A2C8AB5-E15D-478C-B56A-CF3DAF060028</RequestId>
</RemoveTagsResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"6A2C8AB5-E15D-478C-B56A-CF3DAF060028"
}
```

## Error codes {#section_f85_p7b_uqt .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|404|InvalidRegionId.NotFound|The specified RegionId does not exist.|The error message returned when the specified Region ID does not exist. Check whether the service is available in this region.|
|404|InvalidResourceType.NotFound|The ResourceType provided does not exist in our records.|The error message returned when the specified resource type does not exist.|
|400|InvalidTagCount|The specified tags are beyond the permitted range.|The error message returned when the specified tags are outside of the valid range.|
|400|InvalidResourceType.NotFound|The specified ResourceType does not exist.|The error message returned when the ResourceType parameter is invalid.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

