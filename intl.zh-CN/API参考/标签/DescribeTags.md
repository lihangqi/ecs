# DescribeTags {#doc_api_Ecs_DescribeTags .reference}

查询可以供您使用的标签。您可以根据资源类型、资源ID、标签键或标签值等条件查询标签，筛选条件之间为逻辑与（&&）关系，返回满足所有筛选条件的标签。

## 接口说明 {#description .section}

如果您指定了标签键（Tag.N.Key）但没有指定标签值（Tag.N.Value），我们将查询该标签键对应的所有标签键值对。如果您指定了标签键值对，就查询精确匹配该键值对的标签。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=DescribeTags)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|RegionId|String|是|cn-hangzhou|地域ID。您可以调用 [DescribeRegions](~~25609~~) 查看最新的阿里云地域列表。

 |
|Action|String|否|DescribeTags|系统规定参数。取值：DescribeTags

 |
|PageNumber|Integer|否|1|标签列表的页码。 起始值：1

 默认值：1

 |
|PageSize|Integer|否|50|分页查询时设置的每页行数。 最大值：100

 默认值：50

 |
|ResourceId|String|否|s-946ntx4wr|标签绑定的资源ID。例如，当资源类型（ResourceType）为实例（instance）时，资源ID可以理解为实例ID。

 |
|ResourceType|String|否|snapshot|资源类型。取值范围：

 -   disk
-   instance
-   image
-   securitygroup
-   snapshot

 以上取值均为小写。

 |
|Tag.N.Key|String|否|Finance|资源的标签键。N 的取值范围：1~20。一旦传入该值，则不允许为空字符串。最多支持 64 个字符，不能以 aliyun 和 acs: 开头，不能包含 http:// 或者 https:// 。

 |
|Tag.N.Value|String|否|Finance|资源的标签值。N 的取值范围：1~20。一旦传入该值，可以为空字符串。最多支持 128 个字符，不能以 aliyun 和 acs: 开头，不能包含 http:// 或者 https:// 。

 |
|Tag.N.key|String|否|Finance|资源的标签键。

 **说明：** 该参数即将被弃用，为提高兼容性，建议您尽量使用Tag.N.Key参数。

 |
|Tag.N.value|String|否|Finance|资源的标签值。

 **说明：** 该参数即将被弃用，为提高兼容性，建议您尽量使用Tag.N.Value参数。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|PageNumber|Integer|1|标签列表的页码

 |
|PageSize|Integer|50|分页查询时设置的每页行数

 |
|RequestId|String|B04B8CF3-4489-432D-83BA-6F128E4F2295|请求 ID

 |
|Tags| | |满足所有筛选条件的标签

 |
|└ResourceTypeCount| | |资源类型计数。

 |
|└Ddh|Integer|1|该标签标记了多少专有宿主机。

 |
|└Disk|Integer|15|该标签标记了多少磁盘。

 |
|└Eni|Integer|5|该标签标记了多少弹性网卡。

 |
|└Image|Integer|6|该标签标记了多少镜像。

 |
|└Instance|Integer|45|该标签标记了多少实例。

 |
|└KeyPair|Integer|17|该标签标记了多少密钥对。

 |
|└LaunchTemplate|Integer|6|该标签标记了多少启动模板。

 |
|└Securitygroup|Integer|4|该标签标记了多少安全组。

 |
|└Snapshot|Integer|15|该标签标记了多少快照。

 |
|└Volume|Integer|6|该标签标记了多少扩展卷。

 |
|└TagKey|String|test|标签键

 |
|└TagValue|String|api|标签值

 |
|TotalCount|Integer|1|标签总个数

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

https://ecs.aliyuncs.com/?Action=DescribeTags
&RegionId=cn-hangzhou
&PageSize=50
&PageNumber=1
&ResourceType=snapshot
&ResourceId=s-946ntx4wr
&Tag.1.value=Finance
&Tag.1.key=Finance
&Tag.1.Key=Finance
&Tag.1.Value=Finance
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeTagsResponse>
  <RequestId>B04B8CF3-4489-432D-83BA-6F128E4F2295</RequestId>
  <PageNumber>1</PageNumber>
  <PageSize>50</PageSize>
  <Tags>
    <Tag>
      <TagKey>test</TagKey>
      <TagValue>api</TagValue>
    </Tag>
  </Tags>
  <TotalCount>1</TotalCount>
</DescribeTagsResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"Tags":{
		"Tag":[
			{
				"TagValue":"api",
				"TagKey":"test"
			}
		]
	},
	"PageNumber":1,
	"TotalCount":1,
	"PageSize":50,
	"RequestId":"B04B8CF3-4489-432D-83BA-6F128E4F2295"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|404|InvalidRegionId.NotFound|The specified RegionId does not exist.|指定的 RegionId 不存在，请您检查此产品在该地域是否可用。|
|404|InvalidResourceType.NotFound|The ResourceType provided does not exist in our records.|指定的资源类型不存在。|
|400|InvalidTagCount|The specified tags are beyond the permitted range.|指定的标记超出取值范围。|
|400|InvalidTagKey.Malformed|The parameter Tag.n.Key is illegal.|Tag.n.Key 不合法。|
|400|InvalidTagValue.Malformed|The parameter Tag.n.Value is illegal.|Tag.n.Value 不合法。|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Ecs)

