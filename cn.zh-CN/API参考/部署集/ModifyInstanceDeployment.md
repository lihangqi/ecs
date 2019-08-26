# ModifyInstanceDeployment {#doc_api_Ecs_ModifyInstanceDeployment .reference}

调用ModifyInstanceDeployment在同一地域下，修改一台ECS实例的宿主机。

## 接口说明 {#description .section}

ModifyInstanceDeployment可以为您完成以下任务：

-   将一台实例加入一个部署集，或者将实例从一个部署集调整到另外一个部署集。此时，请求参数`DeploymentSetId`是必需参数。
-   如果您有可用的专有宿主机，可以将ECS实例从一台共享宿主机迁移到指定的专有宿主机上，也可以在两台专有宿主机上调整实例部署。此时，请求参数`DedicatedHostId`是必需参数。

迁移到专有宿主机时，您需要注意：

-   ECS实例必须处于**已停止**（Stopped）状态，迁移后实例自动重启。
-   只支持专有网络VPC类型的ECS实例。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=ModifyInstanceDeployment&type=RPC&version=2014-05-26)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|InstanceId|String|是|i-instanceid1|实例ID。实例必须处于**运行中**（Running）或**已停止**（Stopped）状态。

 |
|RegionId|String|是|cn-hangzhou|实例共在的地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。

 |
|Action|String|否|ModifyInstanceDeployment|系统规定参数。取值：ModifyInstanceDeployment

 |
|DedicatedHostId|String|否|dh-2ze3lmtckdjw1pt8n\*\*\*|专有宿主机ID。您可以调用[DescribeDedicatedHosts](~~94572~~)查看可以使用的专有宿主机。

 |
|DeploymentSetId|String|否|ds-deploymentsetid1|部署集ID。

 |
|Force|Boolean|否|false|是否强制更换实例宿主机。

 -   true：允许实例更换宿主机，允许重启**运行中**（Running）的实例、**已停止**（Stopped）状态的预付费（包年包月）实例和已停止的停机收费的按量付费实例。
-   false（默认）：不允许实例更换宿主机，只在当前宿主机上加入部署集。这可能导致更换部署集失败。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=ModifyInstanceDeployment
&RegionId=cn-hangzhou
&DeploymentSetId=ds-bp13v7bjnj9gisn***
&<公共请求参数>
```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ModifyInstanceDeploymentResponse>
	  <RequestId>04F0F334-1335-436C-A1D7-6C044FE73368</RequestId>
</ModifyInstanceDeploymentResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"04F0F334-1335-436C-A1D7-6C044FE73368"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|404|InvalidDedicatedHostId.NotFound|The specified DedicatedHostId does not exist.|指定的专有宿主机ID不存在。|
|404|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|指定的实例不存在，请您检查实例ID是否正确。|
|400|OperationDenied.UnstoppedInstance|Operation denied due to unstopped instance.|非停止实例不支持当前操作。|
|400|InvalidDedicatedHostStatus.NotSupport|Operation denied due to dedicated host status.|资源状态不支持操作。|
|400|InvalidPeriod.ExceededDedicatedHost|Instance expired date can't exceed dedicated host expired date.|实例的自动订阅时长不能晚于专有宿主机订阅时长。|
|404|InvalidInstanceNetworkType.NotSupport|The specified Instance network type not support.|指定实例的网络类型不支持。|
|404|InvalidInstanceType.NotSupport|The Dedicated host not support the specified instance type.|当前宿主机不支持当前实例的规格。|
|400|LackResource|There's no enough resource on the specified dedicated host.|专有宿主机的资源使用空间已满。|
|400|OperationDenied.LocalDiskInstance|Operation denied due to instance has local disk|实例有本地盘不支持当前操作。|
|403|IncorrectInstanceStatus|%s|实例当前的状态不支持该操作。|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

