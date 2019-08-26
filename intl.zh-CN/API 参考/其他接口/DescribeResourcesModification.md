# DescribeResourcesModification {#DescribeResourcesModification .reference}

查询升级和降配实例规格或者系统盘时，某一可用区的可用资源信息。

## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：DescribeResourcesModification|
|RegionId|String|是|目标地域 ID。您可以调用 [DescribeRegions](intl.zh-CN/API 参考/地域/DescribeRegions.md#) 查看最新的阿里云地域列表。|
|ResourceId|String|是|资源 ID。例如，当待查询的资源为实例时，可以理解为 InstanceId。|
|DestinationResource|String|是|目标资源类型。取值范围：-   InstanceType：实例规格
-   SystemDisk：系统盘类型

|
|MigrateAcrossZone|Boolean|否|是否支持跨集群升级实例规格。取值范围：-   True：支持
-   False：不支持

默认值：False当参数 `MigrateAcrossZone` 取值为 `True` 时，一旦您根据返回信息升级了云服务器，请留意以下注意事项：-   经典网络类型实例：
    -   对于 [已停售的实例规格](https://www.alibabacloud.com/help/faq-detail/55263.htm)，非 I/O 优化实例变配到 I/O 优化实例时，实例私网 IP 地址、磁盘设备名和软件授权码会发生变化。对于 Linux 实例，普通云盘（`cloud`）会被识别为 `xvda` 或者 `xvdb` 等，高效云盘（`cloud_efficiency`） 和 SSD 云盘（`cloud_ssd`）会被识别为 `vda` 或者 `vdb` 等。
    -   对于[正常售卖的实例规格族](../../../../intl.zh-CN/产品简介/实例规格族.md#)，实例的私网 IP 地址会发生变化。
-   专有网络 VPC 类型实例：

对于 [已停售的实例规格](https://www.alibabacloud.com/help/faq-detail/55263.htm)，非 I/O 优化实例变配到 I/O 优化实例时，云服务器磁盘设备名和软件授权码会发生变化。Linux 实例的普通云盘（`cloud`）会被识别为 `xvda` 或者 `xvdb`等，高效云盘（`cloud_efficiency`） 和 SSD 云盘（`cloud_ssd`）会被识别为 `vda` 或者 `vdb` 等。


|
|OperationType|String|否|更改配置的操作类型。取值范围：-   Upgrade：升级资源
-   Downgrade：降级资源
-   RenewDowngrade：续费降配
-   RenewModify：过期实例到续费变配

默认值：Upgrade|
|InstanceType|String|否|实例规格。更多详情，请参阅 [实例规格族](../../../../intl.zh-CN/产品简介/实例规格族.md#)，也可以调用 [DescribeInstanceTypes](intl.zh-CN/API 参考/实例/DescribeInstanceTypes.md#)接口获得最新的规格表。当参数 `DestinationResource` 取值为 `SystemDisk` 时，必须同时指定该参数 `InstanceType`。|

## 返回参数 {#ResponseParameter .section}

|名称|类型|描述|
|:-|:-|:-|
|AvailableZones|Array of [`AvailableZones`](#AvailableZoneType)|数据中心信息 AvailableZoneType 组成的集合|

**AvailableZoneType** 

|名称|类型|描述|
|:-|:-|:-|
|RegionId|String|地域 ID|
|ZoneId|String|可用区 ID|
|Status|String|资源状态，返回值：-   Available：资源充足
-   SoldOut：资源已售罄

|
|AvailableResources|Array of [`AvailableResourcesType`](#AvailableResourcesType)|可供创建的具体资源组成的数组|

**AvailableResourcesType** 

|名称|类型|描述|
|:-|:-|:-|
|Type|String|资源类型。返回值：-   Zone：可用区
-   IoOptimized：I/O 优化
-   InstanceType：实例规格
-   SystemDisk：系统盘类型
-   DataDisk：数据盘类型
-   Network：网络类型

|
|SupportedResources|Array of [`SupportedResourcesType`](#SupportedResourcesType)|支持的可供创建的具体资源组成的数组|

**SupportedResourcesType** 

|名称|类型|描述|
|:-|:-|:-|
|Value|String|资源值|
|Status|String|资源状态，返回值：-   Available：资源充足
-   SoldOut：资源已售罄

|
|Min|Integer|资源规格的最小值，该参数值为空时不返回|
|Max|Integer|资源规格的最大值，该参数值为空时不返回|
|Unit|Integer|资源规格单位，该参数值为空时不返回|

## 示例 { .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=DescribeResourcesModification
&DestinationResource=InstanceType
&RegionId=cn-hangzhou
&<公共请求参数>
```

**返回示例** 

**XML 格式**

```
<DescribeResourcesModificationResponse>
    <AvailableZones>
        <AvailableZone>
            <ZoneId>cn-hangzhou-d</ZoneId>
            <RegionId>cn-hangzhou</RegionId>
            <Status>Available</Status>
            <AvailableResources>
                <AvailableResource>
                    <Type>instanceType</Type>
                    <SupportedResources>
                        <SupportedResource>
                            <Value>ecs.d1ne.xlarge</Value>
                            <Status>Available</Status>
                        </SupportedResource>
                         <SupportedResource>
                            <Value>ecs.d1ne.2xlarge</Value>
                            <Status>Available</Status>
                        </SupportedResource>
                    </SupportedResources>
                </AvailableResource>
            </AvailableResources>
        </AvailableZone>
        <AvailableZone>
            <ZoneId>cn-hangzhou-e</ZoneId>
            <RegionId>cn-hangzhou</RegionId>
            <Status>Available</Status>
            <AvailableResources>
                <AvailableResource>
                    <Type>instanceType</Type>
                    <SupportedResources>
                        <SupportedResource>
                            <Value>ecs.d1ne.xlarge</Value>
                            <Status>Available</Status>
                        </SupportedResource>
                         <SupportedResource>
                            <Value>ecs.d1ne.2xlarge</Value>
                            <Status>Available</Status>
                        </SupportedResource>
                    </SupportedResources>
                </AvailableResource>
            </AvailableResources>
        </AvailableZone>
    </AvailableZones>
    <RequestId>6DB97BCC-92BA-424D-A7C8-3F6486612BAE</RequestId>
</DescribeResourcesModificationResponse>
```

 **JSON 格式** 

```
{
    "RequestId": "D0233A65-7F00-4B50-8023-101427229D4F",
    "AvailableZones": {
        "AvailableZone": [
            {
                "Status": "available",
                "RegionId": "cn-hangzhou",
                "AvailableResources": {
                    "AvailableResource": [
                        {
                            "Type": "instanceType",
                            "SupportedResources": {
                                "SupportedResource": [
                                    {
                                        "Status": "available",
                                        "Value": "ecs.sn1ne.xlarge"
                                    },
                                    {
                                        "Status": "available",
                                        "Value": "ecs.sn2ne.xlarge"
                                    }
                                ]
                            }
                        }
                    ]
                },
                "ZoneId": "cn-hangzhou-e",
            }
        ]
    }
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问 [API 错误中心](https://error-center.alibabacloud.com/status/product/Ecs)。

|错误代码|错误信息|HTTP 状态码|说明|
|:---|:---|:-------|:-|
|Invalid.Param|The input parameter DestinationResource that is mandatory for processing this request is not supplied.|400|您必须指定必需参数 `DestinationResource`。|
|Unavailable.Regions|The specified region is limited to access.|404|指定的 `RegionId` 没有权限。|
|InvalidRegionId.NotFound|The specified RegionId does not exist.|404|指定的 `RegionId` 不存在。|

