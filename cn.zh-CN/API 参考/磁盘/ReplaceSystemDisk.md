# ReplaceSystemDisk {#ReplaceSystemDisk .reference}

更换一台 ECS 实例的系统盘或者操作系统。

## 描述 {#section_lgv_qq5_xdb .section}

调用该接口时，您需要注意：

-   您不能更换系统盘的磁盘类型。

-   换系统盘不能修改磁盘的类型和付费方式，但是会改变系统盘的磁盘 ID，原磁盘会被释放。

-   实例的状态必须为 **已停止**（`Stopped`）状态。如果您的专有网络 VPC 类型实例开启了 VPC 内实例停机不收费功能后，为防止地域内 ECS 实例资源不足而引起更换系统盘后无法重启实例，您需要在停止实例时关闭停机不收费功能。更多详情，请参阅 [StopInstance](intl.zh-CN/API 参考/实例/StopInstance.md#)。

-   被 [安全控制](intl.zh-CN/API 参考/附录/安全锁定时的 API 行为.md#) 的 ECS 实例的 `OperationLocks` 不能标记为 `"LockReason" : "security"` 。

-   实例不能为欠费状态。

-   您可以通过参数 `SystemDisk.Size` 重新指定系统盘的容量大小，`SystemDisk.Size` 的值必须大于等于 max\{20, 当前系统盘容量\}。超过 max\{20, 更换前的系统盘容量\} 的磁盘容量部分，将收取额外费用。


## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：ReplaceSystemDisk|
|InstanceId|String|是|指定实例的 ID。|
|ImageId|String|是|重置系统时使用的镜像 ID。|
|Password|String|否|实例的密码。长度为 8 至 30 个字符，必须同时包含大小写英文字母、数字和特殊符号。特殊符号可以是\(\)\` ~!@\#$%^&\*-+=|\{\}\[\]:;‘<\>,.?/。其中，Windows 实例不能以斜线号（/）为密码首字符。**说明：** 如果传入 `Password` 参数，请务必使用 HTTPS 协议调用 API，避免密码泄露。

|
|PasswordInherit|Boolean|否|是否使用镜像预设的密码。使用该参数时，`Password`参数必须为空，同时您需要确保使用的镜像已经设置了密码。|
|KeyPairName|String|否|密钥对名称。-   Windows ECS 实例，忽略该参数。默认为空。即使填写了该参数，仍旧只执行 `Password` 的内容。
-   Linux ECS 实例的密码登录方式会被初始化成禁止。

|
|SystemDisk.Size|Integer|否|新的系统盘容量，单位为 GB。取值范围：\[Max\{20, 参数ImageId对应的镜像大小\}, 500\]默认值：Max\{40, 参数ImageId对应的镜像大小\}

|
|ClientToken|String|否|保证请求幂等性。从您的客户端生成一个参数值，确保不同请求间该参数值唯一。只支持ASCII字符，且不能超过64个字符。更多详情，请参阅[如何保证幂等性](../intl.zh-CN/API 参考/附录/如何保证幂等性.md#)。

|
|SecurityEnhancementStrategy|String|否|当指定的云盘为系统盘时，您可以设置是否开启安全加固，加载云服务器 ECS 安全组件云盾等。取值范围：-   Active：启用安全加固，免费安装云盾。该值仅支持公共镜像。
-   DeactiveDeactive：不启用安全加固，卸载云盾等安全组件。该值支持所有镜像。

|

## 返回参数 {#ResponseParameter .section}

|名称|类型|描述|
|:-|:-|:-|
|DiskId|String|新系统盘的磁盘 ID|

## 示例 { .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=ReplaceSystemDisk
&InstanceId=i-23jggx34b
&ImageId=m-myimage11
&<公共请求参数>
```

**返回示例** 

**XML 格式**

```
<ReplaceSystemDiskResponse>
    <DiskId>d-23jbf2v5m</DiskId>
    <RequestId>F3CD6886-D8D0-4FEE-B93E-1B73239673DE</RequestId>
</ReplaceSystemDiskResponse>
```

**JSON 格式** 

```
{
    "RequestId":"337568C5-64F3-4B76-8CDD-D3D8C57B5B8C",
    "DiskId":"d-j6cam2z21u4ks3dj6flb"
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问[API错误中心](https://error-center.alibabacloud.com/status/product/Ecs)。

|错误代码|错误信息|HTTP 状态码|说明|
|:---|:---|:-------|:-|
|InvalidParameter.Conflict|The specified image does not support the specified instance type.|400|指定的镜像不支持创建这一类规格的实例。|
|InvalidPassword.Malformed|The specified parameter “Password” is not valid.|400|指定的 `Password` 格式不合法。|
|InvalidPasswordParam.Mismatch|The input password should be null when passwdInherit is true.|400|指定了 `PasswdInherit`后，您不能指定 `Password` 参数。|
|InvalidSystemDiskSize|The specified parameter SystemDisk.Size is invalid.|400|指定的参数 `SystemDisk.Size` 不合法。|
|InvalidSystemDiskSize.ImageNotSupportResize|The specified image does not support resize.|400|指定的镜像不支持磁盘扩容。|
|InvalidSystemDiskSize.ValueNotSupported|The specified parameter SystemDisk.Size is invalid.|400|指定的参数 SystemDisk.Size 不合法。|
|OperationDenied|The specified image contains the snapshot of the data disk,does not support this operation.|400|包含数据盘快照的镜像不能进行更换系统盘操作。|
|ChargeTypeViolation|The operation is not permitted due to charge type of the instance.|403|指定实例的付费方式不支持更换系统盘。|
|DiskCreatingSnapshot|The operation is denied due to a snapshot of the specified disk is not completed yet.|403|指定的磁盘正在创建快照。|
|ImageNotSubscribed|The specified image has not be subscribed.|403|指定的镜像未在镜像市场订阅。|
|ImageNotSupportInstanceType|The specified image don not support the InstanceType instance.|403|指定镜像不支持该实例类型。|
|ImageRemovedInMarket|The specified market image is not available, Or the specified user defined image includes product code because it is based on an image subscribed from marketplace, and that image in marketplace includeing exact the same product code has been removed.|403|指定的镜像已经从镜像市场中下架。|
|IncorrectInstanceStatus|The current status of the resource does not support this operation.|403|指定的实例状态不正确。|
|INST\_HAS\_UNPAID\_ORDER|The instance has unpaid order.|403|该实例有未支付的订单。|
|InstanceExpiredOrInArrears|The specified operation is denied as your prepay instance is expired \(prepay mode\) or in arrears \(afterpay mode\).|403|指定的实例已欠费。|
|InstanceLockedForSecurity|The instance is locked due to security.|403|指定的实例被安全锁定。|
|IoOptimized.NotSupported|The specified image is not support IoOptimized Instance.|403|镜像必须支持 I/O 优化实例。|
|QuotaExceed.BuyImage|The specified image is from the image market,You have not bought it or your quota has been exceeded.|403|指定镜像来自镜像市场，您需要先购买再使用，或者您的镜像个数已超出最大限制。|
|InvalidImageId.NotFound|The specified ImageId does not exist.|404|指定的镜像不存在。|
|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|404|指定的实例不存在。|
|InvalidSystemDiskSize.LessThanImageSize|The specified parameter SystemDisk.Size is less than the image size.|404|指定的参数 `SystemDisk.Size` 小于参数 `ImageId`对应的镜像大小。|
|InvalidSystemDiskSize.LessThanMinSize|The specified parameter SystemDisk.Size is less than the min size.|404|指定的参数 SystemDisk.Size 不能小于 40 GB。|
|InvalidSystemDiskSize.MoreThanMaxSize|The specified SystemDisk.Size parameter exceeds the maximum size.|404|指定的参数 `SystemDisk.Size` 不能大于 500 GB。|
|NoSuchResource|The specified resource is not found.|404|指定资源不存在。|
|OperationDenied|Internal Error.|500|内部错误，请稍后再试。|

