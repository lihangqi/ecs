# DescribeUserData {#doc_api_1161579 .reference}

Queries the user data of an ECS instance.

## Description {#description .section}

-   The returned user data is encoded in Base64.
-   If user data does not exist, a null value is returned.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=DescribeUserData) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|InstanceId|String|Yes|i-instanceid1| The ID of the instance.

 |
|RegionId|String|Yes|cn-hangzhou| The region ID of the instance. You can call the [DescribeRegions](~~25609~~) operation to view the latest region list.

 |
|Action|String|No|DescribeUserData| The operation that you want to perform. Set the value to DescribeUserdata.

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|InstanceId|String|i-instanceid1| The ID of the instance.

 |
|RegionId|String|cn-hangzhou| The region ID of the instance.

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The request ID.

 |
|UserData|String|ZWNobyBoZWxsbyBlY3Mh| The user data of the instance. It is encoded in Base64.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action= DescribeUserdata
&RegionId=cn-shenzhen
&InstanceId=i-instance1 
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<DescribeUserdataResponse>
  <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId> 
  <UserData>userdata1</UserData>
  <InstanceId> i-instance1</InstanceId>
  <RegionId> cn-shenzhen </RegionId>
</DescribeUserdataResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	" UserData ":" userdata1",
	"RequestId":"473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E",
	" InstanceId ":" i-instance1",
	" RegionId":"cn-shenzhen"
}
```

## Error codes { .section}

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

