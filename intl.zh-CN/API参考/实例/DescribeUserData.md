# DescribeUserData {#doc_api_1161579 .reference}

查询一台 ECS 实例的 自定义数据。

## 描述 {#description .section}

-   返回的实例自定义数据将以 Base64 编码的方式显示。
-   如果实例不存在自定义数据，则返回空值。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=DescribeUserData)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|InstanceId|String|是|i-instanceid1|要查询的实例 ID。

 |
|RegionId|String|是|cn-hangzhou|实例所属的地域 ID。您可以调用 [DescribeRegions](~~25609~~) 查看最新的阿里云地域列表。

 |
|Action|String|否|DescribeUserData|系统规定参数。取值：DescribeUserdata

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|InstanceId|String|i-instanceid1|实例ID

 |
|RegionId|String|cn-hangzhou|地域 ID

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。无论调用接口成功与否，我们都会返回请求 ID。

 |
|UserData|String|ZWNobyBoZWxsbyBlY3Mh|实例的自定义数据，并以 Base64 编码方式的方式显示

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

https://ecs.aliyuncs.com/?Action= DescribeUserdata
&RegionId=cn-shenzhen
&InstanceId=i-instance1
&<公共请求参数>


```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeUserdataResponse>
  <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
  <UserData>userdata1</UserData>
  <InstanceId> i-instance1</InstanceId>
  <RegionId> cn-shenzhen </RegionId>
</DescribeUserdataResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	" UserData ":" userdata1",
	"RequestId":"473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E",
	" InstanceId ":" i-instance1",
	" RegionId":"cn-shenzhen"
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/Ecs)

