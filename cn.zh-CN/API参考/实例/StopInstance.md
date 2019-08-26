# StopInstance {#doc_api_1161592 .reference}

停止运行一台实例。

## 接口说明 {#description .section}

-   只有状态为 **运行中**（`Running`）的实例才可以进行此操作。
-   成功调用接口后实例进入 **停止中**（`Stopping`） 状态。实例成功停止关机后进入 **已停止**（`Stopped`）状态。
-   支持强制停止，等同于断电处理，可能丢失实例操作系统中未写入磁盘的数据。
-   [安全控制](~~25695~~) 的实例的 `OperationLocks` 中标记了 `"LockReason" : "security"` 的锁定状态时，不能停止实例。
-   对于配置 [本地盘存储](~~63138~~)（Local\\\_storage） 的 [I1 规格族](~~25378#i1~~) 实例，`ConfirmStop` 入参为必选，取值为 `True` 后接口调用才会成功，否则会返回错误码。
-   I1 规格族实例，成功调用接口后，本地盘存储上的数据将会被清空，需要通过应用层的数据冗余保证数据可用性。
-   系统自动忽略其他规格族实例的 `ConfirmStop` 入参。
-   开通 [默认VPC内实例停机不收费](~~63353~~) 功能后，您可以通过设置 `StoppedMode=KeepCharging` 保持停机收费，ECS 实例停止后会继续计费，并为您保留 ECS 实例规格库存和公网 IP 地址。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=StopInstance)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|InstanceId|String|是|i-instanceid1|指定的实例 ID。

 |
|Action|String|否|StopInstance|系统规定参数。取值：StopInstance

 |
|StoppedMode|String|否|keepcharging|停止 ECS 实例后，实例依然计费。取值：KeepCharging

 开通 [默认VPC内实例停机不收费](~~63353~~) 功能后，您可以通过设置 `StoppedMode=KeepCharging` 保持停机收费，ECS 实例停止后会继续计费，并为您保留 ECS 实例规格库存和公网 IP 地址。

 |
|ForceStop|Boolean|否|false|停止实例时的是否强制关机策略。取值范围：

 -   true：强制关机
-   false（默认）：正常关机流程

 |
|ConfirmStop|Boolean|否|true|是否确认关机。仅对 I1 型实例规格族生效，且为 I1 型的实例规格族的必须入参。默认值：false

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

https://ecs.aliyuncs.com/?Action=StopInstance
&InstanceId=i-instanceid1
&ConfirmStop=true
&ForceStop=false
&StoppedMode=keepcharging
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<StopInstanceResponse>
  <RequestId>1C488B66-B819-4D14-8711-C4EAAA13AC01</RequestId>
</StopInstanceResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"1C488B66-B819-4D14-8711-C4EAAA13AC01"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|403|IncorrectInstanceStatus|The current status of the resource does not support this operation.|该资源目前的状态不支持此操作。|
|403|InstanceType.ParameterMismatch|The input parameter ConfirmStop must be true when an instance have localstorage.|当实例使用本地存储时，输入参数 ConfirmStop 必须为 Ture。|
|403|InstanceExpiredOrInArrears|The specified operation is denied as your prepay instance is expired \(prepay mode\) or in arrears \(afterpay mode\).|包年包月实例已过期，请您续费后再进行操作。|
|403|InvalidInstanceId.NotSupport|Classic network Instance does not support this operation.|经典网络类型实例不支持该操作。|
|403|InvalidInstanceId.NotSupport|Pre pay instance does not support this operation.|预付费实例不支持该操作。|
|403|InvalidInstanceId.NotSupport|Local disk instance does not support this operation.|本地盘实例不支持该操作。|
|403|InvalidInstanceId.NotSupport|Spot instance does not support this operation.|抢占式实例不支持该操作。|
|403|IncorrectInstanceStatus|%s|实例当前的状态不支持该操作。|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Ecs)

