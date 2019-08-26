# DescribeSnapshotPackage {#doc_api_Ecs_DescribeSnapshotPackage .reference}

调用DescribeSnapshotPackage查询您在一个阿里云地域下已经购买的对象存储OSS存储包，存储包可以用于抵扣快照存储容量。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=DescribeSnapshotPackage&type=RPC&version=2014-05-26)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|RegionId|String|是|cn-hangzhou|快照所属的地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。

 |
|Action|String|否|DescribeSnapshotPackage|系统规定参数。取值：DescribeSnapshotPackage

 |
|PageNumber|Integer|否|1|OSS存储包列表的页码。起始值：1

 默认值：1

 |
|PageSize|Integer|否|10|分页查询时设置的每页行数。最大值：100

 默认值：10

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|PageNumber|Integer|1|OSS存储包列表的页码。

 |
|PageSize|Integer|10|分页查询时设置的每页行数。

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。

 |
|SnapshotPackages| | |存储包信息组成的集合。

 |
|DisplayName|String|FinanceJoshua|存储包名称。

 |
|EndTime|String|2018-11-30T06:32:31Z|存储包的过期时间。按照[ISO8601](~~25696~~)标准表示，并使用UTC +0时间，格式为yyyy-MM-ddTHH:mm:ssZ。

 |
|InitCapacity|Long|500|存储包的最大容量。

 |
|StartTime|String|2017-11-30T06:32:31Z|存储包的购买时间。按照[ISO8601](~~25696~~)标准表示，并使用UTC +0时间，格式为yyyy-MM-ddTHH:mm:ssZ。

 |
|TotalCount|Integer|1|返回的OSS存储包总数。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=DescribeSnapshotPackage
&RegionId=cn-hangzhou
&<公共请求参数>
```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeSnapshotPackageResponse>
	  <TotalCount>1</TotalCount>
	  <PageNumber>1</PageNumber>
	  <PageSize>5</PageSize>
	  <SnapshotPackages>
		    <SnapshotPackage>
			      <StartTime>2017-11-30T06:32:31Z</StartTime>
			      <EndTime>2018-11-30T06:32:31Z</EndTime>
			      <InitCapacity>500</InitCapacity>
			      <DisplayName>sp-snapshotpackage1</DisplayName>
		    </SnapshotPackage>
	  </SnapshotPackages>
	  <RequestId>ACD9BBB0-A9D1-46D7-9630-B7A69889E110</RequestId>
</DescribeSnapshotPackageResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"SnapshotPackages":{
		"SnapshotPackage":[
			{
				"InitCapacity":"500",
				"EndTime":"2018-11-30T06:32:31Z",
				"StartTime":"2017-11-30T06:32:31Z",
				"DisplayName":"sp-snapshotpackage1"
			}
		]
	},
	"PageNumber":"1",
	"TotalCount":"1",
	"PageSize":"5",
	"RequestId":"ACD9BBB0-A9D1-46D7-9630-B7A69889E110"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

