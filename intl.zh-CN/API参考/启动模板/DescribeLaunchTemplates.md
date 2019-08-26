# DescribeLaunchTemplates {#doc_api_Ecs_DescribeLaunchTemplates .reference}

查询一个或多个可用的实例启动模板。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=DescribeLaunchTemplates)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|RegionId|String|是|cn-hangzhou|地域ID。您可以调用 [DescribeRegions](~~25609~~) 查看最新的阿里云地域列表。

 |
|Action|String|否|DescribeLaunchTemplates|系统规定参数。取值：DescribeLaunchTemplates

 |
|LaunchTemplateId.N|RepeatList|否|lt-m5e3ofjr1zn1aw7qdxxx|一个或多个实例启动模板ID，最多支持查询 100 个启动模板。您必须指定LaunchTemplateId或LaunchTemplateName以确定模板。

 |
|LaunchTemplateName.N|RepeatList|否|wd-1526307480xxx|一个或多个实例启动模板名称，最多支持查询 100 个启动模板。

 |
|PageNumber|Integer|否|1|实例启动模板列表的页码。起始值：1

 默认值：1

 |
|PageSize|Integer|否|10|分页查询时设置的每页行数。最大值：50

 默认值：10

 |
|TemplateResourceGroupId|String|否|rg-resourcegroupid1|启动模板所在的企业资源组 ID。

 |
|TemplateTag.N.Key|String|否|FinanceDept|启动模板的标签键。N 的取值范围：1~5。一旦传入该值，则不允许为空字符串。最多支持 64 个字符，不能以 aliyun 和 acs: 开头，不能包含 http:// 或者 https:// 。

 |
|TemplateTag.N.Value|String|否|FinanceDepltJoshua|启动模板的标签值。N 的取值范围：1~5。一旦传入该值，可以为空字符串。最多支持 128 个字符，不能以 aliyun 和 acs: 开头，不能包含 http:// 或者 https:// 。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|LaunchTemplateSets| | |实例启动模板的信息集合

 |
|└CreateTime|String|2018-05-14T14:18:00Z|实例启动模板创建时间

 |
|└CreatedBy|String|1942111349714xxx|模板的创建者

 |
|└DefaultVersionNumber|Long|1|模板默认版本号

 |
|└LatestVersionNumber|Long|1|模板最新版本号

 |
|└LaunchTemplateId|String|lt-m5e3ofjr1zn1aw7qdxxx|模板ID

 |
|└LaunchTemplateName|String|wd-1526307480xxx|模板名称

 |
|└ModifiedTime|String|2018-05-14T14:18:00Z|修改时间

 |
|└ResourceGroupId|String|rg-resourcegroupid1|启动模板所在的企业资源组 ID。

 |
|└Tags| | |启动模板的标签对属性。

 |
|└TagKey|String|FinanceDept|启动模板的标签键。

 |
|└TagValue|String|FinanceDeptJoshua|启动模板的标签值。

 |
|PageNumber|Integer|1|当前页码

 |
|PageSize|Integer|10|分页查询时设置的每页行数

 |
|RequestId|String|04F0F334-1335-436C-A1D7-6C044FExxxxx|请求 ID

 |
|TotalCount|Integer|1|实例启动模板总个数

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

https://ecs.aliyuncs.com/?Action=DescribeLaunchTemplates
&RegionId=cn-hangzhou
&TemplateTag.1.Key=FinanceDept
&TemplateTag.1.Value=FinanceDepltJoshua
&LaunchTemplateId.1=lt-m5e3ofjr1zn1aw7qdxxx
&LaunchTemplateName.1=wd-1526307480xxx
&PageNumber=1
&PageSize=10
&TemplateResourceGroupId=rg-resourcegroupid1
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeLaunchTemplatesResponse>
  <RequestId>04F0F334-1335-436C-A1D7-6C044FExxxxx</RequestId>
  <TotalCount>1</TotalCount>
  <PageNumber>1</PageNumber>
  <PageSize>10</PageSize>
  <LaunchTemplateSets>
    <LaunchTemplateSet>
      <CreateTime>2018-05-14T14:18:00Z</CreateTime>
      <ModifiedTime>2018-05-14T14:18:00Z</ModifiedTime>
      <LaunchTemplateid>lt-m5e3ofjr1zn1aw7xxxx</LaunchTemplateid>
      <LaunchTemplateName>wd-1526307480xxx</LaunchTemplateName>
      <DefaultVersionNumber>1</DefaultVersionNumber>
      <LatestVersionNumber>1</LatestVersionNumber>
      <CreatedBy>1942111349714xxx</CreatedBy>
    </LaunchTemplateSet>
  </LaunchTemplateSets>
</DescribeLaunchTemplatesResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"PageNumber":1,
	"TotalCount":1,
	"LaunchTemplateSets":{
		"LaunchTemplateSet":[
			{
				"DefaultVersionNumber":1,
				"LaunchTemplateId":"lt-m5e3ofjr1zn1aw7qdxxx",
				"LatestVersionNumber":1,
				"CreateTime":"2018-05-14T14:18:00Z",
				"CreatedBy":"1942111349714xxx",
				"ModifiedTime":"2018-05-14T14:18:00Z",
				"LaunchTemplateName":"wd-1526307480xxx"
			}
		]
	},
	"PageSize":10,
	"RequestId":"04F0F334-1335-436C-A1D7-6C044FExxxxx"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InvalidRegion.NotExist|%s|指定的Region不存在。|
|400|MissingParameter|%s|缺失必需参数。|
|400|InvalidParameter|%s|参数格式不正确。|
|403|InnerServiceFailed|%s|内部服务调用失败。|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Ecs)

