# DescribeSnapshotPackage {#doc_api_1006029 .reference}

查询您在一个阿里云地域下已经购买了用于可以抵扣快照存储容量的对象存储OSS（存储包）。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=DescribeSnapshotPackage)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|RegionId|String|是|cn-hangzhou|快照所属的地域 ID。您可以调用 [DescribeRegions](~~25609~~) 查看最新的阿里云地域列表。

 |
|Action|String|否|DescribeSnapshotPackage|系统规定参数。取值：DescribeSnapshotPackage

 |
|OwnerAccount|String|否|ECSforCloud@Alibaba.com|RAM用户的账号登录名称。

 |
|PageNumber|Integer|否|1|OSS 存储包列表的页码。起始值：1

 默认值：1

 |
|PageSize|Integer|否|10|分页查询时设置的每页行数。最大值：100

 默认值：10

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|PageNumber|Integer|1|OSS 存储包列表的页码。

 |
|PageSize|Integer|10|分页查询时设置的每页行数。

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。无论调用接口成功与否，我们都会返回请求 ID。

 |
|SnapshotPackages| | |存储包信息组成的集合。

 |
|└DisplayName|String|FinanceJoshua|存储包名称。

 |
|└EndTime|String|2018-11-30T06:32:31Z|存储包的过期时间。按照 [ISO8601](~~25696~~) 标准表示，并需要使用UTC时间，格式为yyyy-MM-ddTHH:mm:ssZ。

 |
|└InitCapacity|Long|500|存储包的最大容量。

 |
|└StartTime|String|2017-11-30T06:32:31Z|存储包的购买时间。按照 [ISO8601](~~25696~~) 标准表示，并需要使用UTC时间，格式为yyyy-MM-ddTHH:mm:ssZ。

 |
|TotalCount|Integer|1|返回的 OSS 存储包总数。

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

[查看本产品错误码](https://error-center.aliyun.com/status/product/Ecs)

