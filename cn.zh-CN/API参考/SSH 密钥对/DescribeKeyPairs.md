# DescribeKeyPairs {#doc_api_Ecs_DescribeKeyPairs .reference}

查询一个或多个密钥对。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=DescribeKeyPairs)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|RegionId|String|是|cn-hangzhou|密钥对所在的地域ID。您可以调用 [DescribeRegions](~~25609~~) 查看最新的阿里云地域列表。

 |
|Action|String|否|DescribeKeyPairs|系统规定参数。取值：DescribeKeyPairs

 |
|KeyPairFingerPrint|String|否|XXXXXXXXXX|密钥对的指纹。根据RFC4716定义的公钥指纹格式，采用MD5信息摘要算法。更多详情，请参阅 [RFC4716](https://tools.ietf.org/html/rfc4716)。

 |
|KeyPairName|String|否|\*Finance\*|密钥对名称。支持正则表达式模糊搜索，使用\*匹配子表达式，示例：

 -   `*SshKey`：查询以SshKey结尾的密钥对名称，包括SshKey。
-   `SshKey*`：查询以SshKey开头的密钥对名称，包括SshKey。
-   `*SshKey*`：查询名称中间有SshKey的密钥对，包括SshKey。
-   `SshKey`：精确匹配SshKey。

 |
|PageNumber|Integer|否|1|密钥对列表的页码。起始值：1

 默认值：1

 |
|PageSize|Integer|否|10|分页查询时设置的每页行数。最大值：50

 默认值：10

 |
|ResourceGroupId|String|否|rg-resourcegroupid1|密钥对所在的企业资源组ID。

 |
|Tag.N.Key|String|否|FinanceDept|密钥对的标签键。N 的取值范围：1~20。一旦传入该值，则不允许为空字符串。最多支持 64 个字符，不能以 aliyun 和 acs: 开头，不能包含 http:// 或者 https:// 。

 |
|Tag.N.Value|String|否|FinanceDept.Joshua|密钥对的标签值。N 的取值范围：1~20。一旦传入该值，可以为空字符串。最多支持 128 个字符，不能以 aliyun 和 acs: 开头，不能包含 http:// 或者 https:// 。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|KeyPairs| | |密钥对信息集合。

 |
|└KeyPairFingerPrint|String|xxxxxxxxxx|密钥对的指纹。

 |
|└KeyPairName|String|FinanceJoshuaV27|密钥对的名称。

 |
|└ResourceGroupId|String|rg-resourcegroupid1|资源组ID。

 |
|└Tags| | |密钥对的标签。

 |
|└TagKey|String|FinanceDept|密钥对的标签键。

 |
|└TagValue|String|FinanceDept.Joshua|密钥对的标签值。

 |
|PageNumber|Integer|1|当前页码。

 |
|PageSize|Integer|10|每页行数。

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。无论调用接口成功与否，我们都会返回请求 ID。

 |
|TotalCount|Integer|1|密钥对的总数。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

https://ecs.aliyuncs.com/?Action=DescribeKeyPairs
&RegionId=cn-qingdao
&KeyPairFingerPrint=xxxxxxxxxx
&KeyPairName=test
&PageNumber=1
&PageSize=20
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeKeyPairsResponse>
  <PageNumber>1</PageNumber>
  <PageSize>2</PageSize>
  <TotalCount>1</TotalCount>
  <KeyPairs>
    <KeyPair>
      <KeyPairName>test</KeyPairName>
      <KeyPairFingerPrint>xxxxxxxxxx</KeyPairFingerPrint>
    </KeyPair>
  </KeyPairs>
  <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</DescribeKeyPairsResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"PageNumber":1,
	"TotalCount":1,
	"KeyPairs":{
		"KeyPair":[
			{
				"KeyPairFingerPrint":"xxxxxxxxxx",
				"KeyPairName":"test"
			}
		]
	},
	"PageSize":2,
	"RequestId":"473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E"
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/Ecs)

