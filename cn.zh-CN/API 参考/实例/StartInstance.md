# StartInstance {#StartInstance .reference}

启动一台实例。

## 描述 {#section_njd_cmm_xdb .section}

-   实例状态必须为 **已停止**（`Stopped`），才可以调用该接口。
-   接口调用成功后实例进入 **启动中** （`Starting`） 状态。
-   被 [安全控制](cn.zh-CN/API 参考/附录/安全锁定时的 API 行为.md#) 的实例 `OperationLocks` 中标记了 `"LockReason" : "security"` 的锁定状态时，不能启动实例。

## 请求参数 {#section_nzr_pww_ydb .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：StartInstance|
|InstanceId|String|是|指定启动的实例 ID。|
|InitLocalDisk|Boolean|否|适用于 [实例规格族](../cn.zh-CN/产品简介/实例规格族.md#) D1、I1 或者 I2 等包含本地盘的实例。当 D1、I1 或者 I2 的本地盘出现故障时，可通过此参数指定启动实例时，是否将实例恢复到最初的健康状态。取值范围：-   true：将实例恢复到最初的健康状态，实例原有本地磁盘中的数据将会丢失。
-   false：不做任何处理，维持现状。

|

## 返回参数 {#section_ujd_cmm_xdb .section}

全是公共返回参数。参阅 [公共返回参数](cn.zh-CN/API 参考/快速入门/公共参数.md#commonResponseParameters)。

## 示例 { .section}

**请求示例** 

```
 https://ecs.aliyuncs.com/?Action=StartInstance
&InstanceId=i-instance1
&<公共请求参数>

```

**返回示例** 

**XML 格式**

```
<StartInstanceResponse>
    <RequestId>C0003E8B-B930-4F59-ADC0-0E20xxxxxxxx</RequestId>
</StartInstanceResponse>
```

**JSON 格式** 

```
{
    "RequestId": "C0003E8B-B930-4F59-ADC0-0E20xxxxxxxx"
}

```

## 错误码 { .section}

以下为本接口特有的错误码。更多错误码，请访问 [API 错误中心](https://error-center.aliyun.com/status/product/Ecs)。

|错误代码|错误信息|HTTP 状态码|说明|
|:---|:---|:-------|:-|
|DiskError|IncorrectDiskStatus.|403|不正常的磁盘状态。|
|IncorrectInstanceStatus|The current status of the resource does not support this operation.|403|该资源目前的状态不支持此操作。|
|InstanceExpired|PrePaid instances has been expired.|403|包年包月实例到期，按量付费实例已欠费。|
|InstanceLockedForSecurity|The specified operation is denied as your instance is locked for security reasons.|403|该资源目前被安全锁定被拒绝操作。|
|InsufficientBalance|Your account does not have enough balance.|403|实例欠费，拒绝启动。|
|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|404|指定的 InstanceId 不存在。|
|InstanceNotReady|The specified instance is not ready for use|500|指定的 Instance 还没有创建完。|
|InternalError|The request processing has failed due to some unknown error.|500|内部错误，请稍后重试。|

