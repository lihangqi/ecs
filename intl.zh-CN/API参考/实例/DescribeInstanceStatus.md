# DescribeInstanceStatus {#doc_api_1161574 .reference}

批量获取实例状态信息。

## 描述 {#description .section}

-   能查询到的所有可能的实例状态参阅 [实例状态表](~~25687~~)。
-   该接口同时可用于获取实例列表。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=DescribeInstanceStatus)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|RegionId|String|是|cn-hangzhou|实例所属的地域 ID。您可以调用 [DescribeRegions](~~25609~~) 查看最新的阿里云地域列表。

 |
|Action|String|否|DescribeInstanceStatus|系统规定参数。取值：DescribeInstanceStatus

 |
|ClusterId|String|否|cls-clusterid1|实例所属的集群 ID。

 **说明：** 该参数即将被弃用，为提高兼容性，请尽量使用其他参数。

 |
|OwnerAccount|String|否|ECSforCloud|RAM用户的账号登录名称。

 |
|PageNumber|Integer|否|1|实例状态列表的页码。起始值：1

 默认值：1

 |
|PageSize|Integer|否|10|分页查询时设置的每页行数。取值范围：1~50

 默认值： 10

 |
|ZoneId|String|否|cn-hangzhou-d|实例所属可用区

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|InstanceStatuses| | |实例状态集类型（InstanceStatusSetType）

 |
|└InstanceId|String|i-instance1|实例 ID。

 |
|└Status|String|Running|实例状态。

 |
|PageNumber|Integer|1|实例列表的页码

 |
|PageSize|Integer|10|输入时设置的每页行数

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID

 |
|TotalCount|Integer|2|实例总个数

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

https://ecs.aliyuncs.com/?Action=DescribeInstanceStatus
&RegionId=cn-hangzhou
&ZoneId=cn-hangzhou-d
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeInstanceStatusResponse>
  <RequestId>6EF60BEC-0242-43AF-BB20-270359FB54A7</RequestId>
  <TotalCount>2</TotalCount>
  <PageNumber>1</PageNumber>
  <PageSize>10</PageSize>
  <InstanceStatuses>
    <InstanceStatus>
      <InstanceId>i-instance1</InstanceId>
      <Status>Running</Status>
    </InstanceStatus>
    <InstanceStatus>
      <InstanceId>i-ae4r89pp</InstanceId>
      <Status>Stopped</Status>
    </InstanceStatus>
  </InstanceStatuses>
</DescribeInstanceStatusResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"PageNumber":1,
	"InstanceStatuses":{
		"InstanceStatus":[
			{
				"Status":"Running",
				"InstanceId":"i-instance1"
			},
			{
				"Status":"Stopped",
				"InstanceId":"i-ae4r89pp"
			}
		]
	},
	"TotalCount":2,
	"PageSize":10,
	"RequestId":"6EF60BEC-0242-43AF-BB20-270359FB54A7"
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/Ecs)

