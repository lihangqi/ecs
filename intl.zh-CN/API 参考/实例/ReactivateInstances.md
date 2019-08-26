# ReactivateInstances {#ReactivateInstances .reference}

重新启动一台已过期或欠费回收中的按量付费 ECS 实例。

## 描述 {#section_gvn_mmx_rfb .section}

调用该接口时，您需要注意：

-   实例必须处于 **已过期**（`Stopped`）或者 **欠费回收中**（`Stopped`）的状态。

-   为避免实例会被释放和无法恢复数据，您必须在实例欠费停机后 15 天内清理账单并重开机实例。无法重开机 VPC 类型实例时，请间隔一段时间后再试或 [提交工单](https://workorder-intl.console.aliyun.com/#/ticket/createIndex) 联系阿里云。

-   更多业务限制，请参阅 [重开机](../intl.zh-CN/用户指南/实例/重开机.md#)。

-   接口调用成功后实例进入 **启动中** （`Starting`）状态。

-   被[安全控制](../intl.zh-CN/API 参考/附录/安全锁定时的 API 行为.md#)的ECS实例的`OperationLocks`不能标记为`"LockReason" : "security"`。


## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：ReactivateInstances|
|InstanceId|String|是|需要重开机的实例 ID。|

## 返回参数 {#ResponseParameter .section}

全是公共返回参数。参阅[公共返回参数](../intl.zh-CN/API 参考/快速入门/公共参数.md#commonResponseParameters)。

## 示例 {#Samples .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=ReactivateInstances
&InstanceId=i-instance1
&<公共请求参数>
```

**返回示例**

**XML 格式**

```
<ReactivateInstancesResponse>
    <RequestId>51AB7717-6E1A-4D1D-A44D-54CBxxxxxxxx</RequestId>
</ReactivateInstancesResponse>
```

**JSON 格式**

```
{
	"RequestId": "51AB7717-6E1A-4D1D-A44D-54CBxxxxxxxx"
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问[API错误中心](https://error-center.alibabacloud.com/status/product/Ecs)。

|错误代码|错误信息|HTTP 状态码|说明|
|:---|:---|:-------|:-|
|IncorrectInstanceStatus|The current status of the resource does not support this operation.|403|该资源目前的状态不支持此操作。|
|InstanceLockedForSecurity|The specified operation is denied as your instance is locked for security reasons.|403|该资源目前被安全锁定被拒绝操作。|
|InsufficientBalance|Your account does not have enough balance.|403|请清理完您的云账号下所有未支付订单后重试。|
|ReactivateInstances.InstanceStatusNotValid|Instance status is not Expired, ImageExpired or EcsAndImageExpired.|403|按量付费实例必须处于 **已过期** 或者 **欠费回收中** 状态。|
|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|404|指定的 InstanceId 不存在。|
|InvalidPayType.NotSupport|The specified pre pay instance not support.|404|只支持按量付费实例。|
|InternalError|The request processing has failed due to some unknown error.|500|内部错误，请稍后重试。|

