# DescribeTags {#DescribeTags .reference}

查询可以供您使用的标签。您可以根据资源类型、资源ID、标签键或标签值等条件查询标签，筛选条件之间为逻辑与（&&）关系，返回满足所有筛选条件的标签。

## 描述 {#section_zxn_2ph_ydb .section}

如果您指定了标签键（`Tag.n.Key`）但没有指定标签值（`Tag.n.Value`），我们将查询该标签键对应的所有标签键值对。如果您指定了标签键值对，就查询精确匹配该键值对的标签。

## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：DescribeTags|
|RegionId|String|是|地域ID。您可以调用[DescribeRegions](../cn.zh-CN/API 参考/地域/DescribeRegions.md#)查看最新的阿里云地域列表。|
|ResourceType|String|是|资源类型。取值范围：-   disk
-   instance
-   image
-   securitygroup
-   snapshot

以上取值均为小写。|
|ResourceId|String|否|标签绑定的资源ID。例如，当资源类型（`ResourceType`）为实例（`instance`）时，资源ID可以理解为实例ID。|
|Tag.n.Key|String|否|资源的标签键。n的取值范围：\[1, 20\]。一旦传入该值，则不允许为空字符串。最多支持64个字符，不能以aliyun、acs:、http://或者https://开头。|
|Tag.n.Value|String|否|资源的标签值。n的取值范围：\[1, 20\]。一旦传入该值，可以为空字符串。最多支持128个字符，不能以aliyun、acs:、http://或者https://开头。|
|PageNumber|Integer|否| 标签列表的页码。

 起始值：1

 默认值：1

 |
|PageSize|Integer|否| 分页查询时设置的每页行数。

 最大值：100

 默认值：50

 |

## 返回参数 {#ResponseParameter .section}

|名称|类型|描述|
|:-|:-|:-|
|Tags|[TagSetItem](cn.zh-CN/API 参考/数据类型/TagSetItem.md#)|满足所有筛选条件的标签|
|TotalCount|Integer|标签总个数|
|PageSize|Integer|分页查询时设置的每页行数|
|PageNumber|Integer|标签列表的页码|

## 示例 { .section}

**请求示例**

```
https://ecs.aliyuncs.com/?Action=DescribeTags
&ResourceType=snapshot
&ResourceId=s-946ntx4wr
&RegionId=cn-hangzhou
&Tag.1.Key=test
&Tag.1.Value=api
&<公共请求参数>
```

**返回示例**

**XML格式**

```
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

**JSON格式**

```
{
  "PageNumber": 1,
  "PageSize": 50,
  "RequestId": "B04B8CF3-4489-432D-83BA-6F128E4F2295",
  "Tags": {
    "Tag": [
      {
        "TagKey": "test",
        "TagValue": "api"
      }
    ]
  },
  "TotalCount": 1
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问[API错误中心](https://error-center.aliyun.com/status/product/Ecs)。

|错误代码|错误信息|HTTP状态码|说明|
|:---|:---|:------|:-|
|nvalidTagKey.Malformed|The parameter Tag.n.Key is illegal.|400|指定的`Tag.n.Key`不合法。|
|InvalidTagValue.Malformed|The parameter Tag.n.Value is illegal.|400|指定的`Tag.n.Value`不合法。|
|InvalidRegionId.NotFound|The RegionId provided does not exist in our records.|404|指定的`RegionId`不存在。|
|InvalidResourceType.NotFound|The ResourceType provided does not exist in our records.|404|指定的`ResourceType`不存在。|

