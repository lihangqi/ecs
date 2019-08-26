# ModifyInstanceDeployment {#doc_api_999436 .reference}

在同一地域下，修改一台 ECS 实例的宿主机。

## 描述 {#description .section}

ModifyInstanceDeployment 可以为您完成以下任务：

-   将一台实例加入一个部署集，或者将实例从一个部署集调整到另外一个部署集。此时，请求参数 DeploymentSetId 是必需参数。
-   如果您有可用的专有宿主机，可以将 ECS 实例从一台共享宿主机迁移到指定的专有宿主机上，也可以在两台专有宿主机上调整实例部署。此时，请求参数 DedicatedHostId 是必需参数。

迁移到专有宿主机时，您需要注意：

-   ECS 实例必须处于已停止（Stopped）状态，迁移后实例自动重启。
-   只支持专有网络 VPC 类型的 ECS 实例。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=ModifyInstanceDeployment)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|InstanceId|String|是|i-instanceid1|实例 ID。实例必须处于Stopped或者Running状态。

 |
|RegionId|String|是|cn-hangzhou|实例共在的地域 ID。您可以调用 [DescribeRegions](~~25609~~) 查看最新的阿里云地域列表。

 |
|Action|String|否|ModifyInstanceDeployment|系统规定参数。取值：ModifyInstanceDeployment

 |
|DedicatedHostId|String|否|dh-2ze3lmtckdjw1pt8nr8x|专有宿主机 ID。您可以调用 [DescribeDedicatedHosts](~~94572~~) 查看可以使用的专有宿主机。

 |
|DeploymentSetId|String|否|ds-deploymentsetid1|部署集 ID。

 |
|Force|Boolean|否|false|是否强制更换实例宿主机。

 -   true：允许实例更换宿主机，允许重启 运行中 的实例、已停止 的预付费（包年包月）实例和 已停止 的停机收费的按量付费实例。
-   false（默认）：不允许实例更换宿主机，只在当前宿主机上加入部署集。这可能导致更换部署集失败。

 |
|OwnerAccount|String|否|ECSforCloud@Alibaba.com|RAM用户的账号登录名称。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。无论调用接口成功与否，我们都会返回请求 ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

https://ecs.aliyuncs.com/?Action=ModifyInstanceDeployment
&RegionId=cn-hangzhou
&DeploymentSetId=ds-bp13v7bjnj9gisnlo1
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
|400|OperationDenied.UnstoppedInstance|Operation denied due to unstopped instance.|非停止实例不支持当前操作。|
|400|InvalidDedicatedHostStatus.NotSupport|Operation denied due to dedicated host status.|资源状态不支持操作。|
|400|InvalidPeriod.ExceededDedicatedHost|Instance expired date can't exceed dedicated host expired date.|实例的自动订阅时长不能晚于专有宿主机订阅时长。|
|404|InvalidInstanceNetworkType.NotSupport|The specified Instance network type not support.|指定实例的网络类型不支持。|
|404|InvalidInstanceType.NotSupport|The Dedicated host not support the specified instance type.|当前宿主机不支持当前实例的规格。|
|400|LackResource|There's no enough resource on the specified dedicated host.|专有宿主机的资源使用空间已满。|
|400|OperationDenied.LocalDiskInstance|Operation denied due to instance has local disk|实例有本地盘不支持当前操作。|
|403|IncorrectInstanceStatus|%s|实例当前的状态不支持该操作。|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Ecs)

