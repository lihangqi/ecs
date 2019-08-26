# DescribeSnapshotPackage {#DescribeSnapshotPackage .reference}

查询您在一个阿里云地域下已经购买了用于可以抵扣快照存储容量的对象存储OSS（存储包）。

## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：DescribeSnapshotPackage|
|RegionId|String|是|快照所属的地域 ID。您可以调用[DescribeRegions](../intl.zh-CN/API 参考/地域/DescribeRegions.md#)查看最新的阿里云地域列表。|
|PageNumber|Integer|否|OSS 存储包列表的页码。起始值：1默认值：1

|
|PageSize|Integer|否|分页查询时设置的每页行数。最大值：100默认值：10

|

## 返回参数 {#ResponseParameter .section}

|名称|类型|描述|
|:-|:-|:-|
|TotalCount|Integer|返回的 OSS 存储包总数。|
|PageNumber|Integer|OSS 存储包列表的页码。|
|PageSize|Integer|分页查询时设置的每页行数。|
|SnapshotPackages|Array of [SnapshotPackage](#)|存储包信息组成的集合。|

|名称|类型|描述|
|:-|:-|:-|
|StartTime|String|存储包的购买时间。按照[ISO8601](../intl.zh-CN/API 参考/附录/时间格式.md#)标准表示，并需要使用UTC时间，格式为yyyy-MM-ddTHH:mm:ssZ。|
|EndTime|String|存储包的过期时间。按照[ISO8601](../intl.zh-CN/API 参考/附录/时间格式.md#)标准表示，并需要使用UTC时间，格式为yyyy-MM-ddTHH:mm:ssZ。|
|InitCapacity|Long|存储包的最大容量。|
|DisplayName|String|存储包名称。|

## 示例 {#Samples .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=DescribeSnapshotPackage
&RegionId=cn-hangzhou
&<公共请求参数>
```

**返回示例**

**XML 格式**

```
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

**JSON 格式**

```
{
	"TotalCount": "1",
	"PageNumber": "1",
	"PageSize": "5",
	"SnapshotPackages": {
		"SnapshotPackage": [
			"StartTime": "2017-11-30T06:32:31Z",
			"EndTime": "2018-11-30T06:32:31Z",
			"InitCapacity": "500",
			"DisplayName": "sp-snapshotpackage1"
		]
	},
	"RequestId": "ACD9BBB0-A9D1-46D7-9630-B7A69889E110"
}
```

## 错误码 {#ErrorCode .section}

全是公共错误码。更多错误码，请访问[API错误中心](https://error-center.alibabacloud.com/status/product/Ecs)。

