# DescribeSnapshotsUsage {#doc_api_999637 .reference}

查询您在一个地域下的快照数量以及快照容量。如果您想知道当前地域下每块磁盘的快照使用情况，推荐使用 DescribeSnapshotLinks 查询磁盘快照链。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=DescribeSnapshotsUsage)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|RegionId|String|是|cn-hangzhou|快照所属的地域 ID。您可以调用 [DescribeRegions](~~25609~~) 查看最新的阿里云地域列表。

 |
|Action|String|否|DescribeSnapshotsUsage|系统规定参数。取值：DescribeSnapshotsUsage

 |
|OwnerAccount|String|否|ECSforCloud@Alibaba.com|RAM用户的账号登录名称。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。无论调用接口成功与否，我们都会返回请求 ID。

 |
|SnapshotCount|Integer|5|当前地域下的快照份数。

 |
|SnapshotSize|Long|122|当前地域下已产生的快照容量，单位 B。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

https://ecs.aliyuncs.com/?Action=DescribeSnapshotsUsage
&RegionId=cn-hangzhou
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeSnapshotsUsageResponse>
  <SnapshotCount>5</SnapshotCount>
  <SnapshotSize>122</SnapshotSize>
  <RequestId>ED5CF6DD-71CA-462C-9C94-A61A78A01479</RequestId>
</DescribeSnapshotsUsageResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"SnapshotSize":"122",
	"RequestId":"ACD9BBB0-A9D1-46D7-9630-B7A69889E110",
	"SnapshotCount":"5"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|403|InvalidParam.RegionId|The specified region is not exist.|指定的region不存在。|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Ecs)

