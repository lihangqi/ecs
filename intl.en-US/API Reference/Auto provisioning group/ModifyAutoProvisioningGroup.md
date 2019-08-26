# ModifyAutoProvisioningGroup {#doc_api_Ecs_ModifyAutoProvisioningGroup .reference}

You can call this operation to modify the configurations of an auto provisioning group.

Before you call this operation, take note of the following points:

-   If you modify the capacity or capacity-related settings of an auto provisioning group, the group will execute scheduling tasks once after modification.
-   You cannot modify an auto provisioning group when the group is being deleted.

## Debugging {#apiExplorer .section}

Alibaba Cloud provides [OpenAPI Explorer](https://api.aliyun.com/#product=Ecs&api=ModifyAutoProvisioningGroup) to simplify API usage. You can use OpenAPI Explorer to search for APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|RegionId|String|Yes|cn-hangzhou| The region ID of the auto provisioning group to be modified.

 |
|Action|String|No|ModifyAutoProvisioningGroup| The operation that you want to perform. Set this parameter to **ModifyAutoProvisioningGroup**.

 |
|AutoProvisioningGroupId|String|No|apg-uf6jel2bbl62wh13\*\*\*\*| The ID of the auto provisioning group to be modified.

 |
|DefaultTargetCapacityType|String|No|PayAsYouGo| The type of supplemental instances. When the total value of **PayAsYouGoTargetCapacity** and **SpotTargetCapacity** is smaller than the value of **TotalTargetCapacity**, the auto provisioning group will create instances of the specified type to meet the capacity requirements. Valid values:

 -   **PayAsYouGo:** Pay-as-you-go instances.
-   **Spot:** Preemptible instances.

 |
|ExcessCapacityTerminationPolicy|String|No|no-termination| The shutdown policy of the auto provisioning group for excess preemptible instances when the target capacity has been exceeded. Valid values:

 -   **no-termination:** Excess preemptible instances are not shut down.
-   **termination:** Excess preemptible instances are to be shut down. The action to be performed on these shutdown instances is specified by the **SpotInstanceInterruptionBehavior** parameter.

 **Note:** The **SpotInstanceInterruptionBehavior** parameter is set during the auto provisioning group creation process and cannot be modified. For more information, see [CreateAutoProvisioningGroup](~~122738~~).

 |
|MaxSpotPrice|Float|No|8| The global maximum price for preemptible instances in the auto provisioning group. If both the **MaxSpotPrice** and **LaunchTemplateConfig.N.MaxPrice** parameters are specified, the maximum price is the lower value of the two.

 **Note:** The **LaunchTemplateConfig.N.MaxPrice** parameter is set during the auto provisioning group creation process and cannot be modified. For more information, see [CreateAutoProvisioningGroup](~~122738~~).

 |
|PayAsYouGoTargetCapacity|String|No|5| The target capacity of pay-as-you-go instances in the auto provisioning group.

 |
|SpotTargetCapacity|String|No|5| The target capacity of preemptible instances in the auto provisioning group.

 |
|TerminateInstancesWithExpiration|Boolean|No|false| The shutdown policy for preemptible instances when the auto provisioning group expires. Valid values:

 -   **true:** shuts down preemptible instances. The action to be performed on these shutdown instances is specified by the **SpotInstanceInterruptionBehavior** parameter.
-   **false:** does not shut down preemptible instances.

 **Note:** The **SpotInstanceInterruptionBehavior** parameter is set during the auto provisioning group creation process and cannot be modified. For more information, see [CreateAutoProvisioningGroup](~~122738~~).

 |
|TotalTargetCapacity|String|No|10| The total capacity of the auto provisioning group. The capacity consists of the following three parts:

 -   The target capacity of pay-as-you-go instances specified by the **PayAsYouGoTargetCapacity** parameter
-   The target capacity of preemptible instances specified by the **SpotTargetCapacity** parameter
-   The supplemental capacity besides **PayAsYouGoTargetCapacity** and **SpotTargetCapacity**

 |

## Response parameters {#resultMapping .section}

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|B48A12CD-1295-4A38-A8F0-0E92C937\*\*\*\*| The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}

http(s)://ecs.aliyuncs.com/? Action=ModifyAutoProvisioningGroup
&RegionId=cn-hangzhou
&AutoProvisioningGroupId=apg-uf6jel2bbl62wh13****
&<Common request parameters>

```

Sample success responses

`XML` format

``` {#xml_return_success_demo}
<ModifyAutoProvisioningGroupResponse>
  <RequestId>928E2273-5715-46B9-A730-238DC996****</RequestId>
</ModifyAutoProvisioningGroupResponse>

```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"B48A12CD-1295-4A38-A8F0-0E92C937****"
}
```

## Error codes {#section_mfz_o40_575 .section}

|HTTP status code|Error code|Description|Error message|
|----------------|----------|-----------|-------------|
|403|Forbidden.RAM|User not authorized to operate on the specified resource, or this API doesn't support RAM.|The error message returned because the RAM user is not authorized.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

