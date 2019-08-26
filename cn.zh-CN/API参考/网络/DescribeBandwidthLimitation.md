# DescribeBandwidthLimitation {#doc_api_Ecs_DescribeBandwidthLimitation .reference}

调用DescribeBandwidthLimitation查询带宽资源列表。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=DescribeBandwidthLimitation&type=RPC&version=2014-05-26)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|RegionId|String|是|cn-hangzhou|目标地域 ID。您可以调用 [DescribeRegions](~~25609~~) 查看最新的阿里云地域列表。

 |
|Action|String|否|DescribeBandwidthLimitation|系统规定参数。取值：DescribeBandwidthLimitation

 |
|InstanceChargeType|String|否|PrePaid|实例的计费方式。更多详情，请参见 [计费概述](~~25398~~)。取值范围：

 -   PrePaid：预付费（包年包月）
-   PostPaid：按量付费

 默认值：PostPaid

 |
|InstanceType|String|否|ecs.g5.large|实例规格。更多详情，请参见 [实例规格族](~~25378~~)，也可以调用 [DescribeInstanceTypes](~~25620~~) 接口获得最新的规格表。

 |
|OperationType|String|否|Upgrade|查询不同操作方式的带宽规格限制。取值范围：

 -   Upgrade：升级带宽
-   Downgrade：降级带宽
-   Create：新建

 默认值：Create

 |
|OwnerAccount|String|否|ECSforCloud@Alibaba.com|RAM 用户的账号登录名称。

 |
|ResourceId|String|否|s-946ntx4xx|资源 ID。当您将参数 OperationType 设置为 Upgrade 或者 Downgrade 时，参数 ResourceId 为必需参数。

 |
|SpotStrategy|String|否|NoSpot|按量付费实例的q抢占策略。取值范围：

 -   NoSpot：正常按量付费实例
-   SpotWithPriceLimit：设置上限价格的抢占式实例
-   SpotAsPriceGo：系统自动出价，最高按量付费价格

 默认值：NoSpot

 当参数 InstanceChargeType 取值为 PostPaid 时，参数 SpotStrategy 才有效。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|Bandwidths| | |数据中心信息组成的集合

 |
|InternetChargeType|String|PayByTraffic|带宽的计费方式。取值范围：

 -   PayByBandwidth：按固定带宽计费
-   PayByTraffic：按流量计费

 |
|Max|Integer|100|带宽最大值，该参数值为空时不返回

 |
|Min|Integer|0|带宽最小值，该参数值为空时不返回

 |
|Unit|String|Mbps|带宽单位，该参数值为空时不返回

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=DescribeBandwidthLimitation
&RegionId=cn-hangzhou
&<公共请求参数>
```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
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

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"675B6D89-A3EB-4987-BAF3-610591E0D019",
	" Bandwidths":{
		" Bandwidth":[
			{
				"Max":100,
				"InternetChargeType":"PayByTraffic",
				"Unit":"Mbps",
				"Min":0
			},
			{
				"Max":100,
				"InternetChargeType":"PayByTraffic",
				"Unit":"Mbps",
				"Min":0
			}
		]
	}
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|Invalid.InstanceChargeType|The specified InstanceChargeType is not valid.|付费类型参数不合法。|
|404|Invalid.NetworkCategory|The specified NetworkCategory is not valid.|网络类型参数不合法。|
|404|Invalid.SpotStrategy|The specified SpotStrategy is not valid.|竞价策略参数不合法。|
|404|Invalid.IoOptimized|The specified IoOptimized is not valid.|I/O优化参数不合法。|
|404|Invalid.ResourceId|The specified ResourceId is not valid.|资源在当前地域不存在或者已释放。|
|404|Invalid.InstancePayType|The specified InstancePayType is not valid.|付费类型参数不合法。|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

