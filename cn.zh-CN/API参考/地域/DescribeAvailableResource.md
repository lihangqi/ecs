# DescribeAvailableResource {#doc_api_Ecs_DescribeAvailableResource .reference}

调用DescribeAvailableResource查询某一可用区的资源列表。例如，您可以在某一可用区创建实例（RunInstances）或者修改实例规格（ModifyInstanceSpec）时查询该可用区的资源列表。

## 接口说明 {#description .section}

调用该接口时，您需要注意：

-   不指定参数`ZoneId`时，返回该地域（`RegionId`）下所有可用区的符合其他条件的目标资源。
-   您可以通过指定参数`DestinationResource`查询不同类型的资源列表，再指定其他参数细化资源条件。参数`DestinationResource`的各个可选取值有不同的逻辑与要求。在下列两个顺序列表中，排在越后面的参数其逻辑与苛刻程度越高。
    -   顺序：（`Zone`）\> `IoOptimized` \> `InstanceType` \> `SystemDisk` \> `DataDisk`
    -   取值示例：
        -   若参数`DestinationResource`取值为`SystemDisk`，则必须传入参数`IoOptimized`和`InstanceType`。
        -   若参数`DestinationResource`取值为`InstanceType`，则必须传入参数`IoOptimized`。
        -   若参数`DestinationResource`取值为`DataDisk`，则必须传入参数`IoOptimized`、`InstanceType`和`SystemDiskCategory`。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=DescribeAvailableResource&type=RPC&version=2014-05-26)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|DestinationResource|String|是|InstanceType|要查询的资源类型。取值范围：

 -   Zone：可用区
-   IoOptimized：I/O优化
-   InstanceType：实例规格
-   SystemDisk：系统盘
-   DataDisk：数据盘
-   Network：网络类型

 |
|RegionId|String|是|cn-hangzhou|目标地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。

 |
|Action|String|否|DescribeAvailableResource|系统规定参数。对于您自行拼凑HTTP/HTTPS URL发起的API请求，`Action`为必选参数。取值：DescribeAvailableResource

 |
|Cores|Integer|否|2|实例规格的vCPU内核数目。取值参见[实例规格族](~~25378~~)。

 当DestinationResource取值为InstanceType时，Cores才为有效参数。

 |
|DataDiskCategory|String|否|cloud\_ssd|数据盘类型。取值范围：

 -   cloud：普通云盘
-   cloud\_efficiency：高效云盘
-   cloud\_ssd：SSD云盘
-   ephemeral\_ssd：本地SSD盘
-   cloud\_essd：ESSD云盘

 |
|DedicatedHostId|String|否|dh-dedicatedhostid|专有宿主机ID。

 |
|InstanceChargeType|String|否|PrePaid|资源的计费方式。更多详情，请参见[计费概述](~~25398~~)。取值范围：

 -   PrePaid：包年包月
-   PostPaid：按量付费

 默认值：PostPaid。

 |
|InstanceType|String|否|ecs.g5.large|实例规格。更多详情，请参见[实例规格族](~~25378~~)，也可以调用[DescribeInstanceTypes](~~25620~~)接口获得最新的规格表。

 当参数DestinationResource取值为SystemDisk或者DataDisk时，InstanceType为必需参数。

 |
|IoOptimized|String|否|optimized|是否为I/O优化实例。取值范围：

 -   none：非I/O优化实例
-   optimized：I/O优化实例

 若参数DestinationResource取值为SystemDisk、InstanceType或者DataDisk时，参数IoOptimized不是必需参数。

 默认值：optimized。

 |
|Memory|Float|否|8.0|实例规格的内存大小，单位为GiB。取值参见[实例规格族](~~25378~~)。

 当DestinationResource取值为InstanceType时，Memory才为有效参数。

 |
|NetworkCategory|String|否|vpc|网络类型。取值范围：

 -   vpc：专有网络
-   classic：经典网络

 |
|ResourceType|String|否|Instance|资源类型。取值范围：

 -   instance：ECS实例
-   disk：云盘
-   reservedinstance：预留实例券
-   ddh：专有宿主机

 |
|SpotStrategy|String|否|NoSpot|按量付费实例的竞价策略。取值范围：

 -   NoSpot：正常按量付费实例
-   SpotWithPriceLimit：设置上限价格的抢占式实例
-   SpotAsPriceGo：系统自动出价，最高按量付费价格

 默认值：NoSpot。

 当参数InstanceChargeType取值为PostPaid时，参数SpotStrategy才有效。

 |
|SystemDiskCategory|String|否|cloud\_ssd|系统盘类型。取值范围：

 -   cloud：普通云盘
-   cloud\_efficiency：高效云盘
-   cloud\_ssd：SSD云盘
-   ephemeral\_ssd：本地SSD盘
-   cloud\_essd：ESSD云盘

 若参数DestinationResource取值为SystemDisk、InstanceType或者DataDisk时，参数SystemDiskCategory不是必需参数。

 默认值：cloud\_efficiency。

 |
|ZoneId|String|否|cn-hangzhou-e|可用区ID。

 默认值：无，表示随机分配当前地域下的可用区。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|AvailableZones| | |数据中心信息组成的集合。

 |
|AvailableResources| | |可供创建的具体资源组成的数组。

 |
|SupportedResources| | |支持的可供创建的具体资源组成的数组。

 |
|Max|Integer|2|资源规格的最大值，该参数值为空时将不返回。

 |
|Min|Integer|1|资源规格的最小值，该参数值为空时将不返回。

 |
|Status|String|Available|资源类型。可能值：

 -   Available：资源充足
-   SoldOut：资源已售罄

 |
|StatusCategory|String|WithStock|根据库存详细分类资源类别。可能值：

 -   WithStock：库存充足
-   ClosedWithStock：库存接近水位低线
-   WithoutStock：库存告罄

 |
|Unit|String|null|资源规格单位，该参数值为空时将不返回。

 |
|Value|String|ecs.d1ne.xlarge|资源值。

 |
|Type|String|InstanceType|资源类型。可能值：

 -   Zone：可用区
-   IoOptimized：I/O优化
-   InstanceType：实例规格
-   SystemDisk：系统盘
-   DataDisk：数据盘
-   Network：网络类型

 |
|RegionId|String|cn-hangzhou|地域ID。

 |
|Status|String|Available|资源类型。可能值：

 -   Available：资源充足
-   SoldOut：资源已售罄

 |
|StatusCategory|String|WithStock|根据库存情况分类资源类别。可能值：

 -   WithStock：库存充足
-   ClosedWithStock：库存供应保障能力低，请优先选用WithStock状态的产品规格
-   WithoutStock：库存告罄

 |
|ZoneId|String|cn-hangzhou-e|可用区ID。

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=DescribeAvailableResource
&DestinationResource=InstanceType
&RegionId=cn-hangzhou
&InstanceChargeType=PrePaid
&SpotStrategy=NoSpot
&ZoneId=cn-hangzhou-e
&IoOptimized=optimized
&DedicatedHostId=dh-dedicatedhostid
&InstanceType="ecs.g5.large"
&SystemDiskCategory=cloud_ssd
&DataDiskCategory=cloud_ssd
&NetworkCategory=vpc
&Cores=2
&Memory=8.0
&ResourceType=Instance
&<公共请求参数>
```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeAvailableResourceResponse>
	  <RequestId>5272B7D8-F366-4781-AF7B-63E735FBC09A</RequestId>
	  <AvailableZones>
		    <AvailableZone>
			      <Status>Available</Status>
			      <RegionId>cn-hangzhou</RegionId>
			      <ZoneId>cn-hangzhou-h</ZoneId>
		    </AvailableZone>
		    <AvailableZone>
			      <Status>Available</Status>
			      <RegionId>cn-hangzhou</RegionId>
			      <ZoneId>cn-hangzhou-g</ZoneId>
		    </AvailableZone>
		    <AvailableZone>
			      <Status>Available</Status>
			      <RegionId>cn-hangzhou</RegionId>
			      <ZoneId>cn-hangzhou-f</ZoneId>
		    </AvailableZone>
		    <AvailableZone>
			      <Status>Available</Status>
			      <RegionId>cn-hangzhou</RegionId>
			      <ZoneId>cn-hangzhou-b</ZoneId>
		    </AvailableZone>
		    <AvailableZone>
			      <Status>Available</Status>
			      <RegionId>cn-hangzhou</RegionId>
			      <ZoneId>cn-hangzhou-e</ZoneId>
		    </AvailableZone>
	  </AvailableZones>
</DescribeAvailableResourceResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"5272B7D8-F366-4781-AF7B-63E735FBC09A",
	"AvailableZones":{
		"AvailableZone":[
			{
				"Status":"Available",
				"RegionId":"cn-hangzhou",
				"ZoneId":"cn-hangzhou-h"
			},
			{
				"Status":"Available",
				"RegionId":"cn-hangzhou",
				"ZoneId":"cn-hangzhou-g"
			},
			{
				"Status":"Available",
				"RegionId":"cn-hangzhou",
				"ZoneId":"cn-hangzhou-f"
			},
			{
				"Status":"Available",
				"RegionId":"cn-hangzhou",
				"ZoneId":"cn-hangzhou-b"
			},
			{
				"Status":"Available",
				"RegionId":"cn-hangzhou",
				"ZoneId":"cn-hangzhou-e"
			}
		]
	}
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|404|Invalid.RegionId|The specified RegionId does not exist.|地域参数不合法。|
|404|Unavailable.Regions|The available regions does not exists|地域参数不合法。|
|400|Invalid.InstanceChargeType|The specified InstanceChargeType is not valid.|付费类型参数不合法。|
|400|Invalid.Param|The input parameter DestinationResource that is mandatory for processing this request is not supplied.|目标资源类型不合法。|
|404|Invalid.ResourceType|The ResourceType provided does not exist in our records.|资源类型不合法。|
|404|Invalid.DestinationResource|The specified DestinationResource is not valid.|目标资源类型无效。|
|404|Invalid.IoOptimized|The specified IoOptimized is not valid.|I/O优化参数不合法。|
|404|Invalid.NetworkCategory|The specified NetworkCategory is not valid.|网络类型参数不合法。|
|404|Invalid.SpotStrategy|The specified SpotStrategy is not valid.|竞价策略参数不合法。|
|403|InvalidDedicatedHostId.NotFound|The specified DedicatedHostId does not exist.|指定的专有宿主机ID不存在。|
|404|Invalid.NetworkType|The specified NetworkType is not valid.|网络类型参数不合法。|
|404|InvalidResourceId.NotFound|The specified ResourceId is not found in our records|实例规格及cpu/内存参数冲突。|
|403|InvalidParam.TypeAndCpuMem.Conflict|The specified 'InstanceType' and 'Cores','Memory' are not blank at the same time.|cpu参数无效。|
|403|InvalidParam.Cores|The specified parameter 'Cores' should be empty|内存参数无效。|
|403|InvalidParam.Memory|The specified parameter 'Memory' should be empty|资源在当前地域不存在或者已释放。|
|400|InvalidRegionId.MalFormed|The specified parameter RegionId is not valid.|指定的 RegionId 不合法。|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

