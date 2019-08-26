# DescribeDeploymentSets {#doc_api_1006118 .reference}

查询一个或多个部署集的属性列表。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=DescribeDeploymentSets)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|RegionId|String|是|cn-hangzhou|部署集所属地域ID。您可以调用 [DescribeRegions](~~25609~~) 查看最新的阿里云地域列表。

 |
|Action|String|否|DescribeDeploymentSets|系统规定参数。取值：DescribeDeploymentSets

 |
|DeploymentSetIds|String|否|\["ds-xxxxxxxxx", "ds-yyyyyyyyy", … "ds-zzzzzzzzz"\]|部署集ID列表。取值可以由多个部署集ID组成一个JSON数组，最多支持100个ID，ID之间用半角逗号（,）隔开。

 |
|DeploymentSetName|String|否|FinanceJoshua|部署集名称。

 |
|Domain|String|否|Default|部署域。

 **说明：** 该参数即将被弃用，为提高兼容性，请尽量使用其他参数。

 |
|Granularity|String|否|Host|部署粒度。

 **说明：** 该参数即将被弃用，为提高兼容性，请尽量使用其他参数。

 |
|NetworkType|String|否|vpc|部署集内的网络类型。

 **说明：** 该参数即将被弃用，为提高兼容性，请尽量使用其他参数。

 |
|OwnerAccount|String|否|ECSforCloud@Alibaba.com|RAM用户的账号登录名称。

 |
|PageNumber|Integer|否|1|部署集列表的页码。起始值：1

 默认值：1

 |
|PageSize|Integer|否|10|分页查询时设置的每页行数，最大值：100

 默认值：10

 |
|Strategy|String|否|Availability|部署策略。取值：Availability

 默认值：空。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|DeploymentSets| | |由DeploymentSet组成的数组格式，返回部署集详细信息。

 |
|└CreationTime|String|2017-12-05T22:40:00Z|部署集的创建时间。

 |
|└DeploymentSetDescription|String|FinanceDeptHighAvailability|部署集的描述信息。

 |
|└DeploymentSetId|String|ds-deploymentsetid1|部署集ID。

 |
|└DeploymentSetName|String|FinanceJoshua|部署集名称。

 |
|└DeploymentStrategy|String|Availability|部署策略。

 |
|└Domain|String|Default|部署域。

 |
|└Granularity|String|Host|部署粒度。

 |
|└InstanceAmount|Integer|1|部署集内的实例数量。

 |
|└InstanceIds| |\["i-instanceid1"\]|部署集内的实例ID列表。

 |
|└Strategy|String|StrictDispersion|部署策略。

 |
|PageNumber|Integer|1|部署集列表的页数。

 |
|PageSize|Integer|10|设置的每页行数。

 |
|RegionId|String|cn-hangzhou|部署集所处的地域 ID。

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。

 |
|TotalCount|Integer|1|查询到的部署集总数。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

https://ecs.aliyuncs.com/?Action=DescribeDeploymentSets
&RegionId=cn-hangzhou
&DeploymentSetsIds=["ds-bp13v7bjnj9gisnlo1"]
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeDeploymentSetsResponse>
  <PageSize>10</PageSize>
  <TotalCount>1</TotalCount>
  <PageNumber>1</PageNumber>
  <RequestId>1CB9A584-9E43-408D-B5A8-DB42CDECE03B</RequestId>
  <DeploymentSets>
    <DeploymentSet>
      <DeploymentSetDescription>default</DeploymentSetDescription>
      <DeploymentSetId>ds-bp13v7bjnj9gisnlo1ow</DeploymentSetId>
      <DeploymentStrategy>Availability</DeploymentStrategy>
      <DeploymentSetName>test default</DeploymentSetName>
      <InstanceIds>
        <InstanceId>i-sdfkjsdfk</InstanceId>
        <InstanceId>i-kiiwsch</InstanceId>
      </InstanceIds>
    </DeploymentSet>
  </DeploymentSets>
</DescribeDeploymentSetsResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"DeploymentSets":{
		"DeploymentSet":[
			{
				"DeploymentSetDescription":"default",
				"InstanceIds":{
					"InstanceId":[
						"i-sdfkjsdfk",
						"i-kiiwsch"
					]
				},
				"DeploymentSetName":"test default",
				"DeploymentStrategy":"Availability",
				"DeploymentSetId":"ds-bp13v7bjnj9gisnlo1ow"
			}
		]
	},
	"PageNumber":1,
	"TotalCount":1,
	"PageSize":10,
	"RequestId":"1CB9A584-9E43-408D-B5A8-DB42CDECE03B"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|403|InvalidDeploymentSetIds.TooManyInput|The parameter DeploymentSets size should less than 100.|指定的 DeploymentSets 数量大于 100。|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Ecs)

