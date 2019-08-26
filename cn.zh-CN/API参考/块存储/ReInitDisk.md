# ReInitDisk {#doc_api_Ecs_ReInitDisk .reference}

调用ReInitDisk重新初始化一块云盘到创建时的初始状态。

## 接口说明 {#description .section}

调用该接口时，您需要注意：

-   云盘的状态必须为**使用中**（In\_use），且挂载的ECS实例的状态必须为**已停止** （Stopped）。
-   实例首次启动前，不能重新初始化挂载在其上的云盘。
-   对于系统盘，初始化到镜像的最初状态。若创建云盘的源镜像被删除，则无法初始化。
-   对于直接创建的数据盘，初始化到空盘状态。
-   对于通过快照创建的数据盘，初始化到快照状态。若源快照已被删除，则无法初始化并返回错误。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=ReInitDisk&type=RPC&version=2014-05-26)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|DiskId|String|是|d-diskid1|指定的云盘ID。

 |
|Action|String|否|ReInitDisk|系统规定参数。取值：ReInitDisk

 |
|AutoStartInstance|Boolean|否|true|重新初始化云盘后是否启动实例。

 |
|KeyPairName|String|否|JoshuaCentOS|密钥对名称。

 |
|Password|String|否|EcsV587!|实例的密码。长度为8至30个字符，必须同时包含大小写英文字母、数字和特殊符号中的三类字符。特殊符号可以是：

 ```

()`~!@#$%^&*-_+=|{}[]:;'<>,.?/

```

 其中，Windows实例不能以斜线号（/）为密码首字符。

 **说明：** 如果传入`Password`参数，建议您使用HTTPS协议发送请求，避免密码泄露。

 |
|SecurityEnhancementStrategy|String|否|Active|当指定的云盘为系统盘时，您可以设置是否开启安全加固，加载云服务器 ECS 安全组件云盾等。取值范围：

 -   Active：启用安全加固，免费安装云盾。该值仅支持公共镜像。
-   Deactive：不启用安全加固，卸载云盾等安全组件。该值支持所有镜像。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=ReInitDisk
&DiskId=d-diskid1
&Password=EcsV587!
&KeyPairName=JoshuaCentOS
&AutoStartInstance=true
&SecurityEnhancementStrategy=Active
&<公共请求参数>
```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ReInitDiskResponse>
      <RequestId>F3CD6886-D8D0-4FEE-B93E-1B73239673DE</RequestId>
</ReInitDiskResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"F3CD6886-D8D0-4FEE-B93E-1B73239673DE"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|404|InvalidDiskId.NotFound|The specified disk does not exist.|指定的磁盘不存在。请您检查磁盘 ID 是否正确。|
|403|IncorrectDiskStatus|The current disk status does not support this operation.|当前的磁盘不支持此操作，请您确认磁盘处于正常使用状态，是否欠费。|
|403|IncorrectInstanceStatus|The current status of the resource does not support this operation.|该资源目前的状态不支持此操作。|
|403|InstanceLockedForSecurity|The instance is locked due to security.|您的资源被安全锁定，拒绝操作。|
|403|InvalidSnapshot.TooOld|The disk is created from a snapshotId made before 2013-07-15, it cannot be re-initiated the specified disk any more since the detached first time.|指定的快照创建时间不能晚于2013年7月15日。|
|403|OperationDenied|The snapshot which is used to create the specified disk has been deleted.|用来创建指定磁盘的快照不存在。|
|403|InstanceExpiredOrInArrears|The specified operation is denied as your prepay instance is expired \(prepay mode\) or in arrears \(afterpay mode\).|包年包月实例已过期，请您续费后再进行操作。|
|403|DiskCreatingSnapshot|The operation is denied due to a snapshot of the specified disk is not completed yet.|指定的磁盘正在创建快照。|
|403|InvalidSourceSnapshot|The snapshot which is used to create the specified disk has been deleted.|用于创建指定磁盘的快照已被删除。|
|404|InvalidImageId.NotFound|The specified ImageId does not exist.|指定的镜像在该用户账号下不存在，请您检查镜像id是否正确。|
|403|SharedImageDeleted|The specified image by others shared is deleted.|指定的共享镜像已删除。|
|400|InvalidPassword.Malformed|The specified parameter "Password" is not valid.|指定的 Password 参数不合法。|
|400|DiskCategory.OperationNotSupported|The operation is not supported to the specified disk due to its disk category|由于磁盘种类限制，指定的磁盘不支持该操作。|
|400|InvalidKeyPairName.NotFound|The specified KeyPairName does not exist.|指定的 KeyPairName 不存在。|
|400|DependencyViolation.IoOptimize|The specified parameter InstanceId is not valid.|指定的实例 ID 不合法。|
|403|UserNotInTheWhiteList|The user is not in volume white list.|用户不在共享块存储白名单中，请您提交工单申请白名单。|
|400|InvalidRegionId.MalFormed|The specified RegionId is not valid|指定的 RegionId 不合法。|
|404|InvalidDiskId.OperationNotSupported|The operation is not supported due to image not exist.|指定的镜像不存在。|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

