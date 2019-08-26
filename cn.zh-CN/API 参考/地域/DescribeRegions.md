# DescribeRegions {#DescribeRegions .reference}

查询您可以使用的阿里云地域。更多详情，请参阅 [地域与可用区](https://www.alibabacloud.com/help/doc-detail/40654.htm)。

## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：DescribeRegions|
|AcceptLanguage|String|否|根据汉语、英语和日语筛选返回结果。更多详情，请参阅 [RFC7231](https://tools.ietf.org/html/rfc7231)。取值范围：

-   zh-CN
-   en-US
-   ja

默认值：null。|

## 返回参数 {#ResponseParameter .section}

|名称|类型|描述|
|:-|:-|:-|
|Regions|[RegionType](intl.zh-CN/API 参考/数据类型/RegionType.md#)|地域信息集合|

## 示例 { .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=DescribeRegions
&<公共请求参数>
```

**返回示例** 

**XML 格式**

```
<DescribeRegionsResponse>
    <RequestId>38EC7366-F5A9-46B1-BDB1-0FDC2E296397</RequestId>
    <Regions>
        <Region>
            <RegionId>cn-shanghai-et2-bo1</RegionId>
            <RegionEndpoint>ecs.aliyuncs.com</RegionEndpoint>
            <LocalName>弹内生产环境-上海</LocalName>
        </Region>
        <Region>
            <RegionId>cn-qingdao-nebula</RegionId>
            <RegionEndpoint>ecs.cn-qingdao-nebula.aliyuncs.com</RegionEndpoint>
            <LocalName>cn-qingdao-nebula</LocalName>
        </Region>
    </Regions>
</DescribeRegionsResponse>
```

**JSON 格式** 

```
{
    "RequestId":"38EC7366-F5A9-46B1-BDB1-0FDC2E296397",
    "Regions":{
        "Region":[
            {
                "RegionId":"cn-shanghai-et2-b01",
                "RegionEndpoint":"ecs.aliyuncs.com",
                "LocalName":"弹内生产环境-上海"
            },
            {
                "RegionId":"cn-qingdao-nebula",
                "RegionEndpoint":"ecs.cn-qingdao-nebula.aliyuncs.com",
                "LocalName":"cn-qingdao-nebula"
            }
        ]
    }
}
```

## 错误码 {#ErrorCode .section}

全是公共错误码。更多错误码，请访问 [API 错误中心](https://error-center.alibabacloud.com/status/product/Ecs)。

