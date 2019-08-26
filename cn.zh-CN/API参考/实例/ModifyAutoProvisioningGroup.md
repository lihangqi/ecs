# ModifyAutoProvisioningGroup {#doc_api_Ecs_ModifyAutoProvisioningGroup .reference}

调用ModifyAutoProvisioningGroup接口修改一个弹性供应组的设置。

修改弹性供应组前，请注意：

-   如果修改了供应组容量或者容量相关设置，供应组会在修改完成后执行一次调度任务。
-   如果供应组处于删除中状态，无法修改供应组。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=ModifyAutoProvisioningGroup)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
| RegionId |String|是|cn-hangzhou| 弹性供应组所在地域的ID。

 |
| Action |String|否|ModifyAutoProvisioningGroup| 系统规定参数，取值： **ModifyAutoProvisioningGroup** 。

 |
| AutoProvisioningGroupId |String|否|apg-uf6jel2bbl62wh13\*\*\*\*| 弹性供应组的ID。

 |
| DefaultTargetCapacityType |String|否|PayAsYouGo| 指定差额容量的类型， **PayAsYouGoTargetCapacity** 和 **SpotTargetCapacity** 之和小于 **TotalTargetCapacity** 时，您可以指定补齐差额容量的实例类型。可选值：

 -    **PayAsYouGo** ：使用按量付费实例补齐差额容量。
-    **Spot** ：使用抢占式实例补齐差额容量。

 |
| ExcessCapacityTerminationPolicy |String|否|no-termination| 弹性供应组超过容量时，超额的抢占式实例的关停策略，可选值：

 -    **no-termination** ：超额的抢占式实例继续运行。
-    **termination** ：关停超额的抢占式实例，关停后的动作由 **SpotInstanceInterruptionBehavior** 指定。

 **说明：** **SpotInstanceInterruptionBehavior** 在创建弹性供应组时设置，且不可修改，更多信息请参见 [CreateAutoProvisioningGroup](~~122738~~) 。

 |
| MaxSpotPrice |Float|否|8| 弹性供应组内抢占式实例的全局价格上限，同时设置 **MaxSpotPrice** 和 **LaunchTemplateConfig.N.MaxPrice** 时，以较低者为准。

 **说明：** **LaunchTemplateConfig.N.MaxPrice** 在创建弹性供应组时设置，且不可修改，更多信息请参见 [CreateAutoProvisioningGroup](~~122738~~) 。

 |
| PayAsYouGoTargetCapacity |String|否|5| 弹性供应组内按量付费实例的目标容量。

 |
| SpotTargetCapacity |String|否|5| 弹性供应组内抢占式实例的目标容量。

 |
| TerminateInstancesWithExpiration |Boolean|否|false| 弹性供应组到期时的关停策略，可选值：

 -    **true** ：关停组内抢占式实例，关停后的动作由 **SpotInstanceInterruptionBehavior** 指定。
-    **false** ：组内抢占式实例继续运行。

 **说明：** **SpotInstanceInterruptionBehavior** 在创建弹性供应组时设置，且不可修改，更多信息请参见 [CreateAutoProvisioningGroup](~~122738~~) 。

 |
| TotalTargetCapacity |String|否|10| 弹性供应组的目标总容量，由以下三个部分组成：

 -    **PayAsYouGoTargetCapacity** 指定的按量付费实例目标容量。
-    **SpotTargetCapacity** 指定的抢占式实例目标容量。
-    **PayAsYouGoTargetCapacity** 和 **SpotTargetCapacity** 之外的差额容量。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|B48A12CD-1295-4A38-A8F0-0E92C937\*\*\*\*| 请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://ecs.aliyuncs.com/?Action=ModifyAutoProvisioningGroup
&RegionId=cn-hangzhou
&AutoProvisioningGroupId=apg-uf6jel2bbl62wh13****
&<公共请求参数>

```

正常返回示例

 `XML` 格式

``` {#xml_return_success_demo}
<ModifyAutoProvisioningGroupResponse>
  <RequestId>928E2273-5715-46B9-A730-238DC996****</RequestId>
</ModifyAutoProvisioningGroupResponse>

```

 `JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"B48A12CD-1295-4A38-A8F0-0E92C937****"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|403|Forbidden.RAM|User not authorized to operate on the specified resource, or this API doesn't support RAM.|子账号鉴权不通过。|

 [查看本产品错误码](https://error-center.aliyun.com/status/product/Ecs) 

