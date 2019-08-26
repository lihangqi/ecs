# ModifyInstanceDeployment {#ModifyInstanceDeployment .reference}

在同一地域下，修改一台 ECS 实例的宿主机。

## 描述 {#section_i5w_p32_lfb .section}

ModifyInstanceDeployment 可以为您完成以下任务：

-   将一台实例加入一个部署集，或者将实例从一个部署集调整到另外一个部署集。此时，请求参数DeploymentSetId 是必需参数。

-   如果您有可用的专有宿主机，可以将 ECS 实例从一台共享宿主机迁移到指定的专有宿主机上，也可以在两台专有宿主机上调整实例部署。此时，请求参数DedicatedHostId 是必需参数。


迁移到专有宿主机时，您需要注意：

-   ECS 实例必须处于已停止（Stopped）状态，迁移后实例自动重启。

-   只支持专有网络 VPC 类型的 ECS 实例。

-   目标专有宿主机与待迁移 ECS 实例的计费方式必须一致。

-   将 ECS 实例从一台共享宿主机迁移到专有宿主机上时，实例的计费方式只能是按量付费，不支持预付费实例和抢占式实例。


## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：ModifyInstanceDeployment|
|RegionId|String|是|实例共在的地域 ID。您可以调用[DescribeRegions](../cn.zh-CN/API 参考/地域/DescribeRegions.md#)查看最新的阿里云地域列表。|
|InstanceId|String|是|实例 ID。实例必须处于`Stopped`或者`Running`状态。|
|DeploymentSetId|String|否|部署集 ID。|
|DedicatedHostId|String|否|专有宿主机 ID。您可以调用 [DescribeDedicatedHosts](cn.zh-CN/API 参考/专有宿主机/DescribeDedicatedHosts.md#) 查看可以使用的专有宿主机。|
|Force|Boolean|否|是否强制更换实例宿主机。-   true：允许实例更换宿主机，允许重启**运行中**的实例、**已停止**的预付费（包年包月）实例和**已停止**的停机收费的按量付费实例。
-   false（默认）：不允许实例更换宿主机，只在当前宿主机上加入部署集。这可能导致更换部署集失败。

|

## 返回参数 {#ResponseParameter .section}

全是公共返回参数。参阅[公共返回参数](../cn.zh-CN/API 参考/快速入门/公共参数.md#commonResponseParameters)。

## 示例 { .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=ModifyInstanceDeployment
&RegionId=cn-hangzhou
&DeploymentSetId=ds-bp13v7bjnj9gisnlo1
&<公共请求参数>
```

**返回示例**

**XML 格式**

```
<ModifyInstanceDeploymentResponse>
	<RequestId>04F0F334-1335-436C-A1D7-6C044FE73368</RequestId>
</ModifyInstanceDeploymentResponse>
```

**JSON 格式**

```
{
	"RequestId": "04F0F334-1335-436C-A1D7-6C044FE73368"
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问[API错误中心](https://error-center.aliyun.com/status/product/Ecs)。

|错误代码|错误信息|HTTP状态码|说明|
|:---|:---|:------|:-|
|DeploymentSet.InvalidId|The specified Deployment Set id doesn't exist.|400|指定的DeploymentSetId不存在。|
|DeploymentSet.InstanceLimitExceeded|The number of instances on the specified Deployment Set has reached the limit.|403|指定的部署集内所含实例已达上限。|
|IncorrectInstanceStatus|The current status of the resource does not support this operation.|403|该资源目前的状态不支持此操作。|
|DeploymentSet.ModificationFailed|The modification of deployment set is currently impossible.|403|无法调整部署集。|
|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|404|指定实例 ID 不存在。|
|InvalidDedicatedHostId.NotFound|The specified DedicatedHostId does not exist.|404|指定专有宿主机 ID 不存在。|
|LackResource|There's no enough resource on the specified dedicated host.|400|指定专有宿主机已满负荷。|
|OperationDenied.UnstoppedInstance|Operation denied due to unstopped instancein your request.|400|迁移到专有宿主机时，ECS 实例必须处于已停止（Stopped）状态，|
|InvalidPeriod.ExceededDedidactedHost|Instance expired date can't exceed dedicated host expired date.|400|预付费 ECS 实例的到期时间不能晚于专有宿主机到期时间。|
|InvalidInstanceNetworkType.NotSupport|The specified Instance network type not support.|404|迁移到专有宿主机时，只支持专有网络 VPC 类型的 ECS 实例。|
|InvalidInstanceChargeType.NotSupport|The Dedicated host not support the specified Instance charge type.|404|将 ECS 实例从一台共享宿主机迁移到专有宿主机上时，实例的计费方式只能是按量付费，不支持预付费实例和抢占式实例。|
|InvalidInstanceType.NotSupport|The Dedicated host not support the specified Instance type|404|专有宿主机不支持目标 ECS 实例的规格。|
|InvalidDedicatedHostStatus.NotSupport|Operation denied due to dedicated host status|400|您的账号已欠费，或者专有宿主机不可用。|
|InternalError|The request processing has failed due to some unknown error,exception or failure.|500|内部错误。|

