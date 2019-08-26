# DescribeImageSharePermission {#DescribeImageSharePermission .reference}

查询一份自定义镜像已经共享的所有用户。返回结果支持分页显示，每页的信息条目默认为 10 条。

## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：DescribeImageSharePermission|
|RegionId|String|是|自定义镜像所属的地域 ID。您可以调用 [DescribeRegions](intl.zh-CN/API参考/地域/DescribeRegions.md#) 查看最新的阿里云地域列表。|
|ImageId|String|是|自定义镜像 ID。|
|PageNumber|Integer|否|查询结果显示的页码。起始值：1默认值：1

|
|PageSize|Integer|否|查询结果显示的每页的信息条目数。最大值：50默认值：10

|

## 返回参数 {#ResponseParameter .section}

|名称|类型|描述|
|:-|:-|:-|
|ImageId|String|自定义镜像 ID|
|RegionId|String|镜像所属地域 ID|
|ShareGroups|[ShareGroupType](intl.zh-CN/API参考/数据类型/ShareGroupType.md#)|共享组类型|
|Accounts|[AccountType](intl.zh-CN/API参考/数据类型/AccountType.md#)|阿里云账号类型|
|TotalCount|Integer|记录总数|
|PageNumber|Integer|查询结果显示的页码|
|PageSize|Integer|每页的信息条目数|

## 示例 { .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=DescribeImageSharePermission
&RegionId=cn-qingdao
&ImageId=m-282dzntc7
&<公共请求参数>
```

**返回示例** 

**XML 格式**

```
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
            <AliyunId>1886508529898586</AliyunId>
        </Account>
    </Accounts>
</DescribeImageSharePermissionResponse>
```

 **JSON 格式** 

```
{
    "ShareGroups": {
        "ShareGroup": [
            {
                "Group": "all"
            }
        ]
    },
    "Accounts": {
        "Account": [
            {
                "AliyunId": "1886508529898586"
            }
        ]
    },
    "ImageId": "m-282dzntc7",
    "PageNumber": 1,
    "PageSize": 10,
    "RegionId": "cn-qingdao",
    "TotalCount": 1,
    "RequestId": "9AD96F49-0BE5-4868-A66A-224352549CEC"
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问 [API 错误中心](https://error-center.alibabacloud.com/status/product/Ecs)。

|错误代码|错误信息|HTTP 状态码|说明|
|:---|:---|:-------|:-|
|MissingParameter|The input parameter “RegionId “ that is mandatory for processing this request is not supplied.|400|您必须指定参数 `RegionId`。|
|MissingParameter|The input parameter “ImageId “ that is mandatory for processing this request is not supplied.|400|您必须指定参数 `ImageId`。|
|InvalidRegionId.NotFound|The specified region does not exist.|404|指定的 `RegionId` 不存在。|
|InvalidImageId.NotFound|The specified ImageId does not exist.|404|指定的自定义镜像不存在。|

