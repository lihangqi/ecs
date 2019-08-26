# StopInstance {#StopInstance .reference}

停止运行一台实例。

## 描述 {#section_tcm_s4m_xdb .section}

-   只有状态为 **运行中**（`Running`）的实例才可以进行此操作。
-   成功调用接口后实例进入 **停止中**（`Stopping`） 状态。实例成功停止关机后进入 **已停止**（`Stopped`）状态。
-   支持强制停止，等同于断电处理，可能丢失实例操作系统中未写入磁盘的数据。
-    [安全控制](cn.zh-CN/API 参考/附录/安全锁定时的 API 行为.md#) 的实例的 `OperationLocks` 中标记了 `"LockReason" : "security"` 的锁定状态时，不能停止实例。
-   对于配置 [本地盘存储](../../../../cn.zh-CN/产品简介/块存储/本地盘.md#)（Local\_storage） 的 [I1 规格族](../../../../cn.zh-CN/产品简介/实例规格族.md#i1) 实例，`ConfirmStop` 入参为必选，取值为 `True` 后接口调用才会成功，否则会返回错误码。
-   I1 规格族实例，成功调用接口后，本地盘存储上的数据将会被清空，需要通过应用层的数据冗余保证数据可用性。
-   系统自动忽略其他规格族实例的 `ConfirmStop` 入参。
-   开通 **[默认VPC内实例停机不收费](../../../../cn.zh-CN/产品定价/按量付费实例停机不收费.md#)** 功能后，您可以通过设置 `StoppedMode=KeepCharging` 保持停机收费，ECS 实例停止后会继续计费，并为您保留 ECS 实例规格库存和公网 IP 地址。

## 请求参数 { .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：StopInstance|
|InstanceId|String|是|指定的实例 ID。|
|ForceStop|String|否|停止实例时的是否强制关机策略。取值范围：-   true：强制关机
-   false：正常关机流程

默认值：false|
|ConfirmStop|String|否|是否确认关机。仅对 I1 型实例规格族生效，且为 I1 型的实例规格族的必须入参。取值范围：-   true
-   false

默认值：false|
|StoppedMode|String|否|停止 ECS 实例后，实例依然计费。取值：KeepCharging开通 **[默认VPC内实例停机不收费](../../../../cn.zh-CN/产品定价/按量付费实例停机不收费.md#)** 功能后，您可以通过设置 `StoppedMode=KeepCharging` 保持停机收费，ECS 实例停止后会继续计费，并为您保留 ECS 实例规格库存和公网 IP 地址。

|

## 返回参数 {#section_edm_s4m_xdb .section}

全是公共返回参数。参阅[公共参数](cn.zh-CN/API 参考/快速入门/公共参数.md#commonResponseParameters)。

## 示例 { .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=StopInstance
&InstanceId=i-instance1
&<公共请求参数>
```

**返回示例** 

**XML 格式** 

```
<StopInstanceResponse>
    <RequestId>1C488B66-B819-4D14-8711-C4EAAA13AC01</RequestId>
</StopInstanceResponse>
```

 **JSON 格式** 

```
{
    "RequestId": "1C488B66-B819-4D14-8711-C4EAAA13AC01"
}
```

## 错误码 { .section}

以下为本接口特有的错误码。更多错误码，请访问 [API 错误中心](https://error-center.aliyun.com/status/product/Ecs)。

|错误代码|错误信息|HTTP 状态码|说明|
|:---|:---|:-------|:-|
|DiskError|IncorrectDiskStatus|403|不正常的磁盘状态。|
|InstanceLockedForSecurity|The specified operation is denied as your instance is locked for security reasons.|403|该资源目前被安全锁定被拒绝操作。|
|IncorrectInstanceStatus|The current status of the resource does not support this operation.|403|该资源目前的状态不支持此操作。|
|InstanceType.ParameterMismatch|The input parameter ConfirmStop must be true when an instance have localstorage.|403|ConfirmStop 入参值不正确。|
|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|404|指定的 InstanceId 不存在。|

