# DescribeZones {#DescribeZones .reference}

查询一个阿里云地域下的可用区。更多详情，请参阅[地域和可用区](../../../../../cn.zh-CN/通用参考/地域和可用区.md#) 。

## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：DescribeZones|
|RegionId|String|是|可用区所在的地域 ID。您可以调用[DescribeRegions](../cn.zh-CN/API 参考/地域/DescribeRegions.md#)查看最新的阿里云地域列表。|
|InstanceChargeType|String|否|可用区里支持的资源计费方式。更多详情，请参阅 [计费概述](../cn.zh-CN/产品定价/计费概述.md#)取值范围：-   PrePaid：预付费（包年包月）
-   PostPaid（默认）：按量付费

|
|SpotStrategy|String|否|按量付费实例的竞价策略。当 `InstanceChargeType` 为`PostPaid` 时，您可以传入该参数。更多详情，请参阅 [抢占式实例](../cn.zh-CN/产品简介/实例/抢占式实例.md#)。取值范围:-   NoSpot（默认）：正常按量付费实例
-   SpotWithPriceLimit：设置上限价格的抢占式实例
-   SpotAsPriceGo：系统自动出价，最高按量付费价格

|

## 返回参数 {#ResponseParameter .section}

|名称|类型|描述|
|:-|:-|:-|
|Zones|[ZoneType](cn.zh-CN/API 参考/数据类型/ZoneType.md#)|数据中心信息 `ZoneType` 组成的集合|

## 示例 { .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=DescribeZones
&RegionId=cn-hangzhou
&<公共请求参数>
```

**返回示例** 

**XML格式** 

```
<DescribeZonesResponse>
    <Zones>
        <Zone>
            <AvailableResourceCreation>
                <ResourceTypes>Instance</ResourceTypes>
                <ResourceTypes>Disk</ResourceTypes>
            </AvailableResourceCreation>
            <LocalName></LocalName>
            <ZoneId>cn-hangzhou-d</ZoneId>
            <AvailableDiskCategories>
                <DiskCategories>cloud</DiskCategories>
            </AvailableDiskCategories>
        </Zone>
        <Zone>
            <AvailableResourceCreation>
                <ResourceTypes>Instance</ResourceTypes>
                <ResourceTypes>Disk</ResourceTypes>
            </AvailableResourceCreation>
            <LocalName></LocalName>
            <ZoneId>cn-hangzhou-b</ZoneId>
            <AvailableDiskCategories>
                <DiskCategories>cloud</DiskCategories>
            </AvailableDiskCategories>
        </Zone>
    </Zones>
    <RequestId>6DB97BCC-92BA-424D-A7C8-3F6486612BAE</RequestId>
</DescribeZonesResponse>
```

**JSON格式** 

```
{
  "RequestId": "A347EF0E-BBCC-4EFA-BD79-27AA3ACFD1BF",
  "Zones": {
    "Zone": [
      {
        "AvailableDiskCategories": {
          "DiskCategories": [
            "cloud"
          ]
        },
        "AvailableResourceCreation": {
          "ResourceTypes": [
            "Instance",
            "Disk"
          ]
        },
        "LocalName": "",
        "ZoneId": "cn-hangzhou-d"
      },
      {
        "AvailableDiskCategories": {
          "DiskCategories": [
            "cloud"
          ]
        },
        "AvailableResourceCreation": {
          "ResourceTypes": [
            "Instance",
            "Disk"
          ]
        },
        "LocalName": "",
        "ZoneId": "cn-hangzhou-b"
      }
    ]
  }
}
```

## 错误码 {#ErrorCode .section}

全是公共错误码。更多错误码，请访问[API错误中心](https://error-center.aliyun.com/status/product/Ecs)。

