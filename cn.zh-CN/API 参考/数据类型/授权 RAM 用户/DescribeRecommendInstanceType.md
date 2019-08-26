# DescribeRecommendInstanceType {#DescribeRecommendInstanceType .reference}

根据一个指定的的实例规格，查找一个或多个备选的实例规格。针对已经或者即将停售的实例规格，DescribeRecommendInstanceType 会罗列出作为替补的所有实例规格。

## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：DescribeRecommendInstanceType|
|RegionId|String|是|地域 ID。您可以调用[DescribeRegions](../cn.zh-CN/API 参考/地域/DescribeRegions.md#)查看最新的阿里云地域列表。|
|InstanceType|String|是|指定的实例规格。更多规格，请参阅 [实例规格族](../cn.zh-CN/产品简介/实例规格族.md#)，也可以调用 [DescribeInstanceTypes](cn.zh-CN/API 参考/实例/DescribeInstanceTypes.md#) 获得最新的规格列表|
|NetworkType|String|是|在哪种网络类型中指定实例规格。取值范围：-   classic：经典网络。
-   vpc（默认）：专有网络 VPC。更多详情，请参阅 [什么是专有网络](../../../../../cn.zh-CN/产品简介/什么是专有网络.md#)。

|
|Scene|String|否|在哪种场景下推荐实例规格。取值范围：-   UPGRADE：升级或降低实例规格。
-   CREATE（默认）：创建实例。

|

## 返回参数 {#ResponseParameter .section}

|名称|类型|描述|
|:-|:-|:-|
|Data|Array of [RecommendInstanceType](#)|推荐的实例规格集合。|

**RecommendInstanceType**

|名称|类型|描述|
|:-|:-|:-|
|RegionNo|String|实例规格所在的地域。|
|InstanceType|Array|实例规格的详细信息。更多详情，请参阅 [InstanceType](#)。|
|Zones|Array of [Zone](#)|实例规格所在的可用区集合。|
|CommodityCode|String|实例规格的商品编码。|
|Scene|String|在哪种场景下推荐实例规格。|

**InstanceType**

|名称|类型|描述|
|:-|:-|:-|
|Generation|String|实例规格族系列。|
|InstanceTypeFamily|String|实例规格族。|
|InstanceType|String|实例规格名称。|
|SupportIoOptimized|String|实例规格是否支持 I/O 优化。|
|Cores|Integer|实例规格的 vCPU 核数。|
|Memory|Integer|实例规格的内存大小。|

**Zone**

|名称|类型|描述|
|:-|:-|:-|
|ZoneNo|String|实例规格所在的可用区名称。|
|NetworkTypes|Array of NetworkType|实例规格的网络类型集合。|

## 示例 {#Samples .section}

**请求示例** 

```
http://ecs.aliyuncs.com/?Action=DescribeRecommendInstanceType
 &NetworkType=vpc
 &RegionId=us-west-1
 &InstanceType=ecs.s1.large
 &<公共请求参数>
```

**返回示例**

**XML 格式**

```
<DescribeRecommendInstanceTypeResponse>
    <Data>
        <RecommendInstanceType>
            <CommodityCode>ecs</CommodityCode>
            <RegionNo>us-west-ot7-a01</RegionNo>
            <Scene>CREATE</Scene>
            <Zones/>
            <InstanceType>
                <Memory>8192</Memory>
                <Cores>1</Cores>
                <InstanceTypeFamily>ecs.s1</InstanceTypeFamily>
                <SupportIoOptimized>none</SupportIoOptimized>
                <Generation>ecs-1</Generation>
                <InstanceType>ecs.s1.large</InstanceType>
            </InstanceType>
        </RecommendInstanceType>
        <RecommendInstanceType>
            <CommodityCode>ecs</CommodityCode>
            <RegionNo>us-west-ot7-a01</RegionNo>
            <Scene>CREATE</Scene>
            <Zones>
                <zone>
                    <ZoneNo>us-west-1a</ZoneNo>
                    <NetworkTypes>
                        <NetworkType>vpc</NetworkType>
                    </NetworkTypes>
                </zone>
            </Zones>
            <InstanceType>
                <Memory>8192</Memory>
                <Cores>1</Cores>
                <InstanceTypeFamily>ecs.e4</InstanceTypeFamily>
                <SupportIoOptimized>optimized</SupportIoOptimized>
                <Generation>ecs-3</Generation>
                <InstanceType>ecs.e4.small</InstanceType>
            </InstanceType>
        </RecommendInstanceType>
        <RecommendInstanceType>
            <CommodityCode>ecs</CommodityCode>
            <RegionNo>us-west-ot7-a01</RegionNo>
            <Scene>CREATE</Scene>
            <Zones>
                <zone>
                    <ZoneNo>us-west-1a</ZoneNo>
                    <NetworkTypes>
                        <NetworkType>vpc</NetworkType>
                    </NetworkTypes>
                </zone>
            </Zones>
            <InstanceType>
                <Memory>8192</Memory>
                <Cores>2</Cores>
                <InstanceTypeFamily>ecs.sn2</InstanceTypeFamily>
                <SupportIoOptimized>optimized</SupportIoOptimized>
                <Generation>ecs-2</Generation>
                <InstanceType>ecs.sn2.medium</InstanceType>
            </InstanceType>
        </RecommendInstanceType>
        <RecommendInstanceType>
            <CommodityCode>ecs</CommodityCode>
            <RegionNo>us-west-ot7-a01</RegionNo>
            <Scene>CREATE</Scene>
            <Zones/>
            <InstanceType>
                <Memory>8192</Memory>
                <Cores>1</Cores>
                <InstanceTypeFamily>ecs.e3</InstanceTypeFamily>
                <SupportIoOptimized>optimized</SupportIoOptimized>
                <Generation>ecs-2</Generation>
                <InstanceType>ecs.e3.small</InstanceType>
            </InstanceType>
        </RecommendInstanceType>
    </Data>
    <RequestId>775643e7-8297-409e6-f0a252aa152d</RequestId>
</DescribeRecommendInstanceTypeResponse>
```

**JSON 格式**

```
{
    "Data":{
        "RecommendInstanceType":[
            {
                "CommodityCode":"ecs",
                "RegionNo":"us-west-ot7-a01",
                "Scene":"CREATE",
                "Zones":{
                    "zone":[

                    ]
                },
                "InstanceType":{
                    "Memory":8192,
                    "Cores":1,
                    "InstanceTypeFamily":"ecs.s1",
                    "SupportIoOptimized":"none",
                    "Generation":"ecs-1",
                    "InstanceType":"ecs.s1.large"
                }
            },
            {
                "CommodityCode":"ecs",
                "RegionNo":"us-west-ot7-a01",
                "Scene":"CREATE",
                "Zones":{
                    "zone":[
                        {
                            "ZoneNo":"us-west-1a",
                            "NetworkTypes":{
                                "NetworkType":[
                                    "vpc"
                                ]
                            }
                        }
                    ]
                },
                "InstanceType":{
                    "Memory":8192,
                    "Cores":1,
                    "InstanceTypeFamily":"ecs.e4",
                    "SupportIoOptimized":"optimized",
                    "Generation":"ecs-3",
                    "InstanceType":"ecs.e4.small"
                }
            },
            {
                "CommodityCode":"ecs",
                "RegionNo":"us-west-ot7-a01",
                "Scene":"CREATE",
                "Zones":{
                    "zone":[
                        {
                            "ZoneNo":"us-west-1a",
                            "NetworkTypes":{
                                "NetworkType":[
                                    "vpc"
                                ]
                            }
                        }
                    ]
                },
                "InstanceType":{
                    "Memory":8192,
                    "Cores":2,
                    "InstanceTypeFamily":"ecs.sn2",
                    "SupportIoOptimized":"optimized",
                    "Generation":"ecs-2",
                    "InstanceType":"ecs.sn2.medium"
                }
            },
            {
                "CommodityCode":"ecs",
                "RegionNo":"us-west-ot7-a01",
                "Scene":"CREATE",
                "Zones":{
                    "zone":[

                    ]
                },
                "InstanceType":{
                    "Memory":8192,
                    "Cores":1,
                    "InstanceTypeFamily":"ecs.e3",
                    "SupportIoOptimized":"optimized",
                    "Generation":"ecs-2",
                    "InstanceType":"ecs.e3.small"
                }
            }
        ]
    },
    "RequestId":"775643e7-8297-40ee-b9e6-f0a252aa152d"
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问[API错误中心](https://error-center.aliyun.com/status/product/Ecs)。

|错误代码|错误信息|HTTP 状态码|说明|
|:---|:---|:-------|:-|
|InvalidParameter.Scene|An input parameter 'Scene' that is mandatory for processing the request is not supplied, expect value is CREATE or UPGRADE.|400|参数 Scene 的取值无效。|
|InvalidNetworkType.ValueNotSupported|The specified parameter NetworkType is not valid.|400|指定的网络类型取值无效。|

