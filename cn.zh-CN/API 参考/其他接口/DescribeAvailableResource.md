# DescribeAvailableResource {#DescribeAvailableResource .reference}

查询某一可用区的资源列表。例如，您可以在某一可用区创建实例（[RunInstances](intl.zh-CN/API 参考/实例/RunInstances.md#)）时查询该可用区的资源列表。

## 描述 {#section_av1_byg_ydb .section}

调用该接口时，您需要注意：

-   不指定参数 `ZoneId` 时，返回该地域（`RegionId`）下所有可用区的符合其他条件的目标资源。
-   您可以通过指定参数 `DestinationResource` 查询不同类型的资源列表，再指定其他参数细化资源条件。参数 `DestinationResource` 的各个可选取值有不同的逻辑与（&&）要求。在下列两个顺序列表中，排在越后面的参数其逻辑与（&&）苛刻程度越高。
    -   顺序：（`Zone`）\> `IoOptimized` \> `InstanceType` \> `SystemDisk` \> `DataDisk`
    -   **取值示例**：
        -   若参数 `DestinationResource` 取值为 `SystemDisk`，则必须传入参数 `IoOptimized` 和 `InstanceType`。
        -   若参数 `DestinationResource` 取值为 `InstanceType`，则必须传入参数 `IoOptimized`。
        -   若参数 `DestinationResource` 取值为 `DataDisk`，则必须传入参数 `IoOptimized`、`InstanceType` 和 `SystemDiskCategory`。

## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：DescribeAvailableResource|
|RegionId|String|是|目标地域 ID。您可以调用[DescribeRegions](../intl.zh-CN/API 参考/地域/DescribeRegions.md#)查看最新的阿里云地域列表。|
|DestinationResource|String|是|要查询的资源类型。取值范围：-   Zone：可用区
-   IoOptimized：I/O 优化
-   InstanceType：实例规格
-   SystemDisk：系统盘
-   DataDisk：数据盘
-   Network：网络类型

|
|ZoneId|String|否|可用区 ID，不传入参数 `ZoneId` 则表示随机分配当前地域下的可用区。|
|InstanceChargeType|String|否|资源的计费方式。更多详情，请参阅 [计费概述](../intl.zh-CN/产品定价/计费概述.md#)。取值范围：-   PrePaid：预付费（包年包月）
-   PostPaid：按量付费

默认值：PostPaid|
|SpotStrategy|String|否|按量付费实例的竞价策略。取值范围：-   NoSpot：正常按量付费实例
-   SpotWithPriceLimit：设置上限价格的抢占式实例
-   SpotAsPriceGo：系统自动出价，最高按量付费价格

默认值：NoSpot 当参数 `InstanceChargeType` 取值为 `PostPaid` 时，参数 `SpotStrategy` 才有效。|
|IoOptimized|String|否|是否为 I/O 优化实例。取值范围：-   none：非 I/O 优化实例
-   optimized：I/O 优化实例

当参数 `DestinationResource` 取值为 `InstanceType`、`SystemDisk` 或者 `DataDisk`时，`IoOptimized` 为必需参数。|
|InstanceType|String|否|实例规格。更多详情，请参阅 [实例规格族](../intl.zh-CN/产品简介/实例规格族.md#)，也可以调用 [DescribeInstanceTypes](intl.zh-CN/API 参考/实例/DescribeInstanceTypes.md#)接口获得最新的规格表。当参数 `DestinationResource` 取值为 `SystemDisk` 或者 `DataDisk` 时，`InstanceType` 为必需参数。|
|Cores|Integer|否|实例规格的vCPU内核数目。取值参阅 [实例规格族](../intl.zh-CN/产品简介/实例规格族.md#)。当 `DestinationResource=InstanceType` 参数有效，`Cores` 才为有效参数。|
|Memory|Integer|否|实例规格的内存大小，单位为GiB。取值参阅 [实例规格族](../intl.zh-CN/产品简介/实例规格族.md#)。当 `DestinationResource=InstanceType`，`Memory` 才为有效参数。|
|SystemDiskCategory|String|否|系统盘类型。取值范围：-   cloud：普通云盘
-   cloud\_efficiency：高效云盘
-   cloud\_ssd：SSD 云盘
-   ephemeral\_ssd：本地 SSD 盘

|
|DataDiskCategory|String|否|数据盘类型。取值范围：-   cloud：普通云盘
-   cloud\_efficiency：高效云盘
-   cloud\_ssd：SSD 云盘
-   ephemeral\_ssd：本地 SSD 盘

|
|NetworkCategory|String|否|网络类型。取值范围：-   vpc：专有网络
-   classic：经典网络

|

## 返回参数 {#ResponseParameter .section}

|名称|类型|描述|
|:-|:-|:-|
|AvailableZones|Array of [AvailableZoneType](#AvailableZoneType)|数据中心信息组成的集合|

**AvailableZoneType**

|名称|类型|描述|
|:-|:-|:-|
|RegionId|String|地域 ID|
|ZoneId|String|可用区 ID|
|Status|String|资源状态。返回值：-   Available：资源充足
-   SoldOut：资源已售罄

|
|AvailableResources|Array of [AvailableResourcesType](#AvailableResourcesType)|可供创建的具体资源组成的数组|

**AvailableResourcesType**

|名称|类型|描述|
|:-|:-|:-|
|Type|String|资源类型。返回值：-   Zone：可用区
-   IoOptimized：I/O 优化
-   InstanceType：实例规格
-   SystemDisk：系统盘
-   DataDisk：数据盘
-   Network：网络类型

|
|SupportedResources|Array of [\\SupportedResourcesType](#SupportedResourcesType)|支持的可供创建的具体资源组成的数组|

**SupportedResourcesType**

|名称|类型|描述|
|:-|:-|:-|
|Value|String|资源值|
|Status|String|资源类型。返回值：-   Available：资源充足
-   SoldOut：资源已售罄

|
|Min|Integer|资源规格的最小值，该参数值为空时将不返回|
|Max|Integer|资源规格的最大值，该参数值为空时将不返回|
|Unit|Integer|资源规格单位，该参数值为空时将不返回|

## 示例 { .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=DescribeAvailableResource
&RegionId=cn-hangzhou
&DestinationResource=InstanceType
&<公共请求参数>
```

**返回示例** 

**XML 格式**

```
<DescribeAvailableResourceResponse>
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
</DescribeAvailableResourceResponse>
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

以下为本接口特有的错误码。更多错误码，请访问 [API错误中心](https://error-center.alibabacloud.com/status/product/Ecs)。

|错误代码|错误信息|HTTP 状态码|说明|
|:---|:---|:-------|:-|
|Invalid.Param|The input parameter DestinationResource that is mandatory for processing this request is not supplied.|400|您必须指定必需参数 `DestinationResource`。|
|Invalid.InstanceChargeType|The specified InstanceChargeType is not valid.|400|指定的 `InstanceChargeType` 不存在。|
|InvalidParam.Cores|The specified parameter 'Cores' should be empty|403|当 `DestinationResource=InstanceType`，`Cores` 才为有效参数。|
|InvalidParam.Memory|The specified parameter 'Memory' should be empty|403|当 `DestinationResource=InstanceType`，`Memory` 才为有效参数。|
|InvalidParam.TypeAndCpuMem.Conflict|The specified 'InstanceType' and 'Cores','Memory' are not blank at the same time.|403|当 `DestinationResource=InstanceType`，`Cores` 和 `Memory` 才为有效参数。|
|Invalid.IoOptimized|The specified IoOptimized is not valid.|404|I/O 优化参数 `IoOptimized` 不合法。|
|Invalid.DestinationResource|The specified DestinationResource is not valid|404|指定的 `DestinationResource` 不存在。|
|Invalid.SpotStrategy|The specified SpotStrategy is not valid.|404|指定的 `SpotStrategy` 不存在。|
|Invalid.NetworkCategory|The specified NetworkCategory is not valid.|404|网络类型参数不合法。|
|InvalidRegionId.NotFound|The specified RegionId does not exist.|404|指定的 `RegionId` 不存在。|
|Unavailable.Regions|The available regions does not exists.|404|您暂时无法使用指定的 `RegionId` 里的资源。|

