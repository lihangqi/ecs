# DescribeRegions {#doc_api_Ecs_DescribeRegions .reference}

调用DescribeRegions查询您可以使用的阿里云地域。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=DescribeRegions&type=RPC&version=2014-05-26)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|AcceptLanguage|String|否|zh-CN|根据汉语、英语和日语筛选返回结果。更多详情，请参见[RFC7231](https://tools.ietf.org/html/rfc7231)。取值范围：

 -   zh-CN：中文
-   en-US：英文
-   ja：日文

 默认值：zh-CN。

 |
|Action|String|否|DescribeRegions|系统规定参数。取值：DescribeRegions

 |
|InstanceChargeType|String|否|PrePaid|实例的计费方式，更多详情，请参见[计费概述](~~25398~~)。取值范围：

 -   PrePaid：包年包月。此时，您必须确认自己的账号支持余额支付或者信用支付，否则将报错InvalidPayMethod。
-   PostPaid（默认）：按量付费。

 |
|ResourceType|String|否|Instance|资源类型。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|Regions| | |地域信息集合。

 |
|LocalName|String|华北 1|地域名称。

 |
|RegionEndpoint|String|ecs.aliyuncs.com|地域对应的接入地址（Endpoint）。

 |
|RegionId|String|cn-shanghai-et2-bo1|地域ID。

 |
|Status|String|available|集群是否售罄，可能值：

 -   available
-   soldOut

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=DescribeRegions
&InstanceChargeType=PrePaid
&ResourceType=Instance
&AcceptLanguage=en-US
&<公共请求参数>
```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeRegionsResponse>
      <RequestId>38EC7366-F5A9-46B1-BDB1-0FDC2E296397</RequestId>
      <Regions>
            <Region>
                  <RegionId>cn-shanghai-et2-bo1</RegionId>
                  <RegionEndpoint>ecs.aliyuncs.com</RegionEndpoint>
                  <LocalName>China (Qingdao)</LocalName>
            </Region>
            <Region>
                  <RegionId>cn-qingdao-nebula</RegionId>
                  <RegionEndpoint>ecs.cn-qingdao-nebula.aliyuncs.com</RegionEndpoint>
                  <LocalName>cn-qingdao-nebula</LocalName>
            </Region>
      </Regions>
</DescribeRegionsResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"38EC7366-F5A9-46B1-BDB1-0FDC2E296397",
	"Regions":{
		"Region":[
			{
				"RegionId":"cn-shanghai-et2-b01",
				"RegionEndpoint":"ecs.aliyuncs.com",
				"LocalName":"China (Qingdao)"
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

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|403|Unauthorized.EmptyRegion|The specified account has no access authority to any region.|当前账号未被授权访问任何地域，请您授权后再重试。|
|404|InvalidAcceptLanguage.NotFound|Only Chinese \(zh-CN\), English \(en-US\), and Japanese \(ja\) are allowed.|不支持指定的语言。|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

