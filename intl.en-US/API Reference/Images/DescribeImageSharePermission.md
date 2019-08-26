# DescribeImageSharePermission {#doc_api_1091446 .reference}

Queries the accounts to which a custom image is shared. The response can be displayed over several pages. Ten entries are displayed on each page by default.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=DescribeImageSharePermission) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|ImageId|String|Yes|m-imageid1| The ID of the custom image.

 |
|RegionId|String|Yes|cn-hangzhou| The ID of the region to which the custom image belongs. You can call [DescribeRegions](~~25609~~) to view the latest regions of Alibaba Cloud.

 |
|Action|String|No|DescribeImageSharePermission| The operation that you want to perform. Set the value to DescribeImageSharePermission.

 |
|PageNumber|Integer|No|1| The page number that you query in the account list. Starting value: 1. Default value: 1.

 |
|PageSize|Integer|No|10| The number of entries on each page. Maximum value: 50. Default value: 10.

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|Accounts| | | The type of an Alibaba Cloud account.

 |
|└AliyunId|String|155780923770| The ID of an Alibaba Cloud account.

 |
|ImageId|String|m-imageid2| The ID of the custom image.

 |
|PageNumber|Integer|1| The page number that you query in the account list.

 |
|PageSize|Integer|10| The number of entries on each page.

 |
|RegionId|String|cn-hangzhou| The ID of the region to which the image belongs.

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request. This parameter is returned regardless of whether the operation is successful.

 |
|ShareGroups| | | The type of the shared group.

 |
|└Group|String|all| The shared group.

 |
|TotalCount|Integer|1| The total number of entries.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=DescribeImageSharePermission
&ImageId=m-imageid1
&RegionId=cn-hangzhou 
&PageNumber=1 
&PageSize=10 
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<DescribeImageSharePermissionResponse>
  <ImageId>m-282dzntc7</ImageId>
  <PageNumber>1</PageNumber> 
  <PageSize>10</PageSize> 
  <RegionId>cn-qingdao</RegionId> 
  <TotalCount>1</TotalCount> 
  <RequestId>441CF898-42FF-47CF-9348-3C3BFF557278</RequestId>
  <ShareGroups>
    <ShareGroup>
      <Group>all</Group>
    </ShareGroup>
  </ShareGroups>
  <Accounts> 
    <Account> 
      <AliyunId>155780923770</AliyunId>
    </Account>
  </Accounts> 
</DescribeImageSharePermissionResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"Accounts":{
		"Account":[
			{
				"AliyunId":"155780923770"
			}
		]
	},
	"PageNumber":1,
	"ImageId":"m-282dzntc7",
	"TotalCount":1,
	"PageSize":10,
	"RequestId":"9AD96F49-0BE5-4868-A66A-224352549CEC",
	"RegionId":"cn-qingdao",
	"ShareGroups":{
		"ShareGroup":[
			{
				"Group":"all"
			}
		]
	}
}
```

## Error codes {#section_hcf_igj_rmw .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|400|MissingParameter|The input parameter RegionId that is mandatory for processing this request is not supplied.|The error message returned when the required RegionId parameter is not specified.|
|400|MissingParameter|The input parameter ImageId that is mandatory for processing this request is not supplied.|The error message returned when the required ImageId parameter is not specified.|
|404|InvalidImageId.NotFound|The specified image does not exist.|The error message returned when the specified image does not exist under this account. Check whether the image ID is correct.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

