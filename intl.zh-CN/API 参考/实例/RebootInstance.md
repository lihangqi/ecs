# RebootInstance {#RebootInstance .reference}

重启一台实例。

## 描述 {#section_nkm_wnr_xdb .section}

-   您只能重启状态为 **运行中**（`Running`）的 ECS 实例。
-   重启 ECS 实例后进入 **启动中**（`Starting`）状态。
-   支持强制重启（`ForceStop`），强制重启等同于传统服务器的断电重启，可能丢失实例操作系统中未写入磁盘的数据。
-   被 [安全控制](intl.zh-CN/API 参考/附录/安全锁定时的 API 行为.md#) 的 ECS 实例的 `OperationLocks` 中标记了 `"LockReason" : "security"` 时，不能重启实例。

## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：RebootInstance|
|InstanceId|String|是|指定实例的 ID。|
|ForceStop|String|否|重启 ECS 实例前是否强制关机策略。取值范围：-   true：重启 ECS 实例前强制关机
-   false：重启 ECS 实例前正常关机

默认值：false|

## 返回参数 {#ResponseParameter .section}

全是公共返回参数。参阅[公共参数](intl.zh-CN/API 参考/快速入门/公共参数.md#commonResponseParameters)

## 示例 { .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=RebootInstance
&InstanceId=i-instance1
&<公共请求参数>
```

**返回示例**

 **XML 格式** 

```
<RebootInstanceResponse>
    <RequestId>F2E2C40D-AB09-45A1-B5C5-EB9F5C4E4E4A</RequestId>
</RebootInstanceResponse>
```

 **JSON 格式** 

```
{
    "RequestId": "F2E2C40D-AB09-45A1-B5C5-EB9F5C4E4E4A"
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问 [API 错误中心](https://error-center.alibabacloud.com/status/product/Ecs)。

|错误代码|错误信息|HTTP 状态码|说明|
|:---|:---|:-------|:-|
|DiskError|IncorrectDiskStatus.|403|不正常的磁盘状态。|
|IncorrectInstanceStatus|The current status of the resource does not support this operation.|403|该资源目前的状态不支持此操作。|
|InstanceLockedForSecurity|The specified operation is denied as your instance is locked for security reasons.|403|该资源目前被安全锁定被拒绝操作。|
|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|404|指定的 `InstanceId` 不存在。|

