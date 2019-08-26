# ModifyInstanceDeployment {#doc_api_999436 .reference}

Migrates an ECS instance to a dedicated host \(DDH\) in the same region.

## Description {#description .section}

You can call the ModifyInstanceDeployment operation to complete the following tasks:

-   Add an instance to a deployment set, or migrate an instance from one deployment set to another. The DeploymentSetId parameter is required for this task.
-   You can migrate ECS instances from a shared host to the specified DDH, or migrate instances between two DDHs to reallocate you resources. The DedicatedHostId parameter is required for this task.

When migrating an ECS instance to a DDH, note that:

-   Make sure that the instance is in the Stopped state. The instance automatically restarts after migration.
-   You can only migrate VPC-connected ECS instances.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=ModifyInstanceDeployment) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|InstanceId|String|Yes|i-instanceid1| The ID of the instance. The instance must be in the Stopped or Running state.

 |
|RegionId|String|Yes|cn-hangzhou| The ID of the region where the instance resides. You can call [DescribeRegions](~~25609~~) to view the latest regions of Alibaba Cloud.

 |
|Action|String|No|ModifyInstanceDeployment| The operation that you want to perform. Set the value to ModifyInstanceDeployment.

 |
|DedicatedHostId|String|No|dh-2ze3lmtckdjw1pt8nr8x| The ID of the DDH. You can call [DescribeDedicatedHosts](~~94572~~) to query available DDHs.

 |
|DeploymentSetId|String|No|ds-deploymentsetid1| The ID of the deployment set.

 |
|Force|Boolean|No|false| Indicates whether the DDH of an instance can be changed.

 -   true: You are allowed to change the DDH of an instance. You can restart a running instance, a stopped Subscription-based instance, or a stopped Pay-As-You-Go instance that is still billed.
-   false: You are not allowed to change the DDH of an instance. You can only create a deployment set on the current DDH. This is the default value. Changing the DDH may cause the replacement of deployment set to fail.

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=ModifyInstanceDeployment
&RegionId=cn-hangzhou 
&DeploymentSetId=ds-bp13v7bjnj9gisnlo1
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<ModifyInstanceDeploymentResponse>
  <RequestId>04F0F334-1335-436C-A1D7-6C044FE73368</RequestId>
</ModifyInstanceDeploymentResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId": "04F0F334-1335-436C-A1D7-6C044FE73368"
}
```

## Error codes {#section_x8u_euw_b8e .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|404|InvalidDedicatedHostId.NotFound|The specified DedicatedHostId does not exist.|The error message returned when the ID of the specified DDH does not exist.|
|400|OperationDenied.UnstoppedInstance|Operation denied due to unstopped instance.|The error message returned when the operation is denied on the running instance.|
|400|InvalidDedicatedHostStatus.NotSupport|Operation denied due to dedicated host status.|The error message returned when the operation is denied under the current instance status.|
|400|InvalidPeriod.ExceededDedicatedHost|Instance expired date can't exceed dedicated host expired date.|The error message returned when the expiration date of the instance is later than that of the DDH.|
|404|InvalidInstanceNetworkType.NotSupport|The specified Instance network type not support.|The error message returned when the network type of the specified instance is not supported.|
|404|InvalidInstanceType.NotSupport|The Dedicated host not support the specified instance type.|The error message returned when the current DDH does not support the instance types.|
|400|LackResource|There's no enough resource on the specified dedicated host.|The error message returned when DDH resources are fully consumed.|
|400|OperationDenied.LocalDiskInstance|Operation denied due to instance has local disk|The error message returned when a local storage disk does not support the current operation.|
|403|IncorrectInstanceStatus|%s|The error message returned when the specified resource is in a state that does not support the current operation.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

