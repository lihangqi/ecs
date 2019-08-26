# ModifyInstanceAttribute {#ModifyInstanceAttribute .reference}

修改一台实例的部分信息，包括实例密码、名称、描述、主机名和自定义数据等。如果是突发性能 t5 实例，可以切换这台实例的性能突发模式。

## 描述 {#section_ufy_4pt_xdb .section}

调用该接口时，您需要注意：

-   实例状态为**启动中**（`Starting`）时，无法重置实例密码。

-   被[安全控制](../intl.zh-CN/API 参考/附录/安全锁定时的 API 行为.md#)的ECS实例的`OperationLocks`不能标记为`"LockReason" : "security"`。

-   重置密码后，您需要在控制台 [重启实例](../intl.zh-CN/用户指南/实例/重启实例.md#) 或者调用 [RebootInstance](intl.zh-CN/API 参考/实例/RebootInstance.md#) 使更改生效，在实例内部重启将不会生效。

-   实例状态为 **已停止**（`Stopped`）且满足 [实例自定义数据](../intl.zh-CN/用户指南/实例/实例自定义数据和元数据/实例自定义数据.md) 使用限制时，支持修改自定义数据。


## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：ModifyInstanceAttribute|
|InstanceId|String|是|实例 ID。|
|InstanceName|String|否|实例名称。长度为 \[2, 128\] 个英文或中文字符。必须以大小字母或中文开头，不能以 http:// 和 https:// 开头。可以包含数字、半角冒号（:）、下划线（\_）或者连字符（-）。|
|Description|String|否|实例描述。长度为 \[2, 256\] 个英文或中文字符，不能以 http:// 和 https:// 开头。默认值：空。

|
|Password|String|否|实例的密码。长度为 8 至 30 个字符，必须同时包含大小写英文字母、数字和特殊符号。特殊符号可以是\(\)\` ~!@\#$%^&\*-+=|\{\}\[\]:;‘<\>,.?/。其中，Windows 实例不能以斜线号（/）为密码首字符。**说明：** 如果传入 `Password` 参数，建议您使用 HTTPS 调用方式，避免密码泄露。

|
|HostName|String|否|操作系统的计算机名。-   点号（.）和短横线（-）不能作为首尾字符，更不能连续使用。
-   Windows 实例：字符长度为 \[2, 15\]，不支持点号（.），不能全是数字。允许大小写英文字母、数字和短横线（-）。
-   其他类型实例（Linux 等）：字符长度为 \[2, 64\]，支持多个点号（.），点之间为一段，每段允许大小写英文字母、数字和短横线（-）。

|
|UserData|String|否|实例自定义数据，需要以 Base64 编码。编码前，原始数据不能超过 16 KB。建议不要明文传入敏感信息，例如密码和私钥等。如果必须传入敏感信息，建议您加密后再以 Base64 编码传入，在实例内部以同样的方式反解密。|
|CreditSpecification|String|否| 修改突发性能 t5 实例的运行模式。取值范围：

 -   Standard：标准模式，实例性能请参阅 [t5性能约束实例](../intl.zh-CN/产品简介/实例/突发性能实例/t5性能约束实例.md#)。
-   Unlimited：无性能约束模式，实例性能请参阅 [t5无性能约束实例](../intl.zh-CN/产品简介/实例/突发性能实例/t5无性能约束实例.md#)。

 默认值：无。

 |

## 返回参数 {#ResponseParameter .section}

全是公共返回参数。参阅[公共返回参数](../intl.zh-CN/API 参考/快速入门/公共参数.md#commonResponseParameters)。

## 示例 { .section}

**请求示例**

```
https://ecs.aliyuncs.com/?Action=ModifyInstanceAttribute
&InstanceId=i-instance1
&Password=pwd
&<公共请求参数>
```

**返回示例**

**XML 格式**

```
<ModifyInstanceAttributeResponse>
    <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</ModifyInstanceAttributeResponse>
```

**JSON 格式**

```
{
    "RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E"
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问[API错误中心](https://error-center.alibabacloud.com/status/product/Ecs)。

|错误代码|错误信息|HTTP 状态码|说明|
|:---|:---|:-------|:-|
|InvalidDescription.Malformed|The specified parameter “Description” is not valid.|400|指定的Description 格式不正确。|
|InvalidDescription.Malformed|The specified destination image description is wrongly formed.|400|指定的Description 不合法。|
|InvalidHostPassword.Malformed|The specified parameter “Password” is not valid.|400|指定的 Password 不合法。|
|InvalidInstanceName.Malformed|The specified parameter “InstanceName” is not valid.|400|指定的 InstanceName 不合法。|
|InvalidInstanceStatus.CreditSpecRestricted|The current status of the resource does not support this operation.|400|您的账号已欠费，无法切换 t5 实例的性能突发模式。|
|InvalidHostName.Malformed|The specified parameter “HostName” is not valid.|400|指定的HostName 不合法。|
|InvalidParameter.CreditSpecification|The specified CreditSpecification is not supported in this region.|400|指定的 CreditSpecification无效。或者当前地域不支持该性能突发模式。|
|InvalidPassword.Malformed|The specified parameter “Password” is not valid.|400|指定的Password 不合法。|
|InvalidUserData.SizeExceeded|The specified parameter “UserData” exceeds the size.|400|Base64 编码UserData 前，原始数据不能超过 16 KB。|
|InvalidUserData.NotSupported|The specified parameter “UserData” only support the vpc and IoOptimized Instance.|400|UserData 只适用于 VPC 类型实例和 I/O 优化实例。|
|IncorrectInstanceStatus|The current status of the resource does not support this operation.|403|该资源目前的状态不支持此操作。|
|InstanceLockedForSecurity|The specified operation is denied as your instance is locked for security reasons.|403|实例目前被安全锁定，拒绝操作。|
|OperationDenied|The Specified operation is denied as your instance is locked for security reasons.|403|实例已经被锁定。|
|OperationDenied|The current status of the resource does not support this operation.|403|实例状态不支持该操作。|
|HOSTNAME\_ILLEGAL|hostname is not valid.|404|指定的HostName 不合法。|
|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|404|指定的 InstanceId 不存在。|
|InvalidSecurityGroupId.NotFound|The specified SecurityGroupId does not exist.|404|指定的 SecurityGroupId 不存在。|

