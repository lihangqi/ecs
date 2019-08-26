# CreateDisk {#CreateDisk .reference}

创建一块按量付费数据盘。磁盘类型包括普通云盘、高效云盘和SSD云盘。

## 描述 {#section_szb_3l5_xdb .section}

-   创建磁盘会涉及到资源计费，建议您提前了解云服务器ECS的计费方式。更多详情，请参阅[计费概述](../intl.zh-CN/产品定价/计费概述.md#)。

-   创建磁盘时，默认在删除磁盘时删除其自动快照，即`DeleteAutoSnapshot`取值为`true`，可以通过[ModifyDiskAttribute](intl.zh-CN/API 参考/磁盘/ModifyDiskAttribute.md#)修改该参数。

-   创建的磁盘默认`Portable`属性为`true`，计费方式默认为按量付费。

-   必须指定一项请求参数`Size`或`SnapshotId`。请求参数`Size`指定磁盘容量大小，请求参数`SnapshotId`使用快照创建磁盘。


## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：CreateDisk|
|RegionId|String|是|所属的地域ID。您可以调用[DescribeRegions](../intl.zh-CN/API 参考/地域/DescribeRegions.md#)查看最新的阿里云地域列表。|
|ZoneId|String|是|可用区ID。|
|DiskName|String|否|磁盘名称。长度为\[2, 128\]个英文或中文字符。必须以大小字母或中文开头，不能以http://和https://开头。可以包含数字、半角冒号（:）、下划线（\_）或者连字符（-）。默认值：空。

|
|Description|String|否|磁盘描述。长度为\[2, 256\]个英文或中文字符，不能以http://和https://开头。默认值：空。

|
|Encrypted|Boolean|否|是否加密。默认值：false|
|DiskCategory|String|否|数据盘的磁盘种类。取值范围：-   cloud：普通云盘
-   cloud\_efficiency：高效云盘
-   cloud\_ssd：SSD云盘

默认值：cloud|
|Size|Integer|否|容量大小，以GiB为单位。指定该参数后，其取值必须≥指定快照ID的容量大小。取值范围：-   cloud：\[5, 2000\]
-   cloud\_efficiency：\[20, 32768\]
-   cloud\_ssd：\[20, 32768\]

|
|SnapshotId|String|否|创建磁盘使用的快照。指定该参数后，`Size`会被忽略，实际创建的磁盘大小为指定快照的大小。2013年7月15日及以前的快照不能用来创建磁盘。|
|Tag.n.Key|String|否|磁盘的标签键。n的取值范围：\[1, 20\]。一旦传入该值，则不允许为空字符串。最多支持64个字符，不能以aliyun、acs:、http://或者https://开头。|
|Tag.n.Value|String|否|磁盘的标签值。n的取值范围：\[1, 20\]。一旦传入该值，可以为空字符串。最多支持128个字符，不能以aliyun、acs:、http://或者https://开头。|
|ClientToken|String|否|保证请求幂等性。从您的客户端生成一个参数值，确保不同请求间该参数值唯一。只支持ASCII字符，且不能超过64个字符。更多详情，请参阅[如何保证幂等性](../intl.zh-CN/API 参考/附录/如何保证幂等性.md#)。

|

## 返回参数 {#ResponseParameter .section}

|名称|类型|描述|
|:-|:-|:-|
|DiskId|String|磁盘ID|

## 示例 { .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=CreateDisk
&RegionId=cn-qingdao
&ZoneId=cn-qingdao-b
&Size=200
&DiskName=ThisIsDiskName
&Description=ThisIsDescription
&<公共请求参数>
```

**返回示例** 

**XML格式**

```
<CreateDiskResponse>
    <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
    <DiskId>d-bp131n0q38u3a4ziXXXXX</DiskId>
</CreateDiskResponse>
```

**JSON格式** 

```
{
    "RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E",
    "DiskId": "d-bp131n0q38u3a4ziXXXXX"
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问[API错误中心](https://error-center.alibabacloud.com/status/product/Ecs)。

|错误代码|错误信息|HTTP状态码|说明|
|:---|:---|:------|:-|
|Account.Arrearage|Your account has an outstanding payment.|400|您的账号余额不足，请更新账号状态后重试。|
|InvalidDescription.Malformed|The specified description is wrongly formed.|400|指定的`DescriptionName`格式不合法。|
|InvalidDiskCategory.NotSupported|The specified disk category is not support.|400|指定的磁盘类型不支持。|
|InvalidDiskCategory.ValueNotSupported|The specified parameter DiskCategory is not valid.|400|指定的`DiskCategory`不合法。|
|InvalidDiskName.Malformed|The specified disk name is wrongly formed.|400|指定的`DiskName`格式不合法。|
|EncryptedOption.Conflict|Encryption value of disk conflicts with that of snapshot .|400|磁盘的加密属性和快照的加密属性不一致。|
|InvalidParameter.Encrypted.KmsNotEnabled|The encrypted disk need enable KMS.|400|账户未开通KMS服务（需用户主动开通KMS服务）。|
|InvalidParameter.EncryptedIllegal|The value of parameter encrypted is illegal.|400|传入的参数`Encrypted`非法。|
|InvalidParameter.EncryptedNotSupported|Encrypted disk is not support in this region.|400|所选择的地域不支持加密特性。|
|InvalidParameter.EncryptedNotSupported|Corresponding data disk category does not support encryption.|400|对应的磁盘类型不支持加密。|
|InvalidSize.ValueNotSupported|The specified parameter Size is not valid.|400|指定的`Size`不合法。|
|MissingParameter|The input parameter either SnapshotId or Size should be specified.|400|`SnapshotId`或者`Size`参数未指定。|
|InstanceDiskCategoryLimitExceed|The total size of specified disk category in an instance exceeds.|403|指定的磁盘种类超过了单实例的最大容量。|
|InvalidAccountStatus.NotEnoughBalance|Your account does not have enough balance.|403|账户余额不足。|
|InvalidAccountStatus.SnapshotServiceUnavailable|Snapshot service has not been opened yet.|403|快照服务未开通。|
|InvalidDataDiskCategory.NotSupported|Specified disk category is not supported.|403|指定的磁盘类型不支持。|
|InvalidDataDiskCategory.NotSupported|diskCategory is CLOUD\_SSD, but the supported DiskCategory is \[io1, io4, io3\].|403|指定的磁盘类型不支持。|
|InvalidDiskCategory.ValueUnauthorized|The disk category is not authorized.|403|指定磁盘种类无权限。|
|InvalidDiskSize.NotSupported|disk size is not supported.|403|指定的磁盘大小不支持。|
|InvalidDiskSize.TooSmall|Specified disk size is less than the size of snapshot.|403|指定的磁盘小于指定快照大小。|
|InvalidSnapshot.NotReady|The specified snapshot creation is not completed yet.|403|指定的快照还在创建中。|
|InvalidSnapshot.TooLarge|The capacity of snapshot exceeds 2000GB.|403|指定快照的容量超过磁盘种类的最大容量。|
|InvalidSnapshot.TooOld|This operation is forbidden because the specified snapshot is created before 2013-07-15.|403|指定快照创建于2013年7月15日（含）之前，不能创建磁盘。|
|InvalidSnapshotId.NotReady|The specified snapshot has not completed yet.|403|指定的快照未完成。|
|OperationDenied|The specified snapshot is not allowed to create disk.|403|指定快照不允许创建磁盘。|
|OperationDenied|The type of the disk does not support the operation.|403|指定磁盘类型不支持该操作。|
|QuotaExceed.PortableCloudDisk|The quota of portable cloud disk exceeds.|403|可卸载普通云盘超过额度。|
|InvalidRegionId.NotFound|The specified RegionId does not exist.|404|指定的`RegionId`不存在。|
|InvalidRegionId.NotFound|The specified RegionId does not exist.|404|指定的`RegionId`不存在。|
|InvalidSnapshotId.NotFound|The specified SnapshotId does not exist.|404|找不到指定的快照。|
|InvalidZoneId.NotFound|The specified zone does not exist.|404|指定的`ZoneId`不存在。|

