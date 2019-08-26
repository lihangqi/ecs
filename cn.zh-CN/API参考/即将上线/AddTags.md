# AddTags {#doc_api_Ecs_AddTags .reference}

添加或者覆盖一个或者多个标签到云服务器ECS的各项资源上。您可以添加标签到实例、磁盘、快照、镜像、安全组等，便于管理资源。

## 接口说明 {#description .section}

调用该接口时，您需要注意：

-   单项云服务器ECS资源最多可以添加20个标签。
-   标签键（`Tag.N.Key`）与标签值（`Tag.N.Value`）必须键值匹配。
-   如果标签键（`Tag.N.Key`）在指定的资源上已经存在，则使用新的标签值（`Tag.N.Value`）自动覆盖原标签值。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=AddTags)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|RegionId|String|是|cn-hangzhou|资源所在的地域。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。

 |
|ResourceId|String|是|i-instanceid1|要绑定标签的资源ID。例如，当资源类型（ResourceType）为实例（instance）时，资源ID可以理解为实例ID。

 |
|ResourceType|String|是|instance|资源类型。取值范围：

 -   disk
-   instance
-   image
-   securitygroup
-   snapshot

 以上取值均为小写。

 |
|Action|String|否|AddTags|系统规定参数。取值：AddTags

 |
|Tag.N.Key|String|否|Finance|资源的标签键。N的取值范围：1~20。一旦传入该值，则不允许为空字符串。最多支持64个字符，不能以aliyun和acs:开头，不能包含 http:// 或者 https:// 。

 |
|Tag.N.Value|String|否|FinanceJoshua|资源的标签值。N的取值范围：1~20。一旦传入该值，可以为空字符串。最多支持128个字符，不能以aliyun和acs:开头，不能包含 http:// 或者 https:// 。

 |
|Tag.N.key|String|否|Finance|资源的标签键。

 **说明：** 为提高兼容性，建议您尽量使用Tag.N.Key参数。

 |
|Tag.N.value|String|否|FinanceJoshua|资源的标签值。

 **说明：** 为提高兼容性，建议您尽量使用Tag.N.Value参数。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=AddTags
&RegionId=cn-hangzhou
&ResourceId=i-instanceid1
&ResourceType=instance
&Tag.1.value=FinanceJoshua
&Tag.1.key=Finance
&Tag.1.Key=Finance
&Tag.1.Value=FinanceJoshua
&<公共请求参数>
```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<AddTagsResponse>
  <RequestId>C46FF5A8-C5F0-4024-8262-B16B639225A0</RequestId>
</AddTagsResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"C46FF5A8-C5F0-4024-8262-B16B639225A0"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|404|InvalidRegionId.NotFound|The specified RegionId does not exist.|指定的 RegionId 不存在，请您检查此产品在该地域是否可用。|
|404|InvalidResourceId.NotFound|The specified ResourceId is not found in our records.|指定的资源不存在，请您检查该资源是否正确。|
|404|InvalidResourceType.NotFound|The ResourceType provided does not exist in our records.|指定的资源类型不存在。|
|400|InvalidTagKey.Malformed|The specified Tag.n.Key is not valid.|指定的标签键不合法。|
|400|InvalidTagValue.Malformed|The specified Tag.n.Value is not valid.|指定的标签值不合法。|
|400|OperationDenied.QuotaExceed|The quota of tags on resource is beyond permitted range.|资源标签已达上限。|
|403|InvalidResourceId.NotSupported|The specified ResourceId does not support tagging.|指定的资源 ID 不支持标记。|
|400|InvalidTag.Mismatch|The specified Tag.n.Key and Tag.n.Value are not match.|指定的 Tag.n.Key 和 Tag.n.Value 不匹配。|
|400|InvalidTagCount|The specified tags are beyond the permitted range.|指定的标记超出取值范围。|
|400|Duplicate.TagKey|The Tag.N.Key contain duplicate key.|标签键中存在重复的键。|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Ecs)

