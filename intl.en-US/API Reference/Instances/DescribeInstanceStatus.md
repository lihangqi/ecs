# DescribeInstanceStatus {#doc_api_1161574 .reference}

Obtains the states of multiple instances.

## Description {#description .section}

-   The states of all instances are returned. For more information, see [Instance states](~~25687~~)。
-   You can also call this operation to obtain the instance list.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=DescribeInstanceStatus) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|RegionId|String|Yes|cn-hangzhou| The region ID of the instance. You can call the [DescribeRegions](~~25609~~) operation to view the latest region list.

 |
|Action|String|No|DescribeInstanceStatus| The operation that you want to perform. Set the value to DescribeInstanceStatus.

 |
|ClusterId|String|No|cls-clusterid1| The ID of the cluster to which the instance belongs.

 **Note:** This parameter will be removed in the future. We recommend that you use other parameters to ensure compatibility.

 |
|PageNumber|Integer|No|1| The page number. This value starts from 1.

 Default value: 1.

 |
|PageSize|Integer|No|10| The number of rows per page. Valid values: 1 to 50.

 Default value: 10

 |
|ZoneId|String|No|cn-hangzhou-d| The zone ID of the instance.

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|InstanceStatuses| | | The returned instance state information. It is an array that consists of InstanceStatusSetType data.

 |
|└InstanceId|String|i-instance1| The ID of the instance.

 |
|└Status|String|Running| The state of the instance.

 |
|PageNumber|Integer|1| The page number.

 |
|PageSize|Integer|10| The number of rows per page.

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The request ID.

 |
|TotalCount|Integer|2| The total number of instances.

 |

## Examples {#demo .section}

Sample request

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=DescribeInstanceStatus
&RegionId=cn-hangzhou 
&ZoneId=cn-hangzhou-d
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<DescribeInstanceStatusResponse>
  <RequestId>6EF60BEC-0242-43AF-BB20-270359FB54A7</RequestId> 
  <TotalCount>2</TotalCount> 
  <PageNumber>1</PageNumber> 
  <PageSize>10</PageSize> 
  <InstanceStatuses>
    <InstanceStatus>
      <InstanceId>i-instance1</InstanceId>
      <Status>Running</Status>
    </InstanceStatus>
    <InstanceStatus>
      <InstanceId>i-ae4r89pp</InstanceId>
      <Status>Stopped</Status>
    </InstanceStatus>
  </InstanceStatuses>
</DescribeInstanceStatusResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"PageNumber":1,
	"InstanceStatuses":{
		"InstanceStatus":[
			{
				"Status":"Running",
				"InstanceId":"i-instance1"
			},
			{
				"Status":"Stopped",
				"InstanceId":"i-ae4r89pp"
			}
		]
	},
	"TotalCount":2,
	"PageSize":10,
	"RequestId":"6EF60BEC-0242-43AF-BB20-270359FB54A7"
}
```

## Error codes { .section}

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

