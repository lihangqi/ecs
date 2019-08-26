# CreateAutoProvisioningGroup {#doc_api_Ecs_CreateAutoProvisioningGroup .reference}

调用CreateAutoProvisioningGroup接口创建一个弹性供应组。

弹性供应为免费功能，但是您需要为通过弹性供应组创建出的实例资源付费，详情请参见 [抢占式实例计费](~~52088~~) 和 [按量付费](~~40653~~) 。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=CreateAutoProvisioningGroup)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
| LaunchTemplateId |String|是|lt-bp1fgzds4bdogu03\*\*\*\*| 弹性供应组关联的实例启动模板的ID，您可以调用 [DescribeLaunchTemplates](~~73759~~) 查询可用的实例启动模板。

 一个弹性供应组只能关联一个实例启动模板，但是可以通过 **LaunchTemplateConfig** 配置多个扩展启动模板。

 |
| RegionId |String|是|cn-hangzhou| 弹性供应组所在地域的ID，您可以调用 [DescribeRegions](~~25609~~) 查看最新的阿里云地域列表。

 |
| TotalTargetCapacity |String|是|60| 弹性供应组的目标总容量，由以下三个部分组成：

 -    **PayAsYouGoTargetCapacity** 指定的按量付费实例目标容量。
-    **SpotTargetCapacity** 指定的抢占式实例目标容量。
-    **PayAsYouGoTargetCapacity** 和 **SpotTargetCapacity** 之外的差额容量。

 |
| Action |String|否|CreateAutoProvisioningGroup| 系统规定参数，取值： **CreateAutoProvisioningGroup** 。

 |
| AutoProvisioningGroupName |String|否|apg-test| 弹性供应组的名称。长度为 2~128 个英文或中文字符。必须以大小字母或中文开头，不能以 http:// 和 https:// 开头。可以包含数字、半角冒号（:）、下划线（\_）或者连字符（-）。

 |
| AutoProvisioningGroupType |String|否|maintain| 弹性供应组的类型，可选值：

 -    **request** ：一次性，供应组仅在启动时尝试一次交付实例集群，调度失败也不再重试。
-    **maintain** ：持续保持，供应组在启动时尝试交付实例集群，并在持续监控实时容量和目标容量，未达到目标容量则尝试继续创建实例满足容量需求。

 默认值： **maintain** 。

 |
| DefaultTargetCapacityType |String|否|Spot| 指定差额容量的类型， **PayAsYouGoTargetCapacity** 和 **SpotTargetCapacity** 之和小于 **TotalTargetCapacity** 时，您可以指定补齐差额容量的实例类型。可选值：

 -    **PayAsYouGo** ：使用按量付费实例补齐差额容量。
-    **Spot** ：使用抢占式实例补齐差额容量。

 默认值： **Spot** 。

 |
| Description |String|否|test| 弹性供应组的描述信息。

 |
| ExcessCapacityTerminationPolicy |String|否|termination| 弹性供应组超过容量时，超额的抢占式实例的关停策略，可选值：

 -    **no-termination** ：超额的抢占式实例继续运行。
-    **termination** ：关停超额的抢占式实例，关停后的动作由 **SpotInstanceInterruptionBehavior** 指定。

 默认值： **no-termination** 。

 |
| LaunchTemplateConfig.N.InstanceType |String|否|ecs.g5.large| 弹性供应组第N个扩展启动模板对应的实例规格。

 |
| LaunchTemplateConfig.N.MaxPrice |Double|否|3| 弹性供应组第N个扩展启动模板对应的实例规格的价格上限。

 |
| LaunchTemplateConfig.N.Priority |Integer|否|1| 弹性供应组第N个扩展启动模板对应的实例规格的优先级，取值为0时最高。

 |
| LaunchTemplateConfig.N.VSwitchId |String|否|vsw-sn5bsitu4lfzgc5o7\*\*\*\*| 弹性供应组第N个扩展启动模板对应的虚拟交换机的ID。

 |
| LaunchTemplateConfig.N.WeightedCapacity |Double|否|2| 弹性供应组第N个扩展启动模板对应的实例规格的权重。

 权重根据指定实例规格的计算力和集群单节点最低计算力得出。权重越大，单台实例满足计算力需求的能力越大，所需的实例数量越小。

 例如，单节点最低计算力为8 vCPU、60 GiB，则8 vCPU、60 GiB的实例规格权重为1，16 vCPU、120 GiB的实例规格权重为2。

 |
| LaunchTemplateVersion |String|否|1| 弹性供应组关联的实例启动模板的版本，您可以调用 [DescribeLaunchTemplateVersions](~~73761~~) 查询可用的实例启动模板版本。

 |
| MaxSpotPrice |Float|否|2| 弹性供应组内抢占式实例的全局价格上限，同时设置 **MaxSpotPrice** 和 **LaunchTemplateConfig.N.MaxPrice** 时，以较低者为准。

 |
| PayAsYouGoAllocationStrategy |String|否|prioritized| 按量付费实例的扩容策略，可选值：

 -    **lowest-price** ：成本优化策略，选择价格最低的实例规格创建实例。
-    **prioritized** ：优先级策略，按照 **LaunchTemplateConfig.N.Priority** 设定的优先级创建实例。

 默认值： **lowest-price** 。

 |
| PayAsYouGoTargetCapacity |String|否|30| 弹性供应组内按量付费实例的目标容量。

 |
| SpotAllocationStrategy |String|否|diversified| 抢占式实例的扩容策略，可选值：

 -    **lowest-price** ：成本优化策略，选择价格最低的实例规格创建实例。
-    **diversified** ：均衡可用区分布策略，在扩展启动模板指定的可用区创建实例，保证实例集群均匀分布到所有可用区。

 默认值： **lowest-price** 。

 |
| SpotInstanceInterruptionBehavior |String|否|terminate| 抢占式实例关停后的默认动作，可选值：

 -    **stop** ：停止抢占式实例。
-    **terminate** ：释放抢占式实例。

 默认值： **stop** 。

 |
| SpotInstancePoolsToUseCount |Integer|否|2| 在 **SpotAllocationStrategy** 为 **lowest-price** 时生效，弹性供应组选择价格最低的数个实例规格创建实例。

 |
| SpotTargetCapacity |String|否|20| 弹性供应组内抢占式实例的目标容量。

 |
| TerminateInstances |Boolean|否|true| 删除弹性供应组时是否释放组内实例，可选值：

 -    **true** ：释放组内实例。
-    **false** ：保留组内实例。

 默认值： **false** 。

 |
| TerminateInstancesWithExpiration |Boolean|否|true| 弹性供应组到期时的关停策略，可选值：

 -    **true** ：关停组内抢占式实例，关停后的动作由 **SpotInstanceInterruptionBehavior** 指定。
-    **false** ：组内抢占式实例继续运行。

 默认值： **false** 。

 |
| ValidFrom |String|否|2019-04-01T15:10:20Z| 弹性供应组的启动时间，和 **ValidUntil** 结合确定有效时段。

 默认为立即生效。

 |
| ValidUntil |String|否|2019-06-01T15:10:20Z| 弹性供应组的结束时间，和 **ValidFrom** 结合确定有效时段。

 默认为无限期。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|AutoProvisioningGroupId|String|apg-sn54avj8htgvtyh8\*\*\*\*| 弹性供应组的ID。

 |
|RequestId|String|745CEC9F-0DD7-4451-9FE7-8B752F39\*\*\*\*| 请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://ecs.aliyuncs.com/?Action=CreateAutoProvisioningGroup
&LaunchTemplateId=lt-bp1fgzds4bdogu03****
&RegionId=cn-hangzhou
&TotalTargetCapacity=60
&<公共请求参数>

```

正常返回示例

 `XML` 格式

``` {#xml_return_success_demo}
<CreateAutoProvisioningGroupResponse>
  <CreateAutoProvisioningGroupId>apg-sn54avj8htgvtyh8****</CreateAutoProvisioningGroupId>
  <RequestId>745CEC9F-0DD7-4451-9FE7-8B752F39****</RequestId>
</CreateAutoProvisioningGroupResponse>

```

 `JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"745CEC9F-0DD7-4451-9FE7-8B752F39****",
	"CreateAutoProvisioningGroupId":"apg-sn54avj8htgvtyh8****"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|500|InternalError|The request processing has failed due to some unknown error.|内部错误，请重试。如果多次尝试失败，请提交工单|

 [查看本产品错误码](https://error-center.aliyun.com/status/product/Ecs) 

