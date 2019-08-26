# DescribeBandwidthLimitation {#DescribeBandwidthLimitation .reference}

查询带宽资源列表。

## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：DescribeBandwidthLimitation|
|RegionId|String|是|目标地域 ID。您可以调用 [DescribeRegions](cn.zh-CN/API 参考/地域/DescribeRegions.md#) 查看最新的阿里云地域列表。|
|InstanceType|String|是|实例规格。更多详情，请参阅 [实例规格族](../../../../cn.zh-CN/产品简介/实例规格族.md#)，也可以调用 [DescribeInstanceTypes](cn.zh-CN/API 参考/实例/DescribeInstanceTypes.md#)接口获得最新的规格表。|
|InstanceChargeType|String|否|实例的计费方式。更多详情，请参阅 [计费概述](../../../../cn.zh-CN/产品定价/计费概述.md#)。取值范围：-   PrePaid：预付费（包年包月）
-   PostPaid：按量付费

默认值：PostPaid|
|SpotStrategy|String|否|按量付费实例的q抢占策略。取值范围：-   NoSpot：正常按量付费实例
-   SpotWithPriceLimit：设置上限价格的抢占式实例
-   SpotAsPriceGo：系统自动出价，最高按量付费价格

默认值：NoSpot 当参数 `InstanceChargeType` 取值为 `PostPaid` 时，参数 `SpotStrategy` 才有效。|
|OperationType|String|否|查询不同操作方式的带宽规格限制。取值范围：-   Upgrade：升级带宽
-   Downgrade：降级带宽
-   Create：新建

默认值：Create|
|ResourceId|String|否|资源 ID。当您将参数 `OperationType` 设置为 `Upgrade` 或者 `Downgrade` 时，参数 `ResourceId` 为必需参数。|

## 返回参数 {#ResponseParameter .section}

|名称|类型|描述|
|:-|:-|:-|
|Bandwidths|Array of [BandwidthType](#BandwidthType)|数据中心信息组成的集合|

 **BandwidthType** 

|名称|类型|描述|
|:-|:-|:-|
|InternetChargeType|String|带宽的计费方式。取值范围-   PayByBandwidth：按固定带宽计费
-   PayByTraffic：按流量计费

|
|Min|Integer|带宽最小值，该参数值为空时不返回|
|Max|Integer|带宽最大值，该参数值为空时不返回|
|Unit|Integer|带宽单位，该参数值为空时不返回|

## 示例 { .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=DescribeBandwidthLimitation
&RegionId=cn-hangzhou
&<公共请求参数>
```

**返回示例** 

**XML 格式**

```
<DescribeBandwidthLimitationResponse>
    <Bandwidths>
          <Bandwidth>
            <InternetChargeType>PayByTraffic</InternetChargeType>
            <Max>100</Max>
            <Min>0</Min>
            <Unit>Mbps</Unit>
        </Bandwidth>
          <Bandwidth>
            <InternetChargeType>PayByTraffic</InternetChargeType>
            <Max>100</Max>
            <Min>0</Min>
            <Unit>Mbps</Unit>
        </Bandwidth>
     </Bandwidths>
    <RequestId>675B6D89-A3EB-4987-BAF3-610591E0D019</RequestId>
</DescribeBandwidthLimitationResponse>
```

 **JSON 格式** 

```
{
    " Bandwidths": {
        " Bandwidth": [
        {
            "InternetChargeType": "PayByTraffic",
            "Max": 100,
            "Min": 0,
            "Unit": "Mbps"
        },
        {
            "InternetChargeType": "PayByTraffic",
            "Max": 100,
            "Min": 0,
            "Unit": "Mbps"
        }]
    },
    "RequestId": "675B6D89-A3EB-4987-BAF3-610591E0D019",
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问 [API 错误中心](https://error-center.aliyun.com/status/product/Ecs)。

|错误代码|错误信息|HTTP 状态码|说明|
|:---|:---|:-------|:-|
|Invalid.InstanceChargeType|The specified InstanceChargeType is not valid.|400|指定的 `InstanceChargeType`不存在。|
|InvalidRegionId.NotFound|The specified RegionId does not exist.|404|指定的 `RegionId` 不存在。|
|Unavailable.Regions|The available regions does not exists.|404|指定的 `RegionId` 没有权限。|

