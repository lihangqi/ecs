# DescribeInstanceTypeFamilies {#doc_api_1161577 .reference}

You can call this operation to query the instance type family list provided by ECS.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=DescribeInstanceTypeFamilies) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|RegionId|String|Yes|cn-hangzhou| The region ID of the instance. You can call the [DescribeRegions](~~25609~~) operation to view the latest region list.

 |
|Action|String|No|DescribeInstanceTypeFamilies| The operation that you want to perform. Set the value to **DescribeInstanceTypeFamilies**.

 |
|Generation|String|No|ecs-3| The generation of the instance type family. For more information, see [Instance type families](~~25378~~). Valid values:

 -   ecs-1: Generation I, which consists of the earliest and cost-effective instance types.
-   ecs-2: Generation II, which is available later than the first generation of instance type families.
-   ecs-3: Generation III, which consists of the quick-response and high-performance instance types.
-   ecs-4: Generation IV, which consists of the latest, low-latency, and wide-application instance types.

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|InstanceTypeFamilies| | | The returned instance type family information. It is an array that consists of **InstanceTypeFamilyItemType** data.

 |
|└Generation|String|ecs-1| The generation of the instance type family.

 |
|└InstanceTypeFamilyId|String|ecs.g5| The ID of the instance type family.

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The request ID.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=DescribeInstanceTypeFamilies
&RegionId=cn-hangzhou 
&Generation=ecs-3
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<DescribeInstanceTypeFamiliesResponse>
  <InstanceTypeFamilies>
    <InstanceTypeFamily>
      <InstanceTypeFamilyId>ecs.t1</InstanceTypeFamilyId>
      <Generation>ecs-1</Generation>
    </InstanceTypeFamily>
    <InstanceTypeFamily>
      <InstanceTypeFamilyId>ecs.s2</InstanceTypeFamilyId>
      <Generation>ecs-1</Generation>
    </InstanceTypeFamily>
    <InstanceTypeFamily>
      <InstanceTypeFamilyId>ecs.s3</InstanceTypeFamilyId>
      <Generation>ecs-1</Generation>
    </InstanceTypeFamily>
  </InstanceTypeFamilies>
  <RequestId>6B187E0A-C075-4D08-8B6F-6213950E8733</RequestId>
</DescribeInstanceTypeFamiliesResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"InstanceTypeFamilies":{
		"InstanceTypeFamily":[
			{
				"InstanceTypeFamilyId":"ecs.t1",
				"Generation":"ecs-1"
			},
			{
				"InstanceTypeFamilyId":"ecs.s2",
				"Generation":"ecs-1"
			},
			{
				"InstanceTypeFamilyId":"ecs.s3",
				"Generation":"ecs-1"
			}
		]
	},
	"RequestId":"6B187E0A-C075-4D08-8B6F-6213950E8733"
}
```

## Error codes { .section}

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

