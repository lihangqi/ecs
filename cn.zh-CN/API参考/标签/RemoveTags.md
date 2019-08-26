# RemoveTags {#doc_api_Ecs_RemoveTags .reference}

从实例、磁盘、快照、镜像或者安全组等解绑一个或多个标签。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=RemoveTags)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|RegionId|String|是|cn-shenzhen|资源所属地域。您可以调用 [DescribeRegions](~~25609~~) 查看最新的阿里云地域列表。

 |
|ResourceId|String|是|s-946ntx4wr|要解绑标签的资源ID。例如，当资源类型（ResourceType）为实例（instance）时，资源ID可以理解为实例 ID。

 |
|ResourceType|String|是|snapshot|资源类型。取值范围：

 -   disk
-   instance
-   image
-   securitygroup
-   snapshot

 以上取值均为小写。

 |
|Action|String|否|RemoveTags|系统规定参数。取值：RemoveTags

 |
|Tag.N.Key|String|否|Finance|资源的标签键。N 的取值范围：1~20。一旦传入该值，则不允许为空字符串。最多支持 64 个字符，不能以 aliyun 和 acs: 开头，不能包含 http:// 或者 https:// 。

 |
|Tag.N.Value|String|否|FinanceJoshua|资源的标签值。N 的取值范围：1~20。一旦传入该值，可以为空字符串。最多支持 128 个字符，不能以 aliyun 和 acs: 开头，不能包含 http:// 或者 https:// 。

 |
|Tag.N.key|String|否|Finance|资源的标签键。

 **说明：** 该参数即将被弃用，为提高兼容性，建议您尽量使用Tag.N.Key参数。

 |
|Tag.N.value|String|否|FinanceJoshua|资源的标签值。

 **说明：** 该参数即将被弃用，为提高兼容性，建议您尽量使用Tag.N.Value参数。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

https://ecs.aliyuncs.com/?Action=RemoveTags
&RegionId=cn-shenzhen
&ResourceId=s-946ntx4wr
&ResourceType=snapshot
&Tag.1.value=FinanceJoshua
&Tag.1.key=Finance
&Tag.1.Key=Finance
&Tag.1.Value=FinanceJoshua
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<RemoveTagsResponse>
  <RequestId>6A2C8AB5-E15D-478C-B56A-CF3DAF060028</RequestId>
</RemoveTagsResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"6A2C8AB5-E15D-478C-B56A-CF3DAF060028"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|404|InvalidResourceId.NotFound|The specified ResourceId is not found in our records.|指定的资源不存在，请您检查该资源是否正确。|
|404|InvalidRegionId.NotFound|The specified RegionId does not exist.|指定的 RegionId 不存在，请您检查此产品在该地域是否可用。|
|404|InvalidResourceType.NotFound|The ResourceType provided does not exist in our records.|指定的资源类型不存在。|
|403|InvalidResourceId.NotSupported|The specified ResourceId does not support tagging.|指定的资源 ID 不支持标记。|
|400|InvalidTagCount|The specified tags are beyond the permitted range.|指定的标记超出取值范围。|
|400|InvalidTagKey.Malformed|The specified Tag.n.Key is not valid.|指定的标签键不合法。|
|400|InvalidResourceType.NotFound|The specified ResourceType does not exist.|资源类型不合法。|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Ecs)

