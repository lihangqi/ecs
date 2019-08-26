# ModifyInstanceAttribute {#doc_api_Ecs_ModifyInstanceAttribute .reference}

修改一台实例的部分信息，包括实例密码、名称、描述、主机名和自定义数据等。如果是t5突发性能实例，可以切换这台实例的性能突发模式。

## 描述 {#description .section}

调用该接口时，您需要注意：

-   实例状态为**启动中**（`Starting`）时，无法重置实例密码。
-   被 [安全控制](~~25695~~)的 ECS 实例的 `OperationLocks` 不能标记为 `"LockReason" : "security"`。
-   重置密码后，您需要在控制台 [重启实例](~~25440~~) 或者调用 API [RebootInstance](~~25502~~) 使更改生效，在实例内部重启将不会生效。
-   实例状态为 **已停止**（`Stopped`）且满足 [实例自定义数据](~~49121~~) 使用限制时，支持修改自定义数据。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=ModifyInstanceAttribute)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|InstanceId|String|是|i-instance1|实例 ID。

 |
|Action|String|否|ModifyInstanceAttribute|接口名称。取值：**ModifyInstanceAttribute**

 |
|CreditSpecification|String|否|Standard|修改t5突发性能实例的运行模式。取值范围：

 -   Standard：标准模式，实例性能请参见 [什么是突发性能实例](~~59977~~) 下的性能约束模式章节。
-   Unlimited：无性能约束模式，实例性能请参见 [什么是突发性能实例](~~59977~~) 下的无性能约束模式章节。

 默认值：无。

 |
|DeletionProtection|Boolean|否|false|实例释放保护属性，指定是否支持通过控制台或 API（[DeleteInstance](~~25507~~)）释放实例。

 默认值：无。

 **说明：** 该属性仅适用于按量付费实例，且只能限制手动释放操作，对系统释放操作不生效。

 |
|Description|String|否|InstanceAttribute|实例描述。长度为 2~256 个英文或中文字符，不能以 http:// 和 https:// 开头。

 默认值：无。

 |
|HostName|String|否|LocalHost|操作系统的计算机名。

 -   点号（`.`）和短横线（`-`）不能作为首尾字符，更不能连续使用。
-   Windows 实例：字符长度为 2~15，不支持点号（`.`），不能全是数字。允许大小写英文字母、数字和短横线（`-`）。
-   其他类型实例（Linux 等）：字符长度为 2~64，支持多个点号（`.`），点之间为一段，每段允许大小写英文字母、数字和短横线（`-`）。

 |
|InstanceName|String|否|EcsInstance|实例名称。长度为 2~128 个英文或中文字符。必须以大小字母或中文开头，不能以 http:// 和 https:// 开头。可以包含数字、半角冒号（`:`）、下划线（`_`）或者连字符（`-`）。

 |
|Password|String|否|EcsV587!|实例的密码。长度为 8 至 30 个字符，必须同时包含大小写英文字母、数字和特殊符号中的三类字符。特殊符号可以是：

 ```

()`~!@#$%^&*-_+=|{}[]:;'<>,.?/

```

 其中，Windows 实例不能以斜线号（/）为密码首字符。

 **说明：** 如果传入`Password`参数，建议您使用HTTPS协议发送请求，避免密码泄露。

 |
|Recyclable|Boolean|否|false|实例是否可以回收。

 |
|UserData|String|否|echo hello ecs!|实例自定义数据，需要以 Base64 编码。编码前，原始数据不能超过 16 KB。建议不要明文传入敏感信息，例如密码和私钥等。如果必须传入敏感信息，建议您加密后再以 Base64 编码传入，在实例内部以同样的方式反解密。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。无论调用接口成功与否，我们都会返回请求 ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

https://ecs.aliyuncs.com/?Action=ModifyInstanceAttribute
/?InstanceId=i-instance1
&Action=ModifyInstanceAttribute
&CreditSpecification=Standard
&DeletionProtection=false
&Description=InstanceAttribute
&HostName=LocalHost
&InstanceName=EcsInstance
&Password=EcsV587!
&Recyclable=
&UserData=echo hello ecs!
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ModifyInstanceAttributeResponse>
  <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</ModifyInstanceAttributeResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InvalidInstanceName.Malformed|The specified parameter "InstanceName" is not valid.|指定的实例名称格式不合法。长度为2-128个字符，以英文字母或中文开头，可包含数字，"."，"\_"或"-"。 不能以 http:// 和 https:// 开头。|
|400|InvalidDescription.Malformed|The specified parameter "Description" is not valid.|指定的资源描述格式不合法。长度为2-256个字符，不能以 http:// 和 https:// 开头。|
|400|InvalidHostPassword.Malformed|The specified parameter "Password" is not valid.|指定的实例密码格式不合法。|
|400|InvalidHostName.Malformed|The specified parameter "HostName" is not valid.|指定的HostName格式不合法。|
|403|IncorrectInstanceStatus|The current status of the resource does not support this operation.|该资源目前的状态不支持此操作。|
|403|InstanceLockedForSecurity|The specified operation is denied as your instance is locked for security reasons.|实例被安全锁定，指定的操作无法完成。|
|404|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|指定的实例不存在，请您检查实例ID是否正确。|
|404|InvalidSecurityGroupId.NotFound|The specified SecurityGroupId does not exist.|指定的安全组在该用户账号下不存在，请您检查安全组id是否正确。|
|403|OperationDenied|The instance amount in the specified SecurityGroup reach its limit.|指定安全组的实例数已达最大值。|
|403|OperationDenied|The current status of the resource does not support this operation.|该资源状态不支持此类操作。|
|400|InvalidPassword.Malformed|The specified parameter "Password" is not valid.|指定的 Password 参数不合法。|
|500|InternalError|The request processing has failed due to some unknown error.|内部错误，请重试。如果多次尝试失败，请提交工单|
|403|InvalidUserData.Forbidden|User not authorized to input the parameter "UserData"please apply for permission "UserData"|该用户无权输入 UserData。请先申请权限。|
|400|InvalidUserData.SizeExceeded|The specified parameter "UserData" exceeds the size.|指定的 UserData 超过大小限制。|
|400|InvalidUserData.NotSupported|TThe specified parameter "UserData" only support the vpc and IoOptimized Instance.|指定的 UserData 仅支持 VPC 和 I/O 优化型实例。|
|400|InvalidUserData.NotSupported|The specified parameter "UserData" only support the vpc and IoOptimized Instance.|指定的 UserData 仅支持 VPC 和 I/O 优化型实例。|
|400|ImageNotSupportCloudInit|The specified image does not support cloud-init.|指定的镜像不支持 cloud-init。|
|403|InvalidUserData.Base64FormatInvalid|The specified UserData is not valid|指定的 UaseData 不合法。|
|400|ChargeTypeViolation|Pay-As-You-Go instances do not support this operation.|按量付费实例不支持该操作，检查实例的付费类型是否与该操作冲突。|
|400|InvalidParameter.RecycleBin|You do not have permission to set recyclable properties.|您未被授权执行该操作。|
|400|InvalidParameter.CreditSpecification|The specified CreditSpecification is not supported in this region.|当前地域不支持指定的CreditSpecification。|
|400|InvalidInstanceStatus.CreditSpecRestricted|The current status of the resource does not support this operation.|资源的当前状态不支持该操作。|
|400|InvalidInstanceStatus.NotRunning|The current status of the resource is invalid, you can only do this operation when instance is running.|资源的当前状态无效。|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Ecs)

