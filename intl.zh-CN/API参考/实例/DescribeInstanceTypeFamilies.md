# DescribeInstanceTypeFamilies {#doc_api_1161577 .reference}

查询云服务器 ECS 提供的实例规格族资源。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=DescribeInstanceTypeFamilies)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|RegionId|String|是|cn-hangzhou|地域 ID。您可以调用 [DescribeRegions](~~25609~~) 查看最新的阿里云地域列表。

 |
|Action|String|否|DescribeInstanceTypeFamilies|接口名称。取值：**DescribeInstanceTypeFamilies**

 |
|Generation|String|否|ecs-3|实例规格族的系列信息。更多详情，请参阅 [实例规格族](~~25378~~)。取值范围：

 -   ecs-1：系列 I 实例规格，上线时间较早，性价比高。
-   ecs-2：系列 II 实例规格族，第二次软硬件升级，实例性能增强。
-   ecs-3：系列 III 实例规格族，实例性能优良，能承载不同业务需求，响应更快。
-   ecs-4：系列 IV 实例规格族，最新规格族，具有强大的场景适应性，能承载海量热门业务需求，延迟更低。

 |
|OwnerAccount|String|否|ECSforCloud@Alibaba.com|RAM用户的账号登录名称。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|InstanceTypeFamilies| | |由实例规格族 **InstanceTypeFamilyItemType** 组成的集合

 |
|└Generation|String|ecs-1|实例规格族所属代数

 |
|└InstanceTypeFamilyId|String|ecs.g5|实例规格族 ID

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。无论调用接口成功与否，我们都会返回请求 ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

https://ecs.aliyuncs.com/?Action=DescribeInstanceTypeFamilies
&RegionId=cn-hangzhou
&Generation=ecs-3
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeInstanceTypeFamiliesResponse>
  <InstanceTypeFamilies>
    <InstanceTypeFamily>
      <InstanceTypeFamilyId>ecs.t1</InstanceTypeFamilyId>
      <Generation>ecs-1</Generation>
    </InstanceTypeFamily>
    <InstanceTypeFamily>
      <InstanceTypeFamilyId>ecs.s2</InstanceTypeFamilyId>
      <Generation>ecs-1</Generation>
    </InstanceTypeFamily>
    <InstanceTypeFamily>
      <InstanceTypeFamilyId>ecs.s3</InstanceTypeFamilyId>
      <Generation>ecs-1</Generation>
    </InstanceTypeFamily>
  </InstanceTypeFamilies>
  <RequestId>6B187E0A-C075-4D08-8B6F-6213950E8733</RequestId>
</DescribeInstanceTypeFamiliesResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"InstanceTypeFamilies":{
		"InstanceTypeFamily":[
			{
				"InstanceTypeFamilyId":"ecs.t1",
				"Generation":"ecs-1"
			},
			{
				"InstanceTypeFamilyId":"ecs.s2",
				"Generation":"ecs-1"
			},
			{
				"InstanceTypeFamilyId":"ecs.s3",
				"Generation":"ecs-1"
			}
		]
	},
	"RequestId":"6B187E0A-C075-4D08-8B6F-6213950E8733"
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/Ecs)

