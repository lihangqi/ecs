# DescribePrice {#doc_api_Ecs_DescribePrice .reference}

调用DescribePrice查询云服务器ECS资源的最新价格。

## 接口说明 {#description .section}

您需要[提交工单](https://selfservice.console.aliyun.com/ticket/createIndex.htm)申请使用询价功能，否则会报错InvalidAction。

查询不同类型资源的价格时，必需参数也会相应不同。即：

-   参数 ResourceType 的值为 instance 时，您必须同时指定参数 InstanceType。
-   参数 ResourceType 的值为 disk 时，您必须同时指定参数 DataDisk.1.Category 和 DataDisk.1.Size。查询 disk 资源的价格时，只返回云盘 [按量付费](~~40653~~) 的价格，即参数 PriceUnit 只能取值为 Hour。
-   查询 bandwidth 资源的价格时, 只返回 按流量计费 （PayByTraffic）的价格。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=DescribePrice)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|RegionId|String|是|cn-hangzhou|地域 ID。您可以调用 [DescribeRegions](~~25609~~) 查看最新的阿里云地域列表。

 |
|Action|String|否|DescribePrice|系统规定参数。取值：DescribePrice

 |
|Amount|Integer|否|1|查询批量购买某种配置的云服务器 ECS 的价格。取值范围：1~1000

 默认值：1

 |
|DataDisk.1.Category|String|否|cloud\_ssd|数据盘n的云盘种类。取值范围：

 -   cloud：普通云盘
-   cloud\_efficiency：高效云盘
-   cloud\_ssd：SSD 云盘
-   ephemeral\_ssd：本地 SSD 盘
-   cloud\_essd：ESSD 云盘

 |
|DataDisk.1.Size|Integer|否|2000|数据盘的容量大小，内存单位为GiB。取值范围：

 -   cloud：5~2000
-   cloud\_efficiency：20~32768
-   cloud\_ssd：20~32768
-   cloud\_essd：20~32768
-   ephemeral\_ssd：5~800

 |
|DataDisk.2.Category|String|否|cloud\_ssd|数据盘n的云盘种类。取值范围：

 -   cloud：普通云盘
-   cloud\_efficiency：高效云盘
-   cloud\_ssd：SSD 云盘
-   ephemeral\_ssd：本地 SSD 盘
-   cloud\_essd：ESSD 云盘

 |
|DataDisk.2.Size|Integer|否|200|数据盘的容量大小，内存单位为GiB。取值范围：

 -   cloud：5~2000
-   cloud\_efficiency：20~32768
-   cloud\_ssd：20~32768
-   cloud\_essd：20~32768
-   ephemeral\_ssd：5~800

 |
|DataDisk.3.Category|String|否|cloud\_ssd|数据盘n的云盘种类。取值范围：

 -   cloud：普通云盘
-   cloud\_efficiency：高效云盘
-   cloud\_ssd：SSD 云盘
-   ephemeral\_ssd：本地 SSD 盘
-   cloud\_essd：ESSD 云盘

 |
|DataDisk.3.Size|Integer|否|2000|数据盘的容量大小，内存单位为GiB。取值范围：

 -   cloud：5~2000
-   cloud\_efficiency：20~32768
-   cloud\_ssd：20~32768
-   cloud\_essd：20~32768
-   ephemeral\_ssd：5~800

 |
|DataDisk.4.Category|String|否|cloud\_ssd|数据盘n的云盘种类。取值范围：

 -   cloud：普通云盘
-   cloud\_efficiency：高效云盘
-   cloud\_ssd：SSD 云盘
-   ephemeral\_ssd：本地 SSD 盘
-   cloud\_essd：ESSD 云盘。

 |
|DataDisk.4.Size|Integer|否|2000|数据盘的容量大小，内存单位为GiB。取值范围：

 -   cloud：5~2000
-   cloud\_efficiency：20~32768
-   cloud\_ssd：20~32768
-   cloud\_essd：20~32768
-   ephemeral\_ssd：5~800

 |
|ImageId|String|否|centos\_7\_05\_64\_20G\_alibase\_20181212.vhd|镜像 ID，表示启动实例时希望装载的运行环境。您可以调用 [DescribeImages](~~25534~~) 查询您可用的镜像资源。如果不指定，默认查询 Linux 镜像的价格。

 |
|InstanceNetworkType|String|否|vpc|实例的网络类型。取值范围：

 -   classic：实例的网络类型为经典网络（Classic）
-   vpc：实例的网络类型为专有网络（VPC）

 默认值：vpc

 |
|InstanceType|String|否|ecs.n1.tiny|实例的资源规格。更多详情，请参见 [实例规格族](~~25378~~)，也可以调用 [DescribeInstanceTypes](~~25620~~) 接口获得最新的规格表。

 |
|InternetChargeType|String|否|PayByTraffic|网络带宽计费方式。取值范围：

 -   PayByBandwidth：按固定带宽计费
-   PayByTraffic：按带宽流量计费

 默认值：PayByTraffic

 |
|InternetMaxBandwidthOut|Integer|否|5|公网出带宽最大值，单位为 Mbps （Megabit per second）。取值范围：0~100

 默认值：0

 |
|IoOptimized|String|否|none|查询的实例是否为 I/O 优化实例。取值范围：

 -   none：非 I/O 优化。
-   optimized：I/O 优化。

 InstanceType 为 [系列I](~~55263~~) 的规格时，默认值：none

 InstanceType 为非 [系列I](~~55263~~) 的规格时，默认值：optimized

 |
|Period|Integer|否|1|云服务器 ECS 的计费时长。取值范围：

 -   当参数 PriceUnit 取值为 Month 时：1~9
-   当参数 PriceUnit 取值为 Year 时：1~3
-   当参数 PriceUnit 取值为 Hour 时：1

 默认值：1

 |
|PriceUnit|String|否|Year|查询云服务器 ECS 不同计费周期的价格。取值范围：

 -   Month：按月计费的价格单位
-   Year：按年计费的价格单位
-   Hour（默认）：按小时计费的价格单位
-   Week：按周计费的价格单位

 |
|ResourceType|String|否|instance|目标资源的类型。取值范围：

 -   instance：查询 ECS 实例的最新价格列表
-   disk：查询云盘的最新价格列表
-   bandwidth：查询带宽的最新价格列表

 默认值：instance

 |
|SystemDisk.Category|String|否|cloud\_ssd|系统盘的云盘种类。InstanceType为 [已停售的实例规格](~~55263~~) 的规格且参数 IoOptimized 取值为 none 时，默认值：cloud。其余情况，默认值：cloud\_efficiency。取值范围：

 -   cloud：普通云盘
-   cloud\_efficiency：高效云盘
-   cloud\_ssd：SSD 云盘
-   ephemeral\_ssd：本地 SSD 盘
-   cloud\_essd：ESSD 云盘

 |
|SystemDisk.Size|Integer|否|80|系统盘大小，单位为GiB。取值范围：20~500

 该参数的取值必须大于或者等于max\{20, ImageSize\}。默认值：max\{40, 参数ImageId对应的镜像大小\}

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|PriceInfo| | |价格信息类型（PriceInfoType），包括价格和优惠规则。

 |
|Price| | |价格。

 |
|Currency|String|CNY|货币单位。

 |
|DetailInfos| | |价格的详细信息。

 |
|DiscountPrice|Float|655.2|折扣价。

 |
|OriginalPrice|Float|4368|原价。

 |
|Resource|String|instance|资源名称。

 |
|SubRules| | |定价规则子集。

 |
|Description|String|买满1年,立享官网价格8.5折优惠|规则子集描述。

 |
|RuleId|Long|587|规则 ID。

 |
|TradePrice|Float|3712.8|成交价。

 |
|DiscountPrice|Float|655.2|折扣

 |
|OriginalPrice|Float|4368|原价。

 |
|TradePrice|Float|3712.8|最终价，为原价减去折扣

 |
|Rules| | |活动规则。

 |
|Description|String|买满1年,立享官网价格8.5折优惠|活动规则描述

 |
|RuleId|Long|587|活动 ID

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=DescribePrice
&RegionId=cn-hangzhou
&InstanceType=ecs.n1.tiny
&<公共请求参数>
```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribePriceResponse>
  <RequestId>04F0F334-1335-436C-A1D7-6C044FE73368</RequestId>
  <PriceInfo>
    <Price>
      <Currency>CNY</Currency>
      <DiscountPrice>655.2</DiscountPrice>
      <OriginalPrice>4368</OriginalPrice>
      <TradePrice>3712.8</TradePrice>
    </Price>
    <Rules>
      <Rule>
        <Description>买满1年,立享官网价格8.5折优惠</Description>
        <RuleId>ONE_YEAR_85_PERCENT</RuleId>
      </Rule>
    </Rules>
  </PriceInfo>
</DescribePriceResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"PriceInfo":{
		"Price":{
			"DiscountPrice":655.2,
			"OriginalPrice":4368,
			"TradePrice":3712.8,
			"Currency":"CNY"
		},
		"Rules":{
			"Rule":[
				{
					"Description":"买满1年,立享官网价格8.5折优惠",
					"Code":"ONE_YEAR_85_PERCENT"
				}
			]
		}
	},
	"RequestId":"04F0F334-1335-436C-A1D7-6C044FE73368"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InvalidInstanceType.ValueUnauthorized|The specified InstanceType is not authorized.|指定的实例规格未授权使用。|
|400|InvalidInstanceType.ValueNotSupported|The specified InstanceType does not exist or beyond the permitted range.|指定的实例规格不支持。|
|400|InvalidInternetChargeType.ValueNotSupported|The specified InternetChargeType is not valid.|指定的实例升降配规格不存在。|
|400|InvalidInternetMaxBandwidthOut.ValueNotSupported|The specified parameter "InternetMaxBandwidthOut" is not valid.|指定的 InternetMaxBandwidthOut 参数不合法。|
|400|InvalidSystemDiskCategory.ValueNotSupported|The specified parameter "SystemDisk.Category" is not valid.|指定的 SystemDisk.Category 不合法。|
|400|InvalidDataDiskSize.ValueNotSupported|The specified DataDisk.n.Size beyond the permitted range, or the capacity of snapshot exceeds the size limit of the specified disk category.|指定的数据盘大小已超过最大允许值。|
|400|InvalidDataDiskCategory.ValueNotSupported|The specified parameter "DataDisk.n.Category" is not valid.|指定的参数 DataDisk.n.Category 不合法。|
|400|InvalidParameter.Conflict|The specified image does not support the specified instance type.|指定的镜像不能用于指定的实例规格。|
|403|ImageNotSubscribed|The specified image has not be subscribed.|指定的镜像未在镜像市场订阅。|
|403|OperationDenied|The specified Image is disabled or is deleted.|指定的镜像被禁用或被删除。|
|403|InvalidSystemDiskCategory.ValueUnauthorized|The disk category is not authorized.|该磁盘类别未经授权。|
|403|InstanceDiskCategoryLimitExceed|The total size of specified disk category in an instance exceeds.|磁盘种类总容量超过实例限制。|
|403|ImageRemovedInMarket|The specified market image is not available, Or the specified user defined image includes product code because it is based on an image subscribed from marketplace, and that image in marketplace includeing exact the same product code has been removed.|指定的云市场镜像不可用。|
|403|QuotaExceed.PortableCloudDisk|The quota of portable cloud disk exceeds.|可卸载磁盘数量已达上限。|
|500|InternalError|The request processing has failed due to some unknown error.|内部错误，请重试。如果多次尝试失败，请提交工单|
|400|InvalidNetworkType.Mismatch|Specified parameter "InternetChargeType" conflict with instance network type.|实例的网络类型不支持指定的网络计费方式。|
|400|InvalidDiskCategory.Mismatch|The specified disk categories' combination is not supported.|不支持的磁盘种类搭配。|
|403|Forbbiden|User not authorized to operate on the specified resource.|用户未被授权操作指定的资源。|
|404|InvalidImageId.NotFound|The specified ImageId does not exist.|指定的镜像在该用户账号下不存在，请您检查镜像id是否正确。|
|403|InstanceDiskNumLimitExceed|The number of specified disk in an instance exceeds.|实例下磁盘数目超过限制。|
|403|IoOptimized.NotSupported|The specified image is not support IoOptimized Instance.|指定的镜像不支持 I/O 优化型实例。|
|403|ImageNotSupportInstanceType|The specified image don't support the InstanceType instance.|指定的镜像不支持此类实例规格。|
|400|InvalidIoOptimizedValue.ValueNotSupported|IoOptimized value not supported.|不支持指定的 I/O 优化值。|
|404|IoOptimized.NotSupported|The specified instancetype is not support IoOptimized instance|指定的实例规格不支持 I/O 优化。|
|403|InvalidDiskSize.TooSmall|Specified disk size is less than the size of snapshot|指定的磁盘容量小于快照容量。|
|403|OperationDenied|The type of the disk does not support the operation|此磁盘种类不支持指定的操作。|
|404|InvalidInstanceChargeType.NotFound|The InstanceChargeType does not exist in our records|指定的实例升降配规格不存在。|
|400|InvalidPeriod|The specified period is not valid.|指定的时段不合法。|
|403|InvalidDiskCategory.Mismatch|The specified disk categories combination is not supported.|不支持的磁盘种类搭配。|
|400|InvalidDataDiskCategory.ValueNotSupported|The specified parameter " DataDisk.n.Category " is not valid.|指定的磁盘类型无效。|
|400|InvalidSystemDiskCategory.ValueNotSupported|The specified parameter " SystemDisk.Category " is not valid.|指定的磁盘类型无效。|
|403|InvalidDiskCategory.NotSupported|The specified disk category is not support the specified instance type.|指定的磁盘种类不支持该实例规格。|
|403|InvalidDiskCategory.NotSupported|The upgrade operation of instance does not support this category of disk.|实例挂载的磁盘限制了升级规格操作。|
|400|InstanceDiskCategoryLimitExceed|The specified DataDisk.n.Size beyond the permitted range, or the capacity of snapshot exceeds the size limit of the specified disk category.|指定的数据盘大小已超过最大允许值。|
|404|DependencyViolation.IoOptimized|The specified instancetype must be IoOptimized instance.|指定的实例规格必须为 I/O 优化实例，请您检查实例规格是否正确。|
|404|InvalidSystemDiskSize.LessThanImageSize|The specified parameter SystemDisk.Size is less than the image size.|指定的参数 SytemDisk.Size 小于镜像文件大小数值。|
|404|InvalidSystemDiskSize.LessThanMinSize|The specified parameter SystemDisk.Size is less than the minimum size.|指定的 SystemDisk.Size 低于最小值。|
|404|InvalidSystemDiskSize.MoreThanMaxSize|The specified parameter SystemDisk.Size is more than the maximum size|指定的 SystemDisk.Size 超过最大值。|
|400|InvalidInternetMaxBandwidthOut.ValueNotSupported|The specified vm bandwidth is not valid.|指定的虚拟机带宽无效。|
|400|InvalidSystemDiskCategory.ValueNotSupported|The specified parameter SystemDisk.Category is not valid.|指定的 SystemDisk.Category 不合法。|
|403|InvalidParameter.ResourceOwnerAccount|ResourceOwnerAccount is Invalid.|指定的 ResourceOwnerAccount 不合法。|
|403|RegionUnauthorized|There is no authority to create instance in the specified region.|用户未被授权在指定的地域创建实例。|
|404|InvalidSystemDiskSize.ValueNotSupported|The specified parameter SystemDisk.Size is invalid.|指定的 SystemDisk.Size 不合法。|
|400|InvalidInternetMaxBandwidthOut.ValueNotSupported|The specified parameter Bandwidth is not valid.|指定的 Bandwidth 不合法。|
|400|InstanceDiskNumber.LimitExceed|The total number of specified disk in an instance exceeds.|实例下磁盘数目超过限制。|
|400|InvalidDiskCategory.ValueNotSupported|The specified parameter "DiskCategory" is not valid.|参数 DiskCategory 不合法。|
|403|OperationDenied|The resource is out of usage.|该实例不在运行状态，请您启动实例或检查操作是否合理。|
|400|InvalidInternetMaxBandwidthOut.ValueNotSupported|%s|InternetMaxBandwidthOut参数设置无效。|
|400|InvalidDataDiskCategory.ValueNotSupported|%s|参数不支持。|
|400|InvalidSystemDiskCategory.ValueNotSupported|%s|参数不支持。|
|400|InvalidParameter.Conflict|%s|参数冲突。|
|400|InvalidInternetChargeType.ValueNotSupported|%s|参数不支持。|
|400|InvalidInstanceType.ValueNotSupported|%s|实例类型属性不正确。|
|403|InstanceType.Offline|%s|实例规格不能使用。|
|400|RegionUnauthorized|%s|指定地域不支持。|
|500|InternalError|%s|内部错误。|
|400|InvalidSystemDiskSize.ValueNotSupported|%s|参数不支持。|
|400|InvalidDataDiskSize.ValueNotSupported|%s|参数不支持。|
|404|InvalidInstanceType.Missing|The InstanceType parameter that is mandatory for processing the request is not provided.|InstanceType参数为必填参数|
|404|InvalidNetworkType.ValueNotSupported|The specified parameter NetworkType is not valid.|指定的网络类型不合法|
|404|InvalidDiskCategory.Missing|The DataDisk.1.Category parameter that is mandatory for processing the request is not provided.|没有指定数据盘类型。|
|400|InvalidSystemDiskCategory.ValueNotSupported|The specified parameter "SystemDisk.Size" is not valid.|指定的 SystemDisk.Size 不合法。|
|400|InvalidSystemDiskSize.LessThanImageSize|The specified parameter "SystemDisk.Size" is less than the image size.|指定的 SystemDisk.Size 小于镜像大小。|
|400|InvalidDataDiskCategory.ValueNotSupported|The specified parameter "DataDisk.Category" is not valid.|指定的参数 DataDisk.Category 不合法。|
|400|InvalidDataDiskSize.ValueNotSupported|The specified parameter "DataDisk.Size" is not valid.|指定的参数 DataDisk.Size 不合法。|
|400|Throttling|Request was denied due to request throttling.|当前的操作太过频繁，请稍后重试。|
|400|PriceNotFound|The price of your queried resource is not available now, please try other resources.|暂无法查询该资源的价格，请稍后重试。|
|400|InvalidResourceType.ValueNotSupported|The specified parameter ResourceType is not valid.|指定的资源类型不合法。|
|400|InvalidPriceUnit.ValueNotSupported|The specified parameter PriceUnit is not valid.|指定的单价不合法。|
|403|OperationDenied|The specified parameter InstanceNetworkType is not authorized.|用户未被授权指定的实例网络类型。|
|400|InvalidInternetMaxBandwidthOut.ValueNotSupported|The specified parameter InternetMaxBandwidthOut is not valid.|指定的公网出带宽最大值不合法。|
|403|InvalidAmount.Malformed|The specified parameter Amount is not valid.|参数 Amount 格式错误。|
|400|EncryptedOption.Conflict|%s|参数不支持（加密盘）。|
|404|Invalid.InstanceId.NotFound|The Instance provided does not exist.|指定的实例不存在。|
|403|InvalidDiskSize.TooSmall|Specified system disk size is less than the size of image|系统盘容量不能低于镜像大小。|
|404|InvalidMarketImage.NotFound|The specified marketplace image does not exist, please change the imageId and try again.|云市场不存在指定的镜像。|
|400|IncorrectImageStatus|The specified marketplace image is not available.|指定的市场镜像不可用。|
|403|InvalidChargeType.MarketImage|The specified chargeType of marketplace image is invalid|该市场镜像的付费类型不支持。|
|403|InvalidDiskIds.NotFound|Some of the specified disks do not exist.|指定的磁盘不存在。|
|403|InvalidDiskCategory.NotSupported|The specified disk category is not supported.|该云盘类型不支持。|
|403|PrePaidInstance.Expired|The prePaid instance has expired.|预付费实例已到期。|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

