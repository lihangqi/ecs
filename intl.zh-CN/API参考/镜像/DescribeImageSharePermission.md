# DescribeImageSharePermission {#doc_api_1091446 .reference}

查询一份自定义镜像已经共享的所有用户。返回结果支持分页显示，每页的信息条目默认为 10 条。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=DescribeImageSharePermission)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|ImageId|String|是|m-imageid1|自定义镜像 ID。

 |
|RegionId|String|是|cn-hangzhou|自定义镜像所属的地域 ID。您可以调用 [DescribeRegions](~~25609~~) 查看最新的阿里云地域列表。

 |
|Action|String|否|DescribeImageSharePermission|系统规定参数。取值：DescribeImageSharePermission

 |
|OwnerAccount|String|否|ECSforCloud@Alibaba.com|RAM用户的账号登录名称。

 |
|PageNumber|Integer|否|1|查询结果显示的页码。起始值：1 默认值：1

 |
|PageSize|Integer|否|10|查询结果显示的每页的信息条目数。最大值：50 默认值：10

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|Accounts| | |阿里云账号类型

 |
|└AliyunId|String|155780923770|阿里云账号 ID

 |
|ImageId|String|m-imageid2|自定义镜像 ID

 |
|PageNumber|Integer|1|查询结果显示的页码

 |
|PageSize|Integer|10|每页的信息条目数

 |
|RegionId|String|cn-hangzhou|镜像所属地域 ID

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。无论调用接口成功与否，我们都会返回请求 ID。

 |
|ShareGroups| | |共享组类型

 |
|└Group|String|all|共享分组

 |
|TotalCount|Integer|1|记录总数

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

https://ecs.aliyuncs.com/?Action=DescribeImageSharePermission
&ImageId=m-imageid1
&RegionId=cn-hangzhou
&PageNumber=1
&PageSize=10
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeImageSharePermissionResponse>
  <ImageId>m-282dzntc7</ImageId>
  <PageNumber>1</PageNumber>
  <PageSize>10</PageSize>
  <RegionId>cn-qingdao</RegionId>
  <TotalCount>1</TotalCount>
  <RequestId>441CF898-42FF-47CF-9348-3C3BFF557278</RequestId>
  <ShareGroups>
    <ShareGroup>
      <Group>all</Group>
    </ShareGroup>
  </ShareGroups>
  <Accounts>
    <Account>
      <AliyunId>155780923770</AliyunId>
    </Account>
  </Accounts>
</DescribeImageSharePermissionResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"Accounts":{
		"Account":[
			{
				"AliyunId":"155780923770"
			}
		]
	},
	"PageNumber":1,
	"ImageId":"m-282dzntc7",
	"TotalCount":1,
	"PageSize":10,
	"RequestId":"9AD96F49-0BE5-4868-A66A-224352549CEC",
	"RegionId":"cn-qingdao",
	"ShareGroups":{
		"ShareGroup":[
			{
				"Group":"all"
			}
		]
	}
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|MissingParameter|The input parameter "RegionId "that is mandatory for processing this request is not supplied.|缺失必需参数RegionId。|
|400|MissingParameter|The input parameter "ImageId "that is mandatory for processing this request is not supplied.|缺失必需参数ImageId。|
|404|InvalidImageId.NotFound|The specified ImageId does not exist.|指定的镜像在该用户账号下不存在，请您检查镜像id是否正确。|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Ecs)

