# StartInstance {#doc_api_1161593 .reference}

启动一台实例。

## 接口说明 {#description .section}

-   实例状态必须为 **已停止**（`Stopped`），才可以调用该接口。
-   接口调用成功后实例进入 **启动中** （`Starting`） 状态。
-   被 [安全控制](~~25695~~) 的实例 `OperationLocks` 中标记了 `"LockReason" : "security"` 的锁定状态时，不能启动实例。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=StartInstance)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|InstanceId|String|是|i-instanceid1|指定启动的实例 ID。

 |
|Action|String|否|StartInstance|系统规定参数。取值：StartInstance

 |
|InitLocalDisk|Boolean|否|false|适用于 [实例规格族](~~25378~~) D1、I1 或者 I2 等包含本地盘的实例。当 D1、I1 或者 I2 的本地盘出现故障时，可通过此参数指定启动实例时，是否将实例恢复到最初的健康状态。取值范围：

 -   true：将实例恢复到最初的健康状态，实例原有本地磁盘中的数据将会丢失。
-   false（默认）：不做任何处理，维持现状。

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
https://ecs.aliyuncs.com/?Action=StartInstance
&InstanceId=i-instanceid1
&InitLocalDisk=false
&<公共请求参数>
```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<StartInstanceResponse>
  <RequestId>C0003E8B-B930-4F59-ADC0-0E20xxxxxxxx</RequestId>
</StartInstanceResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"C0003E8B-B930-4F59-ADC0-0E20xxxxxxxx"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|403|IncorrectInstanceStatus|The current status of the resource does not support this operation.|该资源目前的状态不支持此操作。|
|403|DiskError|IncorrectDiskStatus.|指定的磁盘状态不合法。|
|403|InstanceExpired|The postPaid instance has been expired.Please ensure your account have enough balance.|按量付费实例因账号欠费被停止。|
|403|InstanceExpired|The prePaid instance has been expired.|按量付费实例因账号欠费被停止。|
|403|InstanceNotReady|The specified instance is not ready for use.|该资源目前的状态不支持此操作，请您等待一段时间再进行操作，并确认实例目前状态与操作是否冲突。|
|403|IncorrectInstanceStatus|%s|实例当前的状态不支持该操作。|
|403|InvalidParameter.KMSKeyId.KMSUnauthorized|ECS service have no right to access your KMS.|ECS未被授权访问您的KMS资源。|
|500|InternalError|The request processing has failed due to some unknown error, exception or failure.|发生未知错误。|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Ecs)

