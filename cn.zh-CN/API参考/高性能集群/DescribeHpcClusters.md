# DescribeHpcClusters {#doc_api_Ecs_DescribeHpcClusters .reference}

调用DescribeHpcClusters查询您可用的HPC集群。请求参数作为筛选器（Filter）使用，筛选关系为逻辑与（&&）关系，参数之间无依赖关系。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=DescribeHpcClusters)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|RegionId|String|是|cn-hangzhou|地域 ID。您可以调用 [DescribeRegions](~~25609~~) 查看最新的阿里云地域列表。

 |
|Action|String|否|DescribeHpcClusters|系统规定参数。取值：DescribeHpcClusters

 |
|ClientToken|String|否|123e4567-e89b-12d3-a456-426655440000|保证请求幂等性。从您的客户端生成一个参数值，确保不同请求间该参数值唯一。**ClientToken**只支持ASCII字符，且不能超过64个字符。更多详情，请参见[如何保证幂等性](~~25693~~)。

 |
|HpcClusterIds|String|否|\["hpc-xxxxxxxxx", "hpc-yyyyyyyyy", … "hpc-zzzzzzzzz"\]|HPC 集群 ID。

 取值可以由多个 HPC 集群 ID 组成一个 JSON 数组，最多支持 100 个 ID，ID 之间用半角逗号（,）隔开。

 |
|PageNumber|Integer|否|1|HPC 集群列表的页码。

 起始值：1

 默认值：1

 |
|PageSize|Integer|否|10|分页查询时设置的每页行数。

 最大值：100

 默认值：10

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|HpcClusters| | |由 HpcCluster 组成的数组格式，返回 HPC 集群的信息

 |
|Description|String|FinanceDept|HPC 集群的描述

 |
|HpcClusterId|String|hpc-hpclusterid1|HPC 集群 ID

 |
|Name|String|FinanceJoshua|HPC 集群的名字

 |
|PageNumber|Integer|1|HPC 集群列表的页码

 |
|PageSize|Integer|10|输入时设置的每页行数

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID

 |
|TotalCount|Integer|2|HPC 集群总个数

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=DescribeHpcClusters
&RegionId=cn-hangzhou
&<公共请求参数>
```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeHpcClustersResponse>
  <PageNumber>1</PageNumber>
  <TotalCount>2</TotalCount>
  <HpcClusters>
    <HpcCluster>
      <Name>chuatest1</Name>
      <Description>desc</Description>
      <HpcClusterId>hpc-l6ack54lcr2g17563***</HpcClusterId>
    </HpcCluster>
    <HpcCluster>
      <Name>chuatest2</Name>
      <Description>desc</Description>
      <HpcClusterId>hpc-l6aam7fivcfd21fun***</HpcClusterId>
    </HpcCluster>
  </HpcClusters>
  <PageSize>10</PageSize>
  <RequestId>168D82CE-F8A0-4200-AC5C-26FD94438423</RequestId>
</DescribeHpcClustersResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"PageNumber":1,
	"TotalCount":2,
	"PageSize":10,
	"HpcClusters":{
		"HpcCluster":[
			{
				"Name":"chuatest1",
				"Description":"desc",
				"HpcClusterId":"hpc-l6ack54lcr2g17563***"
			},
			{
				"Name":"chuatest2",
				"Description":"desc",
				"HpcClusterId":"hpc-l6aam7fivcfd21fun***"
			}
		]
	},
	"RequestId":"382960A6-C535-4705-B6EA-8338466270C4"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InvalidRegionId.NotFound|The specified parameter "RegionId" is not valid.|指定的 RegionId 不存在，请您检查此产品在该地域是否可用。|
|400|MissingParameter.HpcClusterId|The input parameter HpcClusterId that is mandatory for processing this request is not supplied.|缺少必填参数hpcClusterId。|
|400|InvalidHpcClusterIds.ExceedLimit|The amount of specified specified hpc cluster ids exceeds the limit.|批量查询的hpcClusterId数量超出记录。|
|400|InvalidHpcClusterIds.Malformed|The amount of specified specified hpc cluster ids is invalid.|批量查询的hpcClusterIds参数不合法。|
|400|Invalid.Parameter|Invalid parameters.|参数不合法。|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

