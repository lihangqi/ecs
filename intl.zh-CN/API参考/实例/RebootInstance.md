# RebootInstance {#doc_api_Ecs_RebootInstance .reference}

重启一台实例。

## 接口说明 {#description .section}

-   您只能重启状态为 **运行中**（`Running`）的 ECS 实例。
-   重启 ECS 实例后进入 **启动中**（`Starting`）状态。
-   支持强制重启（`ForceStop`），强制重启等同于传统服务器的断电重启，可能丢失实例操作系统中未写入磁盘的数据。
-   被 [安全控制](~~25695~~) 的 ECS 实例的 `OperationLocks` 中标记了 `"LockReason" : "security"` 时，不能重启实例。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=RebootInstance)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|InstanceId|String|是|i-instance1|指定实例的 ID。

 |
|Action|String|否|RebootInstance|系统规定参数。取值：RebootInstance

 |
|DryRun|Boolean|否|false|是否只预检此次请求。

 -   true：发送检查请求，不会创建实例。检查项包括是否填写了必需参数、请求格式、业务限制和ECS库存。如果检查不通过，则返回对应错误。如果检查通过，则返回错误码`DryRunOperation`。
-   false（默认）：发送正常请求，通过检查后直接重启实例。

 |
|ForceStop|Boolean|否|false|重启 ECS 实例前是否强制关机策略。取值范围：

 -   true：重启 ECS 实例前强制关机
-   false（默认）：重启 ECS 实例前正常关机

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

https://ecs.aliyuncs.com/?Action=RebootInstance
&InstanceId=i-instance1
&ForceStop=false
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<RebootInstanceResponse>
  <RequestId>F2E2C40D-AB09-45A1-B5C5-EB9F5C4E4E4A</RequestId>
</RebootInstanceResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"F2E2C40D-AB09-45A1-B5C5-EB9F5C4E4E4A"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|404|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|指定的实例不存在，请您检查实例ID是否正确。|
|403|IncorrectInstanceStatus|The current status of the resource does not support this operation.|该资源目前的状态不支持此操作。|
|403|InstanceLockedForSecurity|The specified operation is denied as your instance is locked for security reasons.|实例被安全锁定，指定的操作无法完成。|
|403|DiskError|IncorrectDiskStatus.|指定的磁盘状态不合法。|
|500|InternalError|The request processing has failed due to some unknown error.|内部错误，请重试。如果多次尝试失败，请提交工单|
|403|InstanceExpiredOrInArrears|The specified operation is denied as your prepay instance is expired \(prepay mode\) or in arrears \(afterpay mode\).|包年包月实例已过期，请您续费后再进行操作。|
|403|IncorrectInstanceStatus|%s|实例当前的状态不支持该操作。|
|403|InvalidParameter.KMSKeyId.KMSUnauthorized|ECS service have no right to access your KMS.|ECS未被授权访问您的KMS资源。|
|500|InternalError|The request processing has failed due to some unknown error, exception or failure.|发生未知错误。|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Ecs)

