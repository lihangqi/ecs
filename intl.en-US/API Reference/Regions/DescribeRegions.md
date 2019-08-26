# DescribeRegions {#doc_api_1006043 .reference}

Views the Alibaba Cloud regions that you can use.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=DescribeRegions) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|AcceptLanguage|String|No|zh-CN| The set of supported natural languages. For more information, see [RFC 7231](https://tools.ietf.org/html/rfc7231). Valid values:

 -   zh-CN
-   en-US
-   ja

 Default value: null.

 |
|Action|String|No|DescribeRegions| The operation that you want to perform. Set the value to DescribeRegions.

 |
|InstanceChargeType|String|No|PrePaid| The billing method for the instance. For more information, see [Pricing overview](~~25398~~). Valid values:

 -   PrePaid: Subscription. You must ensure the balance of your account or credit balance can cover the cost of the subscription. Otherwise, the InvalidPayMethod error code will be returned.
-   PostPaid: Pay-As-You-Go. This is the default value.

 |
|ResourceType|String|No|Instance| The type of the resource.

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|Regions| | | A array that consists of region information.

 |
|└LocalName|String|China \(Qingdao\)| The name of the region.

 |
|└RegionEndpoint|String|ecs.aliyuncs.com| The endpoint of the region.

 |
|└RegionId|String|cn-shanghai-et2-bo1| The ID of the region.

 |
|└Status|String|available| |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=DescribeRegions
&InstanceChargeType=PrePaid
&ResourceType=Instance
&AcceptLanguage=null
&<Common request parameters>
```

Successful response examples

`XML` format

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

`JSON` format

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

## Error codes {#section_5pe_0l0_srn .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|404|InvalidAcceptLanguage.NotFound|Only Chinese \(zh-CN\), English \(en-US\), and Japanese \(ja\) are allowed.|The error message returned when the specified language is not supported.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

