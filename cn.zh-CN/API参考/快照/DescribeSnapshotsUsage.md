# DescribeSnapshotsUsage {#doc_api_Ecs_DescribeSnapshotsUsage .reference}

调用DescribeSnapshotsUsage查询您在一个地域下的快照数量以及快照容量。

如果您想知道当前地域下每块磁盘的快照使用情况，推荐使用[DescribeSnapshotLinks](~~55837~~)查询快照链。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=DescribeSnapshotsUsage&type=RPC&version=2014-05-26)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|RegionId|String|是|cn-hangzhou|快照所属的地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。

 |
|Action|String|否|DescribeSnapshotsUsage|系统规定参数。取值：DescribeSnapshotsUsage

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。

 |
|SnapshotCount|Integer|5|当前地域下的快照总数。

 |
|SnapshotSize|Long|122|当前地域下已产生的快照容量，单位Byte。

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

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

