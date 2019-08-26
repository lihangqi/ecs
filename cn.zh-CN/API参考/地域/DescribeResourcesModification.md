# DescribeResourcesModification {#doc_api_Ecs_DescribeResourcesModification .reference}

调用DescribeResourcesModification查询升级和降配实例规格或者系统盘时，某一可用区的可用资源信息。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=DescribeResourcesModification)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|DestinationResource|String|是|InstanceType|目标资源类型。取值范围：

 -   InstanceType：实例规格
-   SystemDisk：系统盘类型

 |
|RegionId|String|是|cn-hangzhou|目标地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。

 |
|ResourceId|String|是|i-instanceid|资源ID。例如，当待查询的资源为实例时，可以理解为InstanceId。

 |
|Action|String|否|DescribeResourcesModification|系统规定参数。对于您自行拼凑HTTP/HTTPS URL发起的API请求，`Action`为必选参数。取值：DescribeResourcesModification

 |
|Cores|Integer|否|2|实例规格的vCPU内核数目。取值参见[实例规格族](~~25378~~)。当DestinationResource=InstanceType参数有效，Cores才为有效参数。

 |
|InstanceType|String|否|ecs.g5.large|实例规格。更多详情，请参见[实例规格族](~~25378~~)，也可以调用[DescribeInstanceTypes](~~25620~~) 接口获得最新的规格表。当参数DestinationResource取值为SystemDisk时，必须同时指定InstanceType参数。

 |
|Memory|Float|否|8.0|实例规格的内存大小，单位为GiB。取值参见[实例规格族](~~25378~~)。当DestinationResource=InstanceType，Memory才为有效参数。

 |
|MigrateAcrossZone|Boolean|否|true|是否支持跨集群升级实例规格。取值范围：

 -   True：支持
-   False：不支持

 默认值：False

 当参数MigrateAcrossZone取值为True时，一旦您根据返回信息升级了云服务器，请留意以下注意事项：

 -   经典网络类型实例：
    -   对于[已停售的实例规格](~~55263~~)，非I/O优化实例变配到I/O优化实例时，实例私网IP地址、磁盘设备名和软件授权码会发生变化。对于Linux实例，普通云盘（cloud）会被识别为xvda或者xvdb等，高效云盘（cloud\_efficiency）和SSD云盘（cloud\_ssd）会被识别为vda或者vdb等。
    -   对于[正常售卖的实例规格族](~~25378~~)，实例的私网IP地址会发生变化。
-   专有网络VPC类型实例：对于[已停售的实例规格](~~55263~~)，非I/O优化实例变配到I/O优化实例时，云服务器磁盘设备名和软件授权码会发生变化。Linux实例的普通云盘（cloud）会被识别为xvda或者xvdb等，高效云盘（cloud\_efficiency）和SSD云盘（cloud\_ssd）会被识别为vda或者vdb等。

 |
|OperationType|String|否|Upgrade|更改预付费（包年包月）配置的操作类型。取值范围：

 -   Upgrade：升级资源
-   Downgrade：降级资源
-   RenewDowngrade：续费降配
-   RenewModify：过期实例到续费变配

 默认值：Upgrade

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|AvailableZones| | |数据中心信息AvailableZoneType组成的集合。

 |
|AvailableResources| | |可供创建的具体资源组成的数组

 |
|SupportedResources| | |支持的可供创建的具体资源组成的数组

 |
|Max|Integer|2|资源规格的最大值，该参数值为空时不返回

 |
|Min|Integer|1|资源规格的最小值，该参数值为空时不返回

 |
|Status|String|Available|资源状态，返回值：

 -   Available：资源充足
-   SoldOut：资源已售罄

 |
|StatusCategory|String|WithStock|根据库存详细分类资源类别。目前的可能值有：

 -   WithStock：库存充足
-   ClosedWithStock：库存接近水位低线
-   WithoutStock：库存告罄

 |
|Unit|String|null|资源规格单位，该参数值为空时不返回

 |
|Value|String|ecs.sn1ne.xlarge|资源值

 |
|Type|String|InstanceType|资源类型。返回值：

 -   Zone：可用区
-   IoOptimized：I/O优化
-   InstanceType：实例规格
-   SystemDisk：系统盘类型
-   DataDisk：数据盘类型
-   Network：网络类型

 |
|RegionId|String|cn-hangzhou|地域ID

 |
|Status|String|Available|资源状态，返回值：

 -   Available：资源充足
-   SoldOut：资源已售罄

 |
|StatusCategory|String|WithStocK|根据库存详细分类资源类别。目前的可能值有：

 -   WithStock：库存充足
-   ClosedWithStock：库存接近水位低线
-   WithoutStock：库存告罄

 |
|ZoneId|String|cn-hangzhou-e|可用区ID

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=DescribeResourcesModification
&DestinationResource=InstanceType
&RegionId=cn-hangzhou
&ResourceId=i-instanceid
&MigrateAcrossZone=true
&OperationType=Upgrade
&InstanceType="ecs.g5.large"
&Cores=2
&Memory=8.0
&<公共请求参数>
```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeResourcesModificationResponse>
  <RequestId>994F2B60-B050-49E3-9283-44655FAC7A4X</RequestId>
  <AvailableZones>
    <AvailableZone>
      <Status>Available</Status>
      <RegionId>cn-hangzhou-dg-a01</RegionId>
      <AvailableResources>
        <AvailableResource>
          <Type>InstanceType</Type>
          <SupportedResources>
            <SupportedResource>
              <Status>Available</Status>
              <Value>ecs.g5.xlarge</Value>
            </SupportedResource>
            <SupportedResource>
              <Status>Available</Status>
              <Value>ecs.t5-lc1m2.large</Value>
            </SupportedResource>
            <SupportedResource>
              <Status>Available</Status>
              <Value>ecs.t5-c1m4.2xlarge</Value>
            </SupportedResource>
            <SupportedResource>
              <Status>Available</Status>
              <Value>ecs.c5.xlarge</Value>
            </SupportedResource>
            <SupportedResource>
              <Status>Available</Status>
              <Value>ecs.hfg5.large</Value>
            </SupportedResource>
            <SupportedResource>
              <Status>Available</Status>
              <Value>ecs.hfc5.3xlarge</Value>
            </SupportedResource>
            <SupportedResource>
              <Status>Available</Status>
              <Value>ecs.hfg5.4xlarge</Value>
            </SupportedResource>
            <SupportedResource>
              <Status>Available</Status>
              <Value>ecs.hfg5.6xlarge</Value>
            </SupportedResource>
            <SupportedResource>
              <Status>Available</Status>
              <Value>ecs.c5.4xlarge</Value>
            </SupportedResource>
            <SupportedResource>
              <Status>Available</Status>
              <Value>ecs.t5-c1m2.xlarge</Value>
            </SupportedResource>
            <SupportedResource>
              <Status>Available</Status>
              <Value>ecs.t5-c1m1.2xlarge</Value>
            </SupportedResource>
            <SupportedResource>
              <Status>Available</Status>
              <Value>ecs.ic5.xlarge</Value>
            </SupportedResource>
            <SupportedResource>
              <Status>Available</Status>
              <Value>ecs.t5-lc1m4.large</Value>
            </SupportedResource>
            <SupportedResource>
              <Status>Available</Status>
              <Value>ecs.hfg5.3xlarge</Value>
            </SupportedResource>
            <SupportedResource>
              <Status>Available</Status>
              <Value>ecs.t5-c1m2.4xlarge</Value>
            </SupportedResource>
            <SupportedResource>
              <Status>Available</Status>
              <Value>ecs.ic5.3xlarge</Value>
            </SupportedResource>
            <SupportedResource>
              <Status>Available</Status>
              <Value>ecs.g5.6xlarge</Value>
            </SupportedResource>
            <SupportedResource>
              <Status>Available</Status>
              <Value>ecs.ic5.large</Value>
            </SupportedResource>
            <SupportedResource>
              <Status>Available</Status>
              <Value>ecs.ic5.2xlarge</Value>
            </SupportedResource>
            <SupportedResource>
              <Status>Available</Status>
              <Value>ecs.hfc5.large</Value>
            </SupportedResource>
            <SupportedResource>
              <Status>Available</Status>
              <Value>ecs.r5.large</Value>
            </SupportedResource>
            <SupportedResource>
              <Status>Available</Status>
              <Value>ecs.g5.large</Value>
            </SupportedResource>
            <SupportedResource>
              <Status>Available</Status>
              <Value>ecs.hfg5.xlarge</Value>
            </SupportedResource>
            <SupportedResource>
              <Status>Available</Status>
              <Value>ecs.r5.4xlarge</Value>
            </SupportedResource>
            <SupportedResource>
              <Status>Available</Status>
              <Value>ecs.hfc5.xlarge</Value>
            </SupportedResource>
            <SupportedResource>
              <Status>Available</Status>
              <Value>ecs.hfc5.4xlarge</Value>
            </SupportedResource>
            <SupportedResource>
              <Status>Available</Status>
              <Value>ecs.t5-lc1m2.small</Value>
            </SupportedResource>
            <SupportedResource>
              <Status>Available</Status>
              <Value>ecs.t5-c1m1.large</Value>
            </SupportedResource>
            <SupportedResource>
              <Status>Available</Status>
              <Value>ecs.g5.2xlarge</Value>
            </SupportedResource>
            <SupportedResource>
              <Status>Available</Status>
              <Value>ecs.r5.6xlarge</Value>
            </SupportedResource>
            <SupportedResource>
              <Status>Available</Status>
              <Value>ecs.t5-c1m2.2xlarge</Value>
            </SupportedResource>
            <SupportedResource>
              <Status>Available</Status>
              <Value>ecs.g5.3xlarge</Value>
            </SupportedResource>
            <SupportedResource>
              <Status>Available</Status>
              <Value>ecs.t5-c1m1.xlarge</Value>
            </SupportedResource>
            <SupportedResource>
              <Status>Available</Status>
              <Value>ecs.hfc5.6xlarge</Value>
            </SupportedResource>
            <SupportedResource>
              <Status>Available</Status>
              <Value>ecs.t5-c1m4.xlarge</Value>
            </SupportedResource>
            <SupportedResource>
              <Status>Available</Status>
              <Value>ecs.hfg5.2xlarge</Value>
            </SupportedResource>
            <SupportedResource>
              <Status>Available</Status>
              <Value>ecs.hfc5.2xlarge</Value>
            </SupportedResource>
            <SupportedResource>
              <Status>Available</Status>
              <Value>ecs.c5.large</Value>
            </SupportedResource>
            <SupportedResource>
              <Status>Available</Status>
              <Value>ecs.c5.6xlarge</Value>
            </SupportedResource>
            <SupportedResource>
              <Status>Available</Status>
              <Value>ecs.t5-c1m4.large</Value>
            </SupportedResource>
            <SupportedResource>
              <Status>Available</Status>
              <Value>ecs.r5.2xlarge</Value>
            </SupportedResource>
            <SupportedResource>
              <Status>Available</Status>
              <Value>ecs.r5.xlarge</Value>
            </SupportedResource>
            <SupportedResource>
              <Status>Available</Status>
              <Value>ecs.c5.3xlarge</Value>
            </SupportedResource>
            <SupportedResource>
              <Status>Available</Status>
              <Value>ecs.ic5.4xlarge</Value>
            </SupportedResource>
            <SupportedResource>
              <Status>Available</Status>
              <Value>ecs.t5-lc1m1.small</Value>
            </SupportedResource>
            <SupportedResource>
              <Status>Available</Status>
              <Value>ecs.c5.2xlarge</Value>
            </SupportedResource>
            <SupportedResource>
              <Status>Available</Status>
              <Value>ecs.t5-c1m1.4xlarge</Value>
            </SupportedResource>
            <SupportedResource>
              <Status>Available</Status>
              <Value>ecs.t5-lc2m1.nano</Value>
            </SupportedResource>
            <SupportedResource>
              <Status>Available</Status>
              <Value>ecs.g5.4xlarge</Value>
            </SupportedResource>
            <SupportedResource>
              <Status>Available</Status>
              <Value>ecs.r5.3xlarge</Value>
            </SupportedResource>
            <SupportedResource>
              <Status>Available</Status>
              <Value>ecs.t5-c1m2.large</Value>
            </SupportedResource>
          </SupportedResources>
        </AvailableResource>
      </AvailableResources>
      <ZoneId>cn-hangzhou-h</ZoneId>
    </AvailableZone>
  </AvailableZones>
</DescribeResourcesModificationResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"994F2B60-B050-49E3-9283-44655FAC7A4X",
	"AvailableZones":{
		"AvailableZone":[
			{
				"Status":"Available",
				"RegionId":"cn-hangzhou-dg-a01",
				"AvailableResources":{
					"AvailableResource":[
						{
							"Type":"InstanceType",
							"SupportedResources":{
								"SupportedResource":[
									{
										"Status":"Available",
										"Value":"ecs.g5.xlarge"
									},
									{
										"Status":"Available",
										"Value":"ecs.t5-lc1m2.large"
									},
									{
										"Status":"Available",
										"Value":"ecs.t5-c1m4.2xlarge"
									},
									{
										"Status":"Available",
										"Value":"ecs.c5.xlarge"
									},
									{
										"Status":"Available",
										"Value":"ecs.hfg5.large"
									},
									{
										"Status":"Available",
										"Value":"ecs.hfc5.3xlarge"
									},
									{
										"Status":"Available",
										"Value":"ecs.hfg5.4xlarge"
									},
									{
										"Status":"Available",
										"Value":"ecs.hfg5.6xlarge"
									},
									{
										"Status":"Available",
										"Value":"ecs.c5.4xlarge"
									},
									{
										"Status":"Available",
										"Value":"ecs.t5-c1m2.xlarge"
									},
									{
										"Status":"Available",
										"Value":"ecs.t5-c1m1.2xlarge"
									},
									{
										"Status":"Available",
										"Value":"ecs.ic5.xlarge"
									},
									{
										"Status":"Available",
										"Value":"ecs.t5-lc1m4.large"
									},
									{
										"Status":"Available",
										"Value":"ecs.hfg5.3xlarge"
									},
									{
										"Status":"Available",
										"Value":"ecs.t5-c1m2.4xlarge"
									},
									{
										"Status":"Available",
										"Value":"ecs.ic5.3xlarge"
									},
									{
										"Status":"Available",
										"Value":"ecs.g5.6xlarge"
									},
									{
										"Status":"Available",
										"Value":"ecs.ic5.large"
									},
									{
										"Status":"Available",
										"Value":"ecs.ic5.2xlarge"
									},
									{
										"Status":"Available",
										"Value":"ecs.hfc5.large"
									},
									{
										"Status":"Available",
										"Value":"ecs.r5.large"
									},
									{
										"Status":"Available",
										"Value":"ecs.g5.large"
									},
									{
										"Status":"Available",
										"Value":"ecs.hfg5.xlarge"
									},
									{
										"Status":"Available",
										"Value":"ecs.r5.4xlarge"
									},
									{
										"Status":"Available",
										"Value":"ecs.hfc5.xlarge"
									},
									{
										"Status":"Available",
										"Value":"ecs.hfc5.4xlarge"
									},
									{
										"Status":"Available",
										"Value":"ecs.t5-lc1m2.small"
									},
									{
										"Status":"Available",
										"Value":"ecs.t5-c1m1.large"
									},
									{
										"Status":"Available",
										"Value":"ecs.g5.2xlarge"
									},
									{
										"Status":"Available",
										"Value":"ecs.r5.6xlarge"
									},
									{
										"Status":"Available",
										"Value":"ecs.t5-c1m2.2xlarge"
									},
									{
										"Status":"Available",
										"Value":"ecs.g5.3xlarge"
									},
									{
										"Status":"Available",
										"Value":"ecs.t5-c1m1.xlarge"
									},
									{
										"Status":"Available",
										"Value":"ecs.hfc5.6xlarge"
									},
									{
										"Status":"Available",
										"Value":"ecs.t5-c1m4.xlarge"
									},
									{
										"Status":"Available",
										"Value":"ecs.hfg5.2xlarge"
									},
									{
										"Status":"Available",
										"Value":"ecs.hfc5.2xlarge"
									},
									{
										"Status":"Available",
										"Value":"ecs.c5.large"
									},
									{
										"Status":"Available",
										"Value":"ecs.c5.6xlarge"
									},
									{
										"Status":"Available",
										"Value":"ecs.t5-c1m4.large"
									},
									{
										"Status":"Available",
										"Value":"ecs.r5.2xlarge"
									},
									{
										"Status":"Available",
										"Value":"ecs.r5.xlarge"
									},
									{
										"Status":"Available",
										"Value":"ecs.c5.3xlarge"
									},
									{
										"Status":"Available",
										"Value":"ecs.ic5.4xlarge"
									},
									{
										"Status":"Available",
										"Value":"ecs.t5-lc1m1.small"
									},
									{
										"Status":"Available",
										"Value":"ecs.c5.2xlarge"
									},
									{
										"Status":"Available",
										"Value":"ecs.t5-c1m1.4xlarge"
									},
									{
										"Status":"Available",
										"Value":"ecs.t5-lc2m1.nano"
									},
									{
										"Status":"Available",
										"Value":"ecs.g5.4xlarge"
									},
									{
										"Status":"Available",
										"Value":"ecs.r5.3xlarge"
									},
									{
										"Status":"Available",
										"Value":"ecs.t5-c1m2.large"
									}
								]
							}
						}
					]
				},
				"ZoneId":"cn-hangzhou-h"
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
|400|Invalid.OperationType|The specified operationType is not valid.|操作类型不合法。|
|400|Invalid.Param|The input parameter DestinationResource that is mandatory for processing this request is not supplied.|目标资源类型不合法。|
|404|Invalid.ResourceType|The ResourceType provided does not exist in our records.|资源类型不合法。|
|404|Invalid.DestinationResource|The specified DestinationResource is not valid.|目标资源类型无效。|
|404|Invalid.IoOptimized|The specified IoOptimized is not valid.|I/O优化参数不合法。|
|404|Invalid.NetworkCategory|The specified NetworkCategory is not valid.|网络类型参数不合法。|
|404|Invalid.SpotStrategy|The specified SpotStrategy is not valid.|竞价策略参数不合法。|
|400|Invalid.InstanceChargeType|The specified InstanceChargeType is not valid.|付费类型参数不合法。|
|404|Invalid.ResourceId|The specified ResourceId is not valid.|资源在当前地域不存在或者已释放。|
|404|Invalid.InstancePayType|The specified InstancePayType is not valid.|付费类型参数不合法。|
|404|OperationDenied|The specified operation is denied as this instanceType is not support.|实例规格不支持当前操作。|
|403|InvalidDedicatedHostId.NotFound|The specified DedicatedHostId does not exist in our records.|资源在当前地域不存在或者已释放。|
|404|InvalidInstanceId.NotFound|The specified InstanceId provided does not exist in our records.|资源在当前地域不存在或者已释放。|
|404|InvalidResourceId.NotFound|The specified ResourceId is not found in our records|实例规格及cpu/内存参数冲突。|
|403|InvalidParam.TypeAndCpuMem.Conflict|The specified 'InstanceType' and 'Cores','Memory' are not blank at the same time.|cpu参数无效。|
|403|InvalidParam.Cores|The specified parameter 'Cores' should be empty|内存参数无效。|
|403|InvalidParam.Memory|The specified parameter 'Memory' should be empty|资源在当前地域不存在或者已释放。|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

