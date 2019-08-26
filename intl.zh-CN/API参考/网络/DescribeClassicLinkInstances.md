# DescribeClassicLinkInstances {#doc_api_1030608 .reference}

查询一台或多台与专有网络 VPC 建立了连接的经典网络类型实例。

## 接口说明 {#description .section}

调用该接口时，您需要注意：

-   该接口仅支持经典网络类型实例。
-   单次最多只能查询 100 台经典网络类型实例。
-   参数 VpcId 和 InstanceId 不能同时为空。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=DescribeClassicLinkInstances)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|RegionId|String|是|cn-hangzhou|实例所属的地域 ID。您可以调用 [DescribeRegions](~~25609~~) 查看最新的阿里云地域列表。

 |
|Action|String|否|DescribeClassicLinkInstances|系统规定参数。取值：DescribeClassicLinkInstances

 |
|InstanceId|String|否|i-test|实例 ID。最多指定 100 台实例 ID，并使用半角逗号（,）隔开。

 |
|PageNumber|String|否|1|当前页码。起始值：1

 默认值：1

 |
|PageSize|String|否|10|分页查询时设置的每页行数。取值范围：1~100

 默认值：10

 |
|VpcId|String|否|vpc-test|VPC ID。目标 VPC 必须已 [开启 ClassicLink 功能](~~65413~~)。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|Links| | |返回经典网络类型实例和 VPC 连接信息

 |
|└InstanceId|String|i-test|实例ID

 |
|└VpcId|String|vpc-test|VPC ID

 |
|PageNumber|Integer|1|连接列表的页码

 |
|PageSize|Integer|10|输入时设置的每页行数

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID

 |
|TotalCount|Integer|2|连接总数

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

https://ecs.aliyuncs.com/?Action=DescribeClassicLinkInstances
&RegionId=cn-hangzhou
&VpcId=vpc-test
&InstanceId=i-test, i-test1
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeClassicLinkInstancesResponse>
  <RequestId>B154D309-F3E1-4AB7-BA94-FEFCA8B89001</RequestId>
  <TotalCount>2</TotalCount>
  <PageNumber>1</PageNumber>
  <PageSize>10</PageSize>
  <Links>
    <Link>
      <InstanceId>i-test</InstanceId>
      <VpcId>vpc-test</VpcId>
    </Link>
    <Link>
      <InstanceId>i-test1</InstanceId>
      <VpcId>vpc-test</VpcId>
    </Link>
  </Links>
</DescribeClassicLinkInstancesResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"PageNumber":1,
	"TotalCount":2,
	"Links":{
		"Link":[
			{
				"InstanceId":"i-test",
				"VpcId":"vpc-test"
			},
			{
				"InstanceId":"i-test1",
				"VpcId":"vpc-test"
			}
		]
	},
	"PageSize":10,
	"RequestId":"B154D309-F3E1-4AB7-BA94-FEFCA8B89001"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|403|InvalidInstanceId.NotBelong|The specified instance is not belong to you.|指定的实例不在您账号下。|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Ecs)

