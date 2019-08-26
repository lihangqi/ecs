# RemoveTags {#RemoveTags .reference}

从云服务器 ECS 资源上解绑一个或多个标签，例如，实例、磁盘、快照、镜像和安全组等。

## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：RemoveTags|
|RegionId|String|是|资源所属地域。您可以调用 [DescribeRegions](intl.zh-CN/API参考/地域/DescribeRegions.md#) 查看最新的阿里云地域列表。|
|ResourceType|String|是|资源类型。取值范围：-   disk
-   instance
-   image
-   securitygroup
-   snapshot

以上取值均为小写。|
|ResourceId|String|是|要解绑标签的资源 ID。例如，当资源类型（`ResourceType`）为实例（`instance`）时，资源 ID 可以理解为实例 ID。|
|Tag.n.Key|String|否|标签键，`n` 的取值范围为 \[1, 5\]。您可以调用 [DescribeTags](intl.zh-CN/API参考/标签/DescribeTags.md#) 查看您可用的标签。|
|Tag.n.Value|String|否|标签值，`n` 的取值范围为 \[1, 5\]。如果您不指定该参数，则解绑由参数 `Tag.n.Key` 确定的标签。|

## 返回参数 {#section_f54_lk5_xdb .section}

全是公共返回参数。参阅 [公共参数](intl.zh-CN/API参考/调用方式/公共参数.md#commonResponseParameters)。

## 示例 { .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=RemoveTags
&ResourceId=s-946ntx4wr
&ResourceType=snapshot
&RegionId=cn-shenzhen
&Tag.1.Key=test
&Tag.1.Value=api
&<公共请求参数>
```

**返回示例** 

**XML 格式**

```
<RemoveTagsResponse>
    <RequestId>6A2C8AB5-E15D-478C-B56A-CF3DAF060028</RequestId>
</RemoveTagsResponse>
```

 **JSON 格式** 

```
{
  "RequestId": "6A2C8AB5-E15D-478C-B56A-CF3DAF060028"
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问 [API 错误中心](https://error-center.alibabacloud.com/status/product/Ecs)。

|错误代码|错误信息|HTTP 状态码|说明|
|:---|:---|:-------|:-|
|InvalidTagCount|The specified tags are beyond the permitted range.|400|指定的标签数不能超过五个。|
|InvalidResourceId.NotSupported|The specified ResourceId does not support tagging.|403|指定的资源不支持标签功能。|
|InvalidResourceId.NotFound|The specified ResourceId is not found in our records.|404|指定的 `ResourceId`不存在。|
|InvalidRegionId.NotFound|The RegionId provided does not exist in our records.|404|指定的 `RegionId` 不存在。|
|InvalidResourceType.NotFound|The ResourceType provided does not exist in our records.|404|指定的 `ResourceType` 不存在。|

