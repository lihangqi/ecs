# DescribeZones {#doc_api_Ecs_DescribeZones .reference}

查询一个阿里云地域下的可用区。

## 接口说明 {#description .section}

DescribeZones仅查询阿里云提供的可用区列表并返回少量库存信息。如果您需要查询具体可用区下可购买的实例规格和云盘规格，推荐您使用[DescribeAvailableResource](~~66186~~)。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=DescribeZones)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|RegionId|String|是|cn-hangzhou|可用区所在的地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。

 |
|AcceptLanguage|String|否|zh-CN|根据汉语、英语和日语筛选返回结果。更多详情，请参见[RFC7231](https://tools.ietf.org/html/rfc7231)。取值范围：

 -   zh-CN
-   en-US
-   ja

 默认值：zh-CN。

 |
|Action|String|否|DescribeZones|系统规定参数。对于您自行拼凑HTTP/HTTPS URL发起的API请求，`Action`为必选参数。取值：DescribeZones

 |
|InstanceChargeType|String|否|PostPaid|可用区里支持的资源计费方式。更多详情，请参见[计费概述](~~25398~~)。取值范围：

 -   PrePaid：预付费（包年包月）
-   PostPaid（默认）：按量付费

 |
|SpotStrategy|String|否|NoSpot|按量付费实例的竞价策略。当InstanceChargeType为PostPaid时，您可以传入该参数。更多详情，请参见[抢占式实例](~~52088~~)。取值范围:

 -   NoSpot（默认）：正常按量付费实例
-   SpotWithPriceLimit：设置上限价格的抢占式实例
-   SpotAsPriceGo：系统自动出价，最高按量付费价格

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。

 |
|Zones| | |数据中心信息ZoneType组成的集合。

 |
|└AvailableDedicatedHostTypes| |计算型|支持的专有宿主机规格，参数数据类型为List

 |
|└AvailableDiskCategories| |cloud|支持的磁盘种类集合，参数数据类型为List

 |
|└AvailableInstanceTypes| |c5|允许创建的实例规格类型，参数数据类型为List

 |
|└AvailableResourceCreation| |DedicatedHost|允许创建的资源类型集合，参数数据类型为List

 |
|└AvailableResources| | |可供创建的具体资源，AvailableResourcesType组成的数组

 |
|└DataDiskCategories| |cloud\_ssd|数据盘类型，参数数据类型为List。取值范围：

 -   cloud：普通云盘
-   cloud\_efficiency：高效云盘
-   cloud\_ssd：SSD云盘
-   cloud\_essd：ESSD云盘
-   ephemeral\_ssd：本地SSD盘

 |
|└InstanceGenerations| |I|实例规格族代数，参数数据类型为List

 |
|└InstanceTypeFamilies| |\["d1", "d1ne"\]|由实例规格族InstanceTypeFamilyItemType组成的集合，参数数据类型为List

 |
|└InstanceTypes| |\["ecs.g5.large"\]|实例规格，参数数据类型为List

 |
|└IoOptimized|Boolean|true|是否为I/O优化实例。取值范围：

 -   none：非I/O优化
-   optimized：I/O优化

 InstanceType为[已停售的实例规格](~~55263~~)的规格默认值：none

 InstanceType为非系列I的规格默认值：optimized

 |
|└NetworkTypes| |VPC|网络类型，参数数据类型为List。取值范围：

 -   VPC：专有网络VPC
-   Classic：经典网络

 |
|└SystemDiskCategories| |cloud\_ssd|系统盘类型，参数数据类型为List。取值范围：

 -   cloud：普通云盘
-   cloud\_efficiency：高效云盘
-   cloud\_ssd：SSD云盘
-   cloud\_essd：ESSD云盘
-   ephemeral\_ssd：本地SSD盘

 |
|└AvailableVolumeCategories| |san\_ssd|可以使用的共享存储类型，参数数据类型为List

 |
|└DedicatedHostGenerations| |I|专有宿主机代数，参数数据类型为List

 |
|└LocalName|String|华东 1 可用区G|可用区本地语言名

 |
|└ZoneId|String|cn-hangzhou-b|可用区ID

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=DescribeZones
&RegionId=cn-hangzhou
&InstanceChargeType=PostPaid
&SpotStrategy=NoSpot
&<公共请求参数>
```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeZonesResponse>
  <Zones>
    <Zone>
      <AvailableResourceCreation>
        <ResourceTypes>Instance</ResourceTypes>
        <ResourceTypes>Disk</ResourceTypes>
      </AvailableResourceCreation>
      <LocalName/>
      <ZoneId>cn-hangzhou-d</ZoneId>
      <AvailableDiskCategories>
        <DiskCategories>cloud</DiskCategories>
      </AvailableDiskCategories>
    </Zone>
    <Zone>
      <AvailableResourceCreation>
        <ResourceTypes>Instance</ResourceTypes>
        <ResourceTypes>Disk</ResourceTypes>
      </AvailableResourceCreation>
      <LocalName/>
      <ZoneId>cn-hangzhou-b</ZoneId>
      <AvailableDiskCategories>
        <DiskCategories>cloud</DiskCategories>
      </AvailableDiskCategories>
    </Zone>
  </Zones>
  <RequestId>6DB97BCC-92BA-424D-A7C8-3F6486612BAE</RequestId>
</DescribeZonesResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"A347EF0E-BBCC-4EFA-BD79-27AA3ACFD1BF",
	"Zones":{
		"Zone":[
			{
				"AvailableResourceCreation":{
					"ResourceTypes":[
						"Instance",
						"Disk"
					]
				},
				"ZoneId":"cn-hangzhou-d",
				"LocalName":"",
				"AvailableDiskCategories":{
					"DiskCategories":[
						"cloud"
					]
				}
			},
			{
				"AvailableResourceCreation":{
					"ResourceTypes":[
						"Instance",
						"Disk"
					]
				},
				"ZoneId":"cn-hangzhou-b",
				"LocalName":"",
				"AvailableDiskCategories":{
					"DiskCategories":[
						"cloud"
					]
				}
			}
		]
	}
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|404|InvalidRegionId.NotFound|The specified RegionId does not exist.|指定的 RegionId 不存在，请您检查此产品在该地域是否可用。|
|404|InvalidInstanceChargeType.NotFound|The InstanceChargeType does not exist in our records|指定的实例升降配规格不存在。|
|400|InvalidSpotStrategy|The specified SpotStrategy is not valid.|竞价实例不支持转换|
|404|InvalidAcceptLanguage.NotFound|Only Chinese \(zh-CN\), English \(en-US\), and Japanese \(ja\) are allowed.|不支持指定的语言。|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Ecs)

