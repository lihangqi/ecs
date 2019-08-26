# DescribeClassicLinkInstances {#doc_api_1030608 .reference}

Queries one or multiple classic network-connected instances that have established ClassicLink with VPCs.

## Description {#description .section}

When you call this operation, note that:

-   This API only supports classic network-connected instances.
-   You can query a maximum of 100 classic network-connected instances each time.
-   Either the VpcId parameter or the InstanceId parameter must be specified.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=DescribeClassicLinkInstances) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|RegionId|String|Yes|cn-hangzhou| The ID of the region where the instance resides. You can call [DescribeRegions](~~25609~~) to view the latest regions of Alibaba Cloud.

 |
|Action|String|No|DescribeClassicLinkInstances| The operation that you want to perform. Set the value to DescribeClassicLinkInstances.

 |
|InstanceId|String|No|i-test| The ID of the instance. You can specify a maximum of 100 instance IDs, which must be separated by commas \(,\).

 |
|PageNumber|String|No|1| The current page number. Starting value: 1.

 Default value: 1.

 |
|PageSize|String|No|10| The number of entries per page. Valid values: 1 to 100.

 Default value: 10.

 |
|VpcId|String|No|vpc-test| The ID of the VPC. The [ClassicLink](~~65413~~) service must be enabled for the specified VPC.

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|Links| | | The links between classic network-connected instances and VPCs.

 |
|└InstanceId|String|i-test| The ID of an instance.

 |
|└VpcId|String|vpc-test| The ID of a VPC.

 |
|PageNumber|Integer|1| The page number you query in the link list.

 |
|PageSize|Integer|10| The number of entries per page.

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the API request.

 |
|TotalCount|Integer|2| The total number of links.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=DescribeClassicLinkInstances
&RegionId=cn-hangzhou 
&VpcId=vpc-test
&InstanceId=i-test, i-test1
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<DescribeClassicLinkInstancesResponse>
  <RequestId>B154D309-F3E1-4AB7-BA94-FEFCA8B89001</RequestId>
  <TotalCount>2</TotalCount>
  <PageNumber>1</PageNumber>
  <PageSize>10</PageSize>
  <Links>
    <Link>
      <InstanceId>i-test</InstanceId>
      <VpcId>vpc-test</VpcId>
    </Link>
    <Link>
      <InstanceId>i-test1</InstanceId>
      <VpcId>vpc-test</VpcId>
    </Link>
  </Links>
</DescribeClassicLinkInstancesResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"PageNumber":1,
	"TotalCount":2,
	"Links":{
		"Link":[
			{
				"InstanceId":"i-test",
				"VpcId":"vpc-test"
			},
			{
				"InstanceId":"i-test1",
				"VpcId":"vpc-test"
			}
		]
	},
	"PageSize":10,
	"RequestId":"B154D309-F3E1-4AB7-BA94-FEFCA8B89001"
}
```

## Error codes {#section_3j2_ujd_r6k .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|403|InvalidInstanceId.NotBelong|The specified instance does not belong to you.|The error message returned when the specified instance does not exist under your account.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

