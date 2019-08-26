# DescribeInstanceTypeFamilies {#DescribeInstanceTypeFamilies .reference}

查询云服务器 ECS 提供的实例规格族资源。更多详情，请参阅 [实例规格族](../../../../intl.zh-CN/产品简介/实例规格族.md#)。

## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：DescribeInstanceTypeFamilies|
|RegionId|String|是|地域 ID。您可以调用 [DescribeRegions](intl.zh-CN/API参考/地域/DescribeRegions.md#) 查看最新的阿里云地域列表。|
|Generation|String|否|实例规格族的系列信息。取值范围：-   ecs-1：系列 I 实例规格，上线时间较早，性价比高。
-   ecs-2：系列 II 实例规格族，第二次软硬件升级，实例性能增强。
-   ecs-3：系列 III 实例规格族，最新规格族，实例性能优良，能承载不同业务需求，响应更快。

|

## 返回参数 {#ResponseParameter .section}

|名称|类型|描述|
|:-|:-|:-|
|InstanceTypeFamilies|[InstanceTypeFamilyItemType](intl.zh-CN/API参考/数据类型/InstanceTypeFamilyItemType.md#)|由实例规格族 InstanceTypeFamilyItemType 组成的集合|

## 示例 { .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=DescribeInstanceTypeFamilies
&RegionId=cn-hangzhou
&<公共请求参数>
```

**返回示例** 

**XML 格式**

```
<DescribeInstanceTypeFamiliesResponse>
    <InstanceTypeFamilies>
        <InstanceTypeFamily>
            <InstanceTypeFamilyId>ecs.t1</InstanceTypeFamilyId>
            <Generation>ecs-1</Generation>
        </InstanceTypeFamily>
        <InstanceTypeFamily>
            <InstanceTypeFamilyId>ecs.s2</InstanceTypeFamilyId>
            <Generation>ecs-1</Generation>
        </InstanceTypeFamily>
        <InstanceTypeFamily>
            <InstanceTypeFamilyId>ecs.s3</InstanceTypeFamilyId>
            <Generation>ecs-1</Generation>
        </InstanceTypeFamily>
    </InstanceTypeFamilies>
    <RequestId>6B187E0A-C075-4D08-8B6F-6213950E8733</RequestId>
</DescribeInstanceTypeFamiliesResponse>
```

 **JSON 格式** 

```
{
    "InstanceTypeFamilies":{
        "InstanceTypeFamily":[
            {
                "InstanceTypeFamilyId":"ecs.t1",
                "Generation":"ecs-1"
            },
            {
                "InstanceTypeFamilyId":"ecs.s2",
                "Generation":"ecs-1"
            },
            {
                "InstanceTypeFamilyId":"ecs.s3",
                "Generation":"ecs-1"
            }
        ]
    },
    "RequestId":"6B187E0A-C075-4D08-8B6F-6213950E8733"
}
```

## 错误码 {#ErrorCode .section}

全是公共错误码。更多错误码，请访问 [API 错误中心](https://error-center.alibabacloud.com/status/product/Ecs)。

