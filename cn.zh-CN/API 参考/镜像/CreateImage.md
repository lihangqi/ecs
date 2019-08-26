# CreateImage {#CreateImage .reference}

创建一份自定义镜像。您可以使用创建的自定义镜像创建ECS实例（[RunInstances](intl.zh-CN/API 参考/实例/RunInstances.md#)）或者更换实例的系统盘（[ReplaceSystemDisk](intl.zh-CN/API 参考/磁盘/ReplaceSystemDisk.md#)）。

## 描述 {#section_yqm_y5y_xdb .section}

调用该接口时，您需要注意：

-   您需要等待镜像状态变为**可用**（`Available`）后才能使用镜像资源。

-   被[安全控制](../intl.zh-CN/API 参考/附录/安全锁定时的 API 行为.md#)的ECS实例的`OperationLocks`不能标记为`"LockReason" : "security"`。


**创建方法**

以下描述了三种通过该接口创建自定义镜像的方法。

**方法一**：针对某一台实例的系统盘创建自定义镜像，只需要指定实例系统盘的一份历史快照ID（`SnapshotId`）。其中，指定的快照不能是2013年7月15日（含）之前创建的快照。

**方法二**：使用一台实例做模板，只需要指定实例ID（`InstanceId`）。该台实例的状态必须为**运行中**（`Running`）或者**已停止**（`Stopped`）。接口调用成功后，该台实例的每块磁盘均会新增一份快照。

**方法三**：将多份磁盘快照组合成一个镜像模板，需要建立几块磁盘的数据关联（`DiskDeviceMapping`）。通过这种方法创建自定义镜像时，您需要注意：

-   只能指定一个系统盘快照，系统盘的设备名必须为/dev/xvda。

-   可以指定多个数据盘快照，数据盘设备名默认由系统有序分配，从/dev/xvdb依次排序到/dev/xvdz，不能重复。

-   可以不指定`SnapshotId`，不指定时会创建一个指定大小的没有任何数据的空数据盘。

-   指定的快照不能是2013年7月15日（含）之前创建的快照。


## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：CreateImage|
|RegionId|String|是|镜像所在的地域ID。您可以调用[DescribeRegions](../intl.zh-CN/API 参考/地域/DescribeRegions.md#)查看最新的阿里云地域列表。|
|InstanceId|String|否|实例ID。|
|SnapshotId|String|否|根据指定的快照创建自定义镜像。|
|Architecture|String|否|指定数据盘快照做镜像的系统盘后，需要通过Architecture确定系统盘的系统架构。取值范围：i386 | x86\_64（默认）|
|Platform|String|否|指定数据盘快照做镜像的系统盘后，需要通过Platform确定系统盘的的操作系统发行版。取值范围：CentOS | Ubuntu | SUSE | OpenSUSE | RedHat | Debian | CoreOS | Aliyun | Windows Server 2003 | Windows Server 2008 | Windows Server 2012 | Windows 7 | Others Linux（默认） | Customized Linux|
|DiskDeviceMapping.N.SnapshotId|String|否|`DiskDeviceMapping.N`磁盘的快照ID，N的取值范围为\[1, 17\]。|
|DiskDeviceMapping.N.DiskType|String|否|指定`DiskDeviceMapping.N.`在新镜像中的磁盘类型。您可以通过该参数使用数据盘快照做为镜像的系统盘，如果不指定，默认为快照对应的磁盘类型。取值范围：-   system：系统盘
-   data：数据盘

|
|DiskDeviceMapping.N.Size|String|否|`DiskDeviceMapping.N`磁盘的大小，单位为GiB。取值范围：\[5, 2000\]-   如果不指定磁盘大小，默认为快照（`DiskDeviceMapping.N.SnapshotId`）的大小。
-   如果没有指定快照（`DiskDeviceMapping.N.SnapshotId`），默认磁盘大小为5 GiB。
-   如果指定了磁盘大小，必须大于等于对应快照（`DiskDeviceMapping.N.SnapshotId`）的大小。

|
|ImageName|String|否|镜像名称。长度为\[2, 128\]个英文或中文字符。必须以大小字母或中文开头，不能以http://和https://开头。可以包含数字、半角冒号（:）、下划线（\_）或者连字符（-）。默认值：空。

|
|ImageVersion|String|否|镜像版本号。长度为\[1, 40\]个英文字符。|
|Description|String|否|镜像的描述信息。长度为\[2, 256\]个英文或中文字符，不能以http://和https://开头。默认值：空。

|
|Tag.n.Key|String|否|镜像的标签键。n的取值范围：\[1, 20\]。一旦传入该值，则不允许为空字符串。最多支持64个字符，不能以aliyun、acs:、http://或者https://开头。|
|Tag.n.Value|String|否|镜像的标签值。n的取值范围：\[1, 20\]。一旦传入该值，可以为空字符串。最多支持128个字符，不能以aliyun、acs:、http://或者https://开头。|
|ClientToken|String|否|保证请求幂等性。从您的客户端生成一个参数值，确保不同请求间该参数值唯一。只支持ASCII字符，且不能超过64个字符。更多详情，请参阅[如何保证幂等性](../intl.zh-CN/API 参考/附录/如何保证幂等性.md#)。

|

## 返回参数 {#ResponseParameter .section}

|名称|类型|描述|
|:-|:-|:-|
|ImageId|String|镜像ID|

## 示例 { .section}

**请求示例**

```
https://ecs.aliyuncs.com/?Action=CreateImage
&RegionId=cn-hangzhou
&SnapshotId=s-snapshot1
&ImageName=demo_image
&<公共请求参数>
```

**返回示例**

**XML格式**

```
<CreateImageResponse>
    <RequestId>C8B26B44-0189-443E-9816-D951F59623A9</RequestId>
    <ImageId>m-63DFD5FB2</ImageId>
</CreateImageResponse>
```

**JSON格式**

```
{
    "RequestId": "C8B26B44-0189-443E-9816-D951F59623A9",
    "ImageId": "m-63DFD5FB2"
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问[API错误中心](https://error-center.alibabacloud.com/status/product/Ecs)。

|错误代码|错误信息|HTTP状态码|说明|
|:---|:---|:------|:-|
| InvalidArchitecture.Malformed|The specified Architecture is wrongly formed.|400|指定的Architecture参数无效。|
|IncorrectInstanceStatus|The current status of the instance does not support this operation.|400|指定的实例状态不正确。|
|InstanceLockedForSecurity|The specified operation is denied as your instance is locked for security reasons.|400|指定的实例被安全锁定。|
|InvalidDescription.Malformed|The specified description is wrongly formed.|400|无效的`Description`取值。|
|InvalidImageName.Duplicated|The specified Image name has already been used.|400|指定的`ImageName`已经被使用。|
|InvalidImageName.Malformed|The specified Image name is wrongly formed.|400|无效的`ImageName`取值（字符不支持或者超出长度）。|
|InvalidImageVersion.Malformed|The specified ImageVersion is wrongly formed.|400|无效的`ImageVersion`取值。或者您无法使用指定的`ImageVersion`。|
|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|400|指定实例不存在。|
|InvalidInstanceId.ValueNotSupported|The specified InstanceId is not allowed to create image.|400|指定的实例不能创建快照。|
| InvalidPlatform.Malformed| The specified Platform is wrongly formed.|400| 指定的Platform参数无效。|
|InvalidSize.ValueNotSupported|The specified parameter DiskDeviceMapping.n.Size beyond the permitted range.|400|指定的`DiskDeviceMapping.n.Size`出范围。|
|MissingParameter|The input parameter SnapshotId or InstanceId or DiskDeviceMapping that is mandatory for processing this request is not supplied.|400|缺少参数`SnapshotId`、`InstanceId`或`DiskDeviceMapping`。|
|OperationDenied|The specified parameter DiskDeviceMapping.n.SnapshotId does not contain system disk snapshot.|400|参数`DiskDeviceMapping.n.SnapshotId`中必须包含系统盘快照。|
|OperationDenied|The specified parameter DiskDeviceMapping.n.SnapshotId contains two or more system disk snapshots.|400|参数`DiskDeviceMapping.n.SnapshotId`只能包含一个系统盘快照。|
|InvalidAccountStatus.NotEnoughBalance|Your account does not have enough balance.|403|账户余额不足。|
|InvalidAccountStatus.SnapshotServiceUnavailable|Snapshot service has not been opened yet.|403|快照服务未开通。|
|InvalidParamter.Conflict|The specified same token is trying to make requests with different parameters.|403|`ClientToken`和参数不一致。|
|InvalidSnapshot.TooOld|This operation is denied because the specified snapshot by DiskDeviceMapping.n.SnapshotId or SnapshotId is created before 2013-07-15.|403|指定快照创建于2013年7月15日（含）之前，不能创建镜像。|
|InvalidSnapshotId.NotReady|The current status of the DiskDeviceMapping.n.SnapshotId or SnapshotId does not support this operation.|403|指定快照的状态不对。|
|OperationDenied|The specified snapshot is not allowed to create image.|403|特定磁盘的快照不能创建镜像。|
|OperationDenied|The specified snapshot is not from system disk.|403|只有系统盘快照才能创建镜像。|
|QuotaExceed.Image|The Image Quota exceeds.|403|自定义镜像额度已用完。|
|InvalidRegionId.NotFound|The specified RegionId does not exist.|404|指定的`RegionId`不存在。|
|InvalidSnapshotId.NotFound|The specified SnapshotId does not exist.|404|找不到指定的快照。|
|InvalidSnapshotId.NotFound|The specified SnapshotId does not exist.|404|指定快照不存在。|

