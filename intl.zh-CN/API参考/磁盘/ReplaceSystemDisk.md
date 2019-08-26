# ReplaceSystemDisk {#doc_api_Ecs_ReplaceSystemDisk .reference}

更换一台 ECS 实例的系统盘或者操作系统。

## 接口说明 {#description .section}

调用该接口时，您需要注意：

-   您不能更换系统盘的磁盘类型。
-   换系统盘不能修改磁盘的类型和计费方式，但是会改变系统盘的磁盘 ID，原磁盘会被释放。
-   实例的状态必须为 已停止（Stopped）状态。如果您的专有网络 VPC 类型实例开启了 VPC 内实例停机不收费功能后，为防止地域内 ECS 实例资源不足而引起更换系统盘后无法重启实例，您需要在停止实例时关闭停机不收费功能。更多详情，请参阅 [StopInstance](~~25501~~)。
-   被 [安全控制](~~25695~~) 的 ECS 实例的 OperationLocks 不能标记为 "LockReason" : "security" 。
-   实例不能为欠费状态。
-   您可以通过参数 SystemDisk.Size 重新指定系统盘的容量大小，SystemDisk.Size 的值必须大于等于 max\{20, 当前系统盘容量\}。超过 max\{20, 更换前的系统盘容量\} 的磁盘容量部分，将收取额外费用。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=ReplaceSystemDisk)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|InstanceId|String|是|i-instanceid1|指定实例的 ID。

 |
|Action|String|否|ReplaceSystemDisk|系统规定参数。取值：ReplaceSystemDisk

 |
|Architecture|String|否|i386|系统架构。取值范围：i386|x86\_64

 |
|ClientToken|String|否|123e4567-e89b-12d3-a456-426655440000|保证请求幂等性。从您的客户端生成一个参数值，确保不同请求间该参数值唯一。**ClientToken** 只支持 ASCII 字符，且不能超过 64 个字符。更多详情，请参阅 [如何保证幂等性](~~25693~~)。

 |
|DiskId|String|否|d-23b3p4r8x|根据该已有磁盘更换系统盘。

 |
|ImageId|String|否|m-imageid1|重置系统时使用的镜像 ID。

 |
|KeyPairName|String|否|JoshuaCentOS|密钥对名称。

 -   Windows ECS 实例，忽略该参数。默认为空。即使填写了该参数，仍旧只执行 Password 的内容。
-   Linux ECS 实例的密码登录方式会被初始化成禁止。

 |
|OwnerAccount|String|否|ECSforCloud@Alibaba.com|RAM 用户的账号登录名称。

 |
|Password|String|否|EcsV587!|实例的密码。长度为 8 至 30 个字符，必须同时包含大小写英文字母、数字和特殊符号中的三类字符。特殊符号可以是：

 ```

()`~!@#$%^&*-_+=|{}[]:;'<>,.?/

```

 其中，Windows 实例不能以斜线号（/）为密码首字符。

 **说明：** 如果传入`Password`参数，建议您使用HTTPS协议发送请求，避免密码泄露。

 |
|PasswordInherit|Boolean|否|false|是否使用镜像预设的密码。使用该参数时，Password参数必须为空，同时您需要确保使用的镜像已经设置了密码。

 默认值：false

 |
|Platform|String|否|CentOS|操作系统发行版。取值为CentOS、Ubuntu等。

 |
|SecurityEnhancementStrategy|String|否|Active|当指定的云盘为系统盘时，您可以设置是否开启安全加固，加载云服务器 ECS 安全组件云盾等。取值范围：

 -   Active：启用安全加固，免费安装云盾。该值仅支持公共镜像。
-   DeactiveDeactive：不启用安全加固，卸载云盾等安全组件。该值支持所有镜像。

 |
|SystemDisk.Size|Integer|否|80|新的系统盘容量，单位为 GB。取值范围：Max\{20, 参数ImageId对应的镜像大小\}~500

 默认值：Max\{40, 参数ImageId对应的镜像大小\}

 |
|UseAdditionalService|Boolean|否|true|是否使用阿里云提供的虚拟机系统配置（Windows：NTP、KMS；Linux：NTP、YUM）。

 **说明：** 挂载系统盘时（即device为/dev/xvda）有效.

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|DiskId|String|d-j6cam2z21u4ks3dj6flb|新系统盘的磁盘 ID。

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

https://ecs.aliyuncs.com/?Action=ReplaceSystemDisk
&InstanceId=i-instanceid1
&ImageId=m-imageid1
&SystemDisk.Size=80
&ClientToken=123e4567-e89b-12d3-a456-426655440000
&Password=EcsV587!
&PasswordInherit=false
&KeyPairName=JoshuaCentOS
&SecurityEnhancementStrategy=Active
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ReplaceSystemDiskResponse>
  <DiskId>d-23jbf2v5m</DiskId>
  <RequestId>F3CD6886-D8D0-4FEE-B93E-1B73239673DE</RequestId>
</ReplaceSystemDiskResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"337568C5-64F3-4B76-8CDD-D3D8C57B5B8C",
	"DiskId":"d-j6cam2z21u4ks3dj6flb"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|404|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|指定的实例不存在，请您检查实例ID是否正确。|
|400|InvalidSystemDiskSize.ValueNotSupported|The specified parameter SystemDisk.Size is invalid.|指定的 SystemDisk.Size 不合法。|
|404|InvalidInstanceId.NotFound|The specified instance does not exist.|指定的实例不存在，请您检查实例ID是否正确。|
|404|InvalidImageId.NotFound|The specified ImageId does not exist.|指定的镜像在该用户账号下不存在，请您检查镜像id是否正确。|
|403|IncorrectInstanceStatus|The current status of the resource does not support this operation.|该资源目前的状态不支持此操作。|
|403|InstanceLockedForSecurity|The instance is locked due to security.|您的资源被安全锁定，拒绝操作。|
|403|ImageNotSubscribed|The specified image has not be subscribed.|指定的镜像未在镜像市场订阅。|
|403|ImageRemovedInMarket|The specified market image is not available, Or the specified user defined image includes product code because it is based on an image subscribed from marketplace, and that image in marketplace includeing exact the same product code has been removed.|指定的云市场镜像不可用。|
|500|OperationDenied|Internal Error.|内部错误。|
|400|InvalidParameter.Conflict|The specified image does not support the specified instance type.|指定的镜像不能用于指定的实例规格。|
|404|InvalidSystemDiskSize.MoreThanMaxSize|The specified SystemDisk.Size parameter exceeds the maximum size.|指定的系统盘大小超出最大容量。|
|500|InternalError|The request processing has failed due to some unknown error.|内部错误，请重试。如果多次尝试失败，请提交工单|
|403|InstanceExpiredOrInArrears|The specified operation is denied as your prepay instance is expired \(prepay mode\) or in arrears \(afterpay mode\).|包年包月实例已过期，请您续费后再进行操作。|
|403|ChargeTypeViolation|The operation is not permitted due to charge type of the instance.|付费方式不支持该操作，请您检查实例的付费类型是否与该操作冲突。|
|403|DiskCreatingSnapshot|The operation is denied due to a snapshot of the specified disk is not completed yet.|指定的磁盘正在创建快照。|
|403|IoOptimized.NotSupported|The specified image is not support IoOptimized Instance.|指定的镜像不支持 I/O 优化型实例。|
|403|ImageNotSupportInstanceType|The specified image don not support the InstanceType instance.|指定的镜像不支持此类实例规格。|
|403|QuotaExceed.BuyImage|The specified image is from the image market,You have not bought it or your quota has been exceeded.|您暂时不能使用指定的市场镜像。|
|404|InvalidSystemDiskSize.LessThanImageSize|The specified parameter SystemDisk.Size is less than the image size.|指定的参数 SytemDisk.Size 小于镜像文件大小数值。|
|404|InvalidSystemDiskSize.LessThanMinSize|The specified parameter SystemDisk.Size is less than the min size.|指定的系统盘小于最低容量。|
|404|NoSuchResource|The specified resource is not found.|指定的资源不存在|
|400|InvalidSystemDiskSize.ImageNotSupportResize|The specified image does not support resize.|指定的镜像不支持扩容。|
|400|InvalidSystemDiskSize|The specified parameter SystemDisk.Size is invalid.|指定的 SystemDisk.Size 不合法。|
|403|INST\_HAS\_UNPAID\_ORDER|The instance has unpaid order.|该实例有未完成的账单。|
|400|InvalidSystemDiskSize.ValueNotSupported|The specified parameter SystemDisk.Size is invalid|指定的 SystemDisk.Size 不合法。|
|400|InvalidPassword.Malformed|The specified parameter "Password" is not valid.|指定的 Password 参数不合法。|
|400|InvalidPasswordParam.Mismatch|The input password should be null when passwdInherit is true.|启用PasswdInherit后，不允许指定用户名密码。|
|400|OperationDenied|The specified image contains the snapshot of the data disk,does not support this operation.|指定的镜像包含了数据盘快照的映射，不支持导出。|
|400|InvalidDiskCategory.ValueNotSupported|The specified parameter "DiskCategory" is not valid.|参数 DiskCategory 不合法。|
|403|OperationDenied.InstanceCreating|The specified instance is creating.|指定的实例已存在。|
|400|InvalidParameter.Conflict|%s|参数冲突。|
|400|InvalidSystemDiskSize.ValueNotSupported|%s|参数不支持。|
|400|InvalidKeyPairName.NotFound|The specified KeyPairName does not exist.|指定的 KeyPairName 不存在。|
|400|DependencyViolation.IoOptimize|The specified parameter InstanceId is not valid.|指定的实例 ID 不合法。|
|403|InvalidParameter.NotMatch|%s|参数冲突。|
|400|MissingParameter.Architecture|Architecture should not be null.|缺失必需参数。|
|400|InvalidArchitecture.Malformed|Architecture is not valid.|指定的参数无效。|
|400|MissingParameter.Platform|Platform should not be null.|参数缺失。|
|400|InvalidPlatform.Malformed|Platform is not valid.|指定的平台类型无效。|
|400|InvalidParameter.AllEmpty|%s|缺失必需参数。|
|400|InvalidDiskId.NotFound|The specified disk do not exist.|指定的磁盘不存在。|
|400|InvalidDatadisk.DiskStatusViolation|The operation is not permitted due to status of the Datadisk.|不支持指定的数据盘类型。|
|400|InvalidDatadisk.DiskCategoryViolation|The operation is not permitted due to category of the Datadisk.|不支持指定的数据盘类型。|
|403|ResourcesNotInSameZone|The specified instance and disk are not in the same zone.|指定的实例和磁盘不在同一可用区。|
|400|InvalidSystemDiskSize.ValueNotSupported|The specified SystemDiskSize is not valid.|指定的 SystemDisk.Size 不合法。|
|400|MissingParameter|The input parameter "ImageId" that is mandatory for processing this request is not supplied.|参数 ImageId 不得为空。|
|403|ImageNotSupportInstanceType|The specified instanceType is not supported by instance with marketplace image.|指定的市场镜像不支持该实例规格。|
|500|InternalError|The request processing has failed due to some unknown error, exception or failure.|发生未知错误。|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Ecs)

