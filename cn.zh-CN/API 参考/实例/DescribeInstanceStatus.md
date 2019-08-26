# DescribeInstanceStatus {#DescribeInstanceStatus .reference}

批量获取实例状态信息。

## 描述 {#section_yfq_yps_xdb .section}

-   能查询到的所有可能的实例状态参阅 [实例状态表](intl.zh-CN/API参考/附录/实例状态表.md#)。
-   该接口同时可用于获取实例列表。

## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：DescribeInstanceStatus|
|RegionId|String|是|实例所属的地域 ID。您可以调用 [DescribeRegions](intl.zh-CN/API参考/地域/DescribeRegions.md#) 查看最新的阿里云地域列表。|
|ZoneId|String|否|实例所属可用区|
|PageNumber|Integer|否|实例状态列表的页码。起始值：1默认值：1

|
|PageSize|Integer|否|分页查询时设置的每页行数。取值范围：\[1, 50\]默认值： 10

|

## 返回参数 {#ResponseParameter .section}

|名称|类型|描述|
|:-|:-|:-|
|TotalCount|Integer|实例总个数|
|PageNumber|Integer|实例列表的页码|
|PageSize|Integer|输入时设置的每页行数|
|InstanceStatuses|Array|实例状态集类型（`[InstanceStatusSetType](intl.zh-CN/API参考/数据类型/InstanceStatusSetType.md#)`）|

## 示例 { .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=DescribeInstanceStatus
&RegionId=cn-hangzhou
&<公共请求参数>
```

**返回示例** 

**XML 格式**

```
<DescribeInstanceStatusResponse>
    <RequestId>6EF60BEC-0242-43AF-BB20-270359FB54A7</RequestId>
    <TotalCount>2</TotalCount>
    <PageNumber>1</PageNumber>
    <PageSize>10</PageSize>
    <InstanceStatuses>
        <InstanceStatus>
            <InstanceId>i-instance1</InstanceId>
                <Status>Running</Status>
            </InstanceStatus>
            <InstanceStatus>
                <InstanceId>i-ae4r89pp</InstanceId>
                <Status>Stopped</Status>
        </InstanceStatus>
    </InstanceStatuses>
</DescribeInstanceStatusResponse>
```

 **JSON 格式** 

```
{
"RequestId": "6EF60BEC-0242-43AF-BB20-270359FB54A7",
"TotalCount": 2,
"PageNumber": 1,
"PageSize": 10,
"InstanceStatuses": {
    "InstanceStatus": [{
        "InstanceId": "i-instance1",
            "Status": "Running"
        },
        {
            "InstanceId": "i-ae4r89pp",
            "Status": "Stopped"
        }]
    }
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问 [API 错误中心](https://error-center.alibabacloud.com/status/product/Ecs)。

|错误代码|错误信息|HTTP 状态码|说明|
|:---|:---|:-------|:-|
|InvalidRegionId.NotFound|The specified RegionId does not exist.|404|指定的 RegionId 不存在。|
|InvalidZoneId.NotFound|The ZoneId provided does not exist in our records.|404|指定的 ZoneId 不存在。|

