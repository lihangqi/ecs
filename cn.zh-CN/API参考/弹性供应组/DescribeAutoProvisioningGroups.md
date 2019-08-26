# DescribeAutoProvisioningGroups {#doc_api_Ecs_DescribeAutoProvisioningGroups .reference}

调用DescribeAutoProvisioningGroups接口查询弹性供应组。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=DescribeAutoProvisioningGroups)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|RegionId|String|是|cn-hangzhou| 弹性供应组所在地域的ID。

 |
|Action|String|否|DescribeAutoProvisioningGroups| 系统规定参数，取值：**DescribeAutoProvisioningGroups**。

 |
|AutoProvisioningGroupId.N|RepeatList|否|apg-sn54avj8htgvtyh8\*\*\*\*| 弹性供应组的ID。

 |
|AutoProvisioningGroupName|String|否|test| 弹性供应组的名称。

 |
|AutoProvisioningGroupStatus.N|RepeatList|否|active| 弹性供应组的状态，取值范围：

 -   **submitted**：完成创建，但弹性供应组尚未开始执行调度任务。
-   **active**：弹性供应组已开始执行调度任务。
-   **deleted**：弹性供应组已删除。
-   **deleted-running**：弹性供应组删除中。
-   **modifying**：弹性供应组修改中。

 |
|PageNumber|Integer|否|1| 实例状态列表的页码。起始值：**1**，默认值：**1**。

 |
|PageSize|Integer|否|10| 分页查询时设置的每页行数。最大值：**100**，默认值：**10**。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|AutoProvisioningGroups| | | 查询到的弹性供应组的信息。

 |
|└AutoProvisioningGroupId|String|apg-sn54avj8htgvtyh8\*\*\*\*| 弹性供应组的ID。

 |
|└AutoProvisioningGroupName|String|apg-test| 弹性供应组的名称。

 |
|└AutoProvisioningGroupType|String|maintain| 弹性供应组的类型，取值范围：

 -   **request**：一次性，供应组仅在启动时尝试一次交付实例集群，调度失败也不再重试。
-   **maintain**：持续保持，供应组在启动时尝试交付实例集群，并持续监控实时容量和目标容量，未达到目标容量则尝试继续创建实例满足容量需求。

 |
|└CreationTime|String|2019-04-01T15:10:20Z| 弹性供应组的创建时间。

 |
|└ExcessCapacityTerminationPolicy|String|termination| 弹性供应组超过容量时，超额的抢占式实例的关停策略，取值范围：

 -   **no-termination**：超额的抢占式实例继续运行。
-   **termination**：关停超额的抢占式实例，关停后的动作由**SpotInstanceInterruptionBehavior**指定。

 **说明：** **SpotInstanceInterruptionBehavior**在创建弹性供应组时设置，且不可修改，更多信息请参见[CreateAutoProvisioningGroup](~~122738~~)。

 |
|└LaunchTemplateConfigs| | | 弹性供应组的扩展启动模板设置。

 |
|└InstanceType|String|ecs.g5.large| 扩展启动模板对应的实例规格。

 |
|└MaxPrice|Float|3| 扩展启动模板对应实例规格的价格上限。

 |
|└Priority|Float|1| 扩展启动模板对应的实例规格的优先级，取值为**0**时最高。

 |
|└VSwitchId|String|vsw-sn5bsitu4lfzgc5o7\*\*\*\*| 扩展启动模板对应的虚拟交换机的ID。

 |
|└WeightedCapacity|Float|2| 扩展启动模板对应的实例规格的权重。

 |
|└LaunchTemplateId|String|lt-bp1fgzds4bdogu03\*\*\*\*| 弹性供应组关联的实例启动模板的ID。

 |
|└LaunchTemplateVersion|String|1| 弹性供应组关联的实例启动模板的版本。

 |
|└MaxSpotPrice|Float|2| 弹性供应组内抢占式实例的全局价格上限，同时设置**MaxSpotPrice**和**LaunchTemplateConfig.N.MaxPrice**时，以较低者为准。

 **说明：** **LaunchTemplateConfig.N.MaxPrice**在创建弹性供应组时设置，且不可修改，更多信息请参见[CreateAutoProvisioningGroup](~~122738~~)。

 |
|└PayAsYouGoOptions| | | 按量付费实例相关的策略。

 |
|└AllocationStrategy|String|prioritized| 按量付费实例的扩容策略，取值范围：

 -   **lowest-price**：成本优化策略，选择价格最低的实例规格创建实例。
-   **prioritized**：优先级策略，按照**LaunchTemplateConfig.N.Priority**设定的优先级创建实例。

 **说明：** **LaunchTemplateConfig.N.Priority**在创建弹性供应组时设置，且不可修改，更多信息请参见[CreateAutoProvisioningGroup](~~122738~~)。

 |
|└RegionId|String|cn-hangzhou| 弹性供应组所在地域的ID。

 |
|└SpotOptions| | | 抢占式实例相关的策略。

 |
|└AllocationStrategy|String|diversified| 抢占式实例的扩容策略，取值范围：

 -   **lowest-price**：成本优化策略，选择价格最低的实例规格创建实例。
-   **diversified**：均衡可用区分布策略，在扩展启动模板指定的可用区创建实例，尽量将实例集群均匀分布到所有可用区。

 |
|└InstanceInterruptionBehavior|String|stop| 抢占式实例关停后的默认动作，取值范围：

 -   **stop**：停止抢占式实例。
-   **terminate**：释放抢占式实例。

 |
|└InstancePoolsToUseCount|Integer|2| 在**SpotAllocationStrategy**为**lowest-price**时生效，弹性供应组选择价格最低的数个实例规格创建实例。

 **说明：** **SpotAllocationStrategy**在创建弹性供应组时设置，且不可修改，更多信息请参见[CreateAutoProvisioningGroup](~~122738~~)。

 |
|└State|String|fulfilled| 弹性供应组整体调度的执行状态，取值范围：

 -   **fulfilled**：调度已完成，并按要求交付实例集群。
-   **pending-fulfillment**：创建实例中。
-   **pending-termination**：移除实例中。
-   **error**：调度时发生异常，未能交付实例集群。

 |
|└Status|String|submitted| 弹性供应组的状态，取值范围：

 -   **submitted**：完成创建，但弹性供应组尚未开始执行调度任务。
-   **active**：弹性供应组已开始执行调度任务。
-   **deleted**：弹性供应组已删除。
-   **deleted-running**：弹性供应组删除中。
-   **modifying**：弹性供应组修改中。

 |
|└TargetCapacitySpecification| | | 弹性供应组的目标容量设置。

 |
|└DefaultTargetCapacityType|String|Spot| 指定差额容量的类型，**PayAsYouGoTargetCapacity**和**SpotTargetCapacity**之和小于**TotalTargetCapacity**时，您可以指定补齐差额容量的实例类型。取值范围：

 -   **PayAsYouGo**：使用按量付费实例补齐差额容量。
-   **Spot**：使用抢占式实例补齐差额容量。

 |
|└PayAsYouGoTargetCapacity|Float|30| 弹性供应组内按量付费实例的目标容量。

 |
|└SpotTargetCapacity|Float|20| 弹性供应组内抢占式实例的目标容量。

 |
|└TotalTargetCapacity|Float|60| 弹性供应组的目标总容量，由以下三个部分组成：

 -   **PayAsYouGoTargetCapacity**指定的按量付费实例目标容量。
-   **SpotTargetCapacity**指定的抢占式实例目标容量。
-   **PayAsYouGoTargetCapacity**和**SpotTargetCapacity**之外的差额容量。

 |
|└TerminateInstances|Boolean|false| 删除弹性供应组时是否释放组内实例，取值范围：

 -   **true**：释放组内实例。
-   **false**：保留组内实例。

 |
|└TerminateInstancesWithExpiration|Boolean|true| 弹性供应组到期时的关停策略，取值范围：

 -   **true**：关停组内抢占式实例，关停后的动作由**SpotInstanceInterruptionBehavior**指定。
-   **false**：组内抢占式实例继续运行。

 **说明：** **SpotInstanceInterruptionBehavior**在创建弹性供应组时设置，且不可修改，更多信息请参见[CreateAutoProvisioningGroup](~~122738~~)。

 |
|└ValidFrom|String|2019-04-01T15:10:20Z| 弹性供应组的启动时间，和**ValidUntil**结合确定有效时段。

 |
|└ValidUntil|String|2019-06-01T15:10:20Z| 弹性供应组的到期时间，和**ValidFrom**结合确定有效时段。

 |
|PageNumber|Integer|1| 实例状态列表的页码。

 |
|PageSize|Integer|10| 分页查询时设置的每页行数。

 |
|RequestId|String|745CEC9F-0DD7-4451-9FE7-8B752F39\*\*\*\*| 请求ID。

 |
|TotalCount|Integer|10| 查询到的弹性供应组的个数。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://ecs.aliyuncs.com/?Action=DescribeAutoProvisioningGroups
&AutoProvisioningGroupId.1=apg-sn54avj8htgvtyh8****
&RegionId=cn-hangzhou
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeAutoProvisioningGroups>
  <PageNumber>1</PageNumber>
  <TotalCount>1</TotalCount>
  <PageSize>10</PageSize>
  <RequestId>85331AC9-82C0-4604-9A14-048865BE****</RequestId>
  <AutoProvisioningGroups>
    <AutoProvisioningGroup>
      <TerminateInstancesWithExpiration>false</TerminateInstancesWithExpiration>
      <TerminateInstances>false</TerminateInstances>
      <ValidFrom>2019-06-17T15:22Z</ValidFrom>
      <AutoProvisioningGroupType>maintain</AutoProvisioningGroupType>
      <PayAsYouGoOptions>
        <AllocationStrategy>lowest-price</AllocationStrategy>
      </PayAsYouGoOptions>
      <AutoProvisioningGroupName>test61****</AutoProvisioningGroupName>
      <CreationTime/>
      <ExcessCapacityTerminationPolicy>no-termination</ExcessCapacityTerminationPolicy>
      <Status>active</Status>
      <MaxSpotPrice>5</MaxSpotPrice>
      <LaunchTemplateVersion>1</LaunchTemplateVersion>
      <ValidUntil>2100-01-01T07:59Z</ValidUntil>
      <TargetCapacitySpecification>
        <SpotTargetCapacity>180</SpotTargetCapacity>
        <TotalTargetCapacity>300</TotalTargetCapacity>
        <PayAsYouGoTargetCapacity>120</PayAsYouGoTargetCapacity>
        <DefaultTargetCapacityType>PayAsYouGo</DefaultTargetCapacityType>
      </TargetCapacitySpecification>
      <State>fulfilled</State>
      <LaunchTemplateId>lt-uf657o6auob6aivd****</LaunchTemplateId>
      <RegionId>cn-shanghai</RegionId>
      <AutoProvisioningGroupId>apg-uf6c7pl7b30t4m98****</AutoProvisioningGroupId>
      <SpotOptions>
        <InstancePoolsToUseCount>1</InstancePoolsToUseCount>
        <InstanceInterruptionBehavior>terminate</InstanceInterruptionBehavior>
        <AllocationStrategy>lowest-price</AllocationStrategy>
      </SpotOptions>
      <LaunchTemplateConfigs>
        <LaunchTemplateConfig>
          <MaxPrice>3</MaxPrice>
          <WeightedCapacity>1</WeightedCapacity>
          <VSwitchId>vsw-uf6qbjwokzl67uqqf****</VSwitchId>
          <Priority>1</Priority>
          <InstanceType>ecs.c5.xlarge</InstanceType>
        </LaunchTemplateConfig>
        <LaunchTemplateConfig>
          <MaxPrice>2</MaxPrice>
          <WeightedCapacity>2</WeightedCapacity>
          <VSwitchId>vsw-uf6n6iy1ib39eqvph****</VSwitchId>
          <Priority>1</Priority>
          <InstanceType>ecs.g5.large</InstanceType>
        </LaunchTemplateConfig>
        <LaunchTemplateConfig>
          <MaxPrice>1</MaxPrice>
          <WeightedCapacity>3</WeightedCapacity>
          <VSwitchId>vsw-uf6gs8uerj5osels4****</VSwitchId>
          <Priority>1</Priority>
          <InstanceType>ecs.hfc5.large</InstanceType>
        </LaunchTemplateConfig>
      </LaunchTemplateConfigs>
    </AutoProvisioningGroup>
  </AutoProvisioningGroups>
</DescribeAutoProvisioningGroups>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"PageNumber":1,
	"TotalCount":1,
	"PageSize":10,
	"RequestId":"85331AC9-82C0-4604-9A14-048865BE****",
	"AutoProvisioningGroups":{
		"AutoProvisioningGroup":[
			{
				"TerminateInstancesWithExpiration":false,
				"TerminateInstances":false,
				"ValidFrom":"2019-06-17T15:22Z",
				"AutoProvisioningGroupType":"maintain",
				"PayAsYouGoOptions":{
					"AllocationStrategy":"lowest-price"
				},
				"AutoProvisioningGroupName":"test61****",
				"CreationTime":"",
				"ExcessCapacityTerminationPolicy":"no-termination",
				"Status":"active",
				"MaxSpotPrice":5,
				"LaunchTemplateVersion":"1",
				"ValidUntil":"2100-01-01T07:59Z",
				"LaunchTemplateId":"lt-uf657o6auob6aivd****",
				"State":"fulfilled",
				"TargetCapacitySpecification":{
					"TotalTargetCapacity":300,
					"SpotTargetCapacity":180,
					"PayAsYouGoTargetCapacity":120,
					"DefaultTargetCapacityType":"PayAsYouGo"
				},
				"RegionId":"cn-shanghai",
				"AutoProvisioningGroupId":"apg-uf6c7pl7b30t4m98****",
				"SpotOptions":{
					"InstancePoolsToUseCount":1,
					"InstanceInterruptionBehavior":"terminate",
					"AllocationStrategy":"lowest-price"
				},
				"LaunchTemplateConfigs":{
					"LaunchTemplateConfig":[
						{
							"MaxPrice":3,
							"WeightedCapacity":1,
							"VSwitchId":"vsw-uf6qbjwokzl67uqqf****",
							"InstanceType":"ecs.c5.xlarge",
							"Priority":1
						},
						{
							"MaxPrice":2,
							"WeightedCapacity":2,
							"VSwitchId":"vsw-uf6n6iy1ib39eqvph****",
							"InstanceType":"ecs.g5.large",
							"Priority":1
						},
						{
							"MaxPrice":1,
							"WeightedCapacity":3,
							"VSwitchId":"vsw-uf6gs8uerj5osels4****",
							"InstanceType":"ecs.hfc5.large",
							"Priority":1
						}
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
|400|MissingParamter.RegionId|The regionId should not be null.|参数 RegionId 不得为空。|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Ecs)

