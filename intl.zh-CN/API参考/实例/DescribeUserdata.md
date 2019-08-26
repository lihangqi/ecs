# DescribeUserdata {#DescribeUserdata .reference}

查询一台 ECS 实例的 [自定义数据](../../../../intl.zh-CN/用户指南/实例/实例自定义/元数据/实例自定义数据.md#)。

## 描述 {#section_jwv_kws_xdb .section}

-   返回的实例自定义数据将以 Base64 编码的方式显示。
-   如果实例不存在自定义数据，则返回空值。

## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：DescribeUserdata|
|RegionId|String|是|实例所属的地域 ID。您可以调用 [DescribeRegions](intl.zh-CN/API参考/地域/DescribeRegions.md#) 查看最新的阿里云地域列表。|
|InstanceId|String|是|要查询的实例 ID。|

## 返回参数 {#ResponseParameter .section}

|名称|类型|描述|
|:-|:-|:-|
|UserData|String|实例的自定义数据，并以 Base64 编码方式的方式显示|
|InstanceId|String|实例Id|
|RegionId|String|地域 ID|

## 示例 { .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action= DescribeUserdata
&RegionId=cn-shenzhen
&InstanceId=i-instance1
&<公共请求参数>

```

```
https://ecs.example.com/?Action= DescribeUserdata
&RegionId=cn-shenzhen
&InstanceId=i-instance1
&<公共请求参数>

```

**返回示例** 

**XML 格式**

```
<DescribeUserdataResponse>
    <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
    <UserData>userdata1</UserData>
    <InstanceId> i-instance1</InstanceId>
    <RegionId> cn-shenzhen </RegionId>
</DescribeUserdataResponse>
```

 **JSON 格式** 

```
{
    "RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E"
    " UserData ": " userdata1"
    " InstanceId ": " i-instance1"
    " RegionId": "cn-shenzhen"
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问 [API 错误中心](https://error-center.alibabacloud.com/status/product/Ecs)。

|错误代码|错误信息|HTTP 状态码|说明|
|:---|:---|:-------|:-|
|InvalidRegionId.NotFound|The specified RegionId does not exist.|404|指定的 `RegionId` 不存在。|
|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|404|指定的 `InstanceId` 不存在。|

