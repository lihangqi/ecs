# CreateDisk {#doc_api_Ecs_CreateDisk .reference}

创建一块按量付费或预付费数据盘。磁盘类型包括普通云盘、高效云盘和SSD云盘。

## 接口说明 {#description .section}

-   创建磁盘会涉及到资源计费，建议您提前了解云服务器ECS的计费方式。更多详情，请参阅[计费概述](~~25398~~)。
-   创建磁盘时，默认在删除磁盘时删除其自动快照，即DeleteAutoSnapshot取值为true，可以通过 [ModifyDiskAttribute](~~25517~~)修改该参数。
-   创建的磁盘默认Portable属性为true，计费方式默认为按量付费。
-   必须指定一项请求参数Size或SnapshotId。请求参数Size指定磁盘容量大小，请求参数SnapshotId使用快照创建磁盘。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=CreateDisk)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|RegionId|String|是|cn-hangzhou|所属的地域ID。您可以调用 [DescribeRegions](~~25609~~) 查看最新的阿里云地域列表。

 |
|Action|String|否|CreateDisk|系统规定参数。取值：CreateDisk

 |
|ZoneId|String|否|cn-hangzhou-g|在指定可用区内创建一块按量付费磁盘。

 -   如果您不设置InstanceId，则ZoneId为必填参数。
-   您不能同时指定ZoneId和InstanceId。

 |
|InstanceId|String|否|i-bp1g6zv0ce8og\*\*\*\*\*\*p|创建一块预付费磁盘，并自动挂载到指定的预付费实例（InstanceId）上。

 -   设置实例ID后，会忽略您设置的ResourceGroupId、Tag.N.Key、Tag.N.Value、ClientToken和KMSKeyId参数。
-   您不能同时指定ZoneId和InstanceId。

 默认值：空，代表创建的是按量付费磁盘，磁盘所属地由RegionId和ZoneId确定。

 |
|SnapshotId|String|否|s-snapshot1|创建磁盘使用的快照。指定该参数后，Size会被忽略，实际创建的磁盘大小为指定快照的大小。2013年7月15日及以前的快照不能用来创建磁盘。

 |
|DiskCategory|String|否|cloud\_ssd|数据盘的磁盘种类。取值范围：

 -   cloud：普通云盘
-   cloud\_efficiency：高效云盘
-   cloud\_ssd：SSD 云盘
-   cloud\_essd：ESSD 云盘。目前 ESSD 云盘正在火热公测中，仅部分地域下的可用区可以选购。更多详情，请参阅 [ESSD 云盘 FAQ](~~64950~~)。

 默认值：cloud

 |
|Size|Integer|否|2000|容量大小，以GiB为单位。指定该参数后，其取值必须≥指定快照ID的容量大小。取值范围：

 -   cloud：5~2000
-   cloud\_efficiency：20~32768
-   cloud\_ssd：20~32768
-   cloud\_essd：20~32768

 |
|DiskName|String|否|FinanceJoshua|磁盘名称。长度为 2~128 个英文或中文字符。必须以大小字母或中文开头，不能以 http:// 和 https:// 开头。可以包含数字、半角冒号（:）、下划线（\_）或者连字符（-）。默认值：空。

 |
|Encrypted|Boolean|否|false|是否加密云盘。默认值：false

 |
|Description|String|否|FinanceDisk|磁盘描述。长度为 2~256 个英文或中文字符，不能以 http:// 和 https:// 开头。默认值：空。

 |
|Tag.N.Key|String|否|FinanceDept|磁盘的标签键。N 的取值范围：1~20。一旦传入该值，则不允许为空字符串。最多支持 64 个字符，不能以 aliyun 和 acs: 开头，不能包含 http:// 或者 https:// 。

 |
|Tag.N.Value|String|否|FinanceDeptJoshua|磁盘的标签值。N 的取值范围：1~20。一旦传入该值，可以为空字符串。最多支持 128 个字符，不能以 aliyun 和 acs: 开头，不能包含 http:// 或者 https:// 。

 |
|ResourceGroupId|String|否|rg-resourcegroupid1|磁盘所在的企业资源组 ID。

 |
|KMSKeyId|String|否|0e478b7a-4262-4802-b8cb-00d3fb40826X|磁盘使用的KMS密钥ID。

 |
|ClientToken|String|否|123e4567-e89b-12d3-a456-426655440000|保证请求幂等性。从您的客户端生成一个参数值，确保不同请求间该参数值唯一。**ClientToken** 只支持 ASCII 字符，且不能超过 64 个字符。更多详情，请参阅 [如何保证幂等性](~~25693~~)。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|DiskId|String|d-bp131n0q38u3a4zi\*\*\*\*\*|磁盘ID。

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

https://ecs.aliyuncs.com/?Action=CreateDisk
&RegionId=cn-hangzhou
&ZoneId=cn-hangzhou-g
&SnapshotId=s-snapshot1
&DiskName=FinanceJoshua
&Size=2000
&DiskCategory=cloud_ssd
&Description=FinanceDisk
&Encrypted=false
&ClientToken=123e4567-e89b-12d3-a456-426655440000
&Tag.1.Key=FinanceDept
&Tag.1.Value=FinanceDeptJoshua
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<CreateDiskResponse>
  <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
  <DiskId>d-bp131n0q38u3a4zi*****</DiskId>
</CreateDiskResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E",
	"DiskId":"d-bp131n0q38u3a4zi*****"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InvalidSize.ValueNotSupported|The specified parameter Size is not valid.|指定的 Size 不合法。|
|403|InvalidDataDiskCategory.NotSupported|Specified disk category is not supported.|不支持指定的磁盘种类。|
|404|InvalidRegionId.NotFound|The specified RegionId does not exist.|指定的 RegionId 不存在，请您检查此产品在该地域是否可用。|
|404|InvalidZoneId.NotFound|The specified zone does not exist.|指定的可用区不存在。|
|404|InvalidSnapshotId.NotFound|The specified SnapshotId does not exist.|指定的快照不存在，请您检查快照是否正确。|
|400|InvalidDiskName.Malformed|The specified disk name is wrongly formed.|磁盘名称格式不正确。长度为2-128个字符，以英文字母或中文开头，可包含数字，"."，"\_"或"-"。 不能以 http:// 和 https:// 开头。|
|400|InvalidDescription.Malformed|The specified description is wrongly formed.|指定的资源描述格式不合法。长度为2-256个字符，不能以 http:// 和 https:// 开头。|
|403|InstanceDiskCategoryLimitExceed|The total size of specified disk category in an instance exceeds.|磁盘种类总容量超过实例限制。|
|403|InvalidSnapshot.NotReady|The specified snapshot creation is not completed yet.|指定快照未创建。|
|403|InvalidSnapshot.TooOld|This operation is forbidden because the specified snapshot is created before 2013-07-15.|指定磁盘的源快照创建于2013年7月15日（含）之前，不能重新初始化。|
|403|InvalidSnapshot.TooLarge|The capacity of snapshot exceeds 2000GB.|快照容量超过 2000 GB。|
|403|OperationDenied|The specified snapshot is not allowed to create disk.|指定快照不支持创建磁盘。|
|403|QuotaExceed.PortableCloudDisk|The quota of portable cloud disk exceeds.|可卸载磁盘数量已达上限。|
|400|MissingParameter|The input parameter either "SnapshotId" or "Size" should be specified.|参数 SnapshotId 或 Size 至少一项不得为空。|
|403|InvalidDiskCategory.ValueUnauthorized|The disk category is not authorized.|该磁盘种类未经授权。|
|403|InvalidSnapshotId.NotReady|The specified snapshot has not completed yet.|指定的快照未完成。|
|403|InvalidSnapshotId.NotDataDiskSnapshot|The specified snapshot is system disk snapshot.|指定的快照为系统磁盘快照。|
|403|InvalidDiskSize.TooSmall|Specified disk size is less than the size of snapshot.|指定的磁盘容量小于快照容量。|
|403|OperationDenied|The type of the disk does not support the operation.|此磁盘种类不支持指定的操作。|
|403|InvalidDataDiskCategory.NotSupported|%s|不支持指定的数据盘类型。|
|403|InvalidDiskSize.NotSupported|disk size is not supported.|磁盘大小不合法。|
|400|InvalidDiskCategory.NotSupported|The specified disk category is not support.|不支持的磁盘种类。|
|400|Account.Arrearage|Your account has an outstanding payment.|账号存在未支付款项。|
|400|InvalidDiskCategory.ValueNotSupported|The specified parameter "DiskCategory" is not valid.|参数 DiskCategory 不合法。|
|403|InvalidAccountStatus.NotEnoughBalance|Your account does not have enough balance.|账号余额不足，请您先充值再进行该操作。|
|403|InvalidAccountStatus.SnapshotServiceUnavailable|Snapshot service has not been opened yet.|快照服务未开通，操作无法执行。|
|400|InvalidDataDiskCategory.ValueNotSupported|%s|参数不支持。|
|400|InvalidParameter.Conflict|%s|参数冲突。|
|400|RegionUnauthorized|%s|指定地域不支持。|
|500|InternalError|The request processing has failed due to some unknown error.|内部错误，请重试。如果多次尝试失败，请提交工单|
|400|Zone.NotOnSale|%s|可用区关闭。|
|400|InvalidDataDiskSize.ValueNotSupported|%s|参数不支持。|
|403|InvalidPayMethod|The specified pay method is not valid.|没有可用的付费方式|
|400|OperationDenied|The specified Zone is not available or not authorized.|指定的可用区不可用或未授权。|
|404|InvalidResourceGroup.NotFound|The ResourceGroup provided does not exist in our records.|资源组并不在记录中。|
|403|InvalidDiskCategory.NotSupported|The specified disk category is not supported.|该云盘类型不支持。|
|403|InvalidDiskSize.NotSupported|The specified disk size is not supported.|指定的磁盘容量不支持。|
|400|InvalidDiskSize.NotSupported|The specified parameter size is not valid.|指定的容量参数无效。|
|403|UserNotInTheWhiteList|The user is not in disk white list.|您暂时不能使用该磁盘服务。|
|400|InvalidDiskSizeOrCategory|The specified disk category or size is invalid.|指定的磁盘类别或大小无效。|
|400|InvalidParameter.EncryptedIllegal|%s|参数不支持（加密盘）。|
|400|InvalidParameter.EncryptedNotSupported|%s|参数不支持（加密盘）。|
|400|EncryptedOption.Conflict|%s|参数不支持（加密盘）。|
|400|InvalidParameter.Encrypted.KmsNotEnabled|The encrypted disk need enable KMS|加密磁盘需要启用密钥管理服务。|
|500|InternalError|The request processing has failed due to some unknown error, exception or failure.|发生未知错误。|
|403|QuotaExceed.PostPaidDisk|Living postPaid disks quota exceeded.|按量付费磁盘数量已超出允许数量。|
|403|InvalidRegion.NotSupport|The specified region does not support byok.|该地域不支持BYOK。|
|403|UserNotInTheWhiteList|The user is not in byok white list.|您暂时不能使用BYOK服务。|
|400|InvalidParameter.EncryptedIllegal|The specified parameter Encrypted must be true when kmsKeyId is not empty.|设置KmsKeyId后，您必须开启加密属性。|
|404|InvalidParameter.KMSKeyId.NotFound|The specified KMSKeyId does not exist.|指定的参数值不存在。|
|403|InvalidParameter.KMSKeyId.KMSUnauthorized|ECS service have no right to access your KMS.|ECS未被授权访问您的KMS资源。|
|403|SecurityRisk.3DVerification|We have detected a security risk with your default credit or debit card. Please proceed with verification via the link in your email.|您的支付方式有安全风险，请根据通知指导排查。|
|400|Duplicate.TagKey|The Tag.N.Key contain duplicate key.|标签键中存在重复的键。|
|400|InvalidTagKey.Malformed|The specified Tag.n.Key is not valid.|指定的标签键不合法。|
|400|InvalidTagValue.Malformed|The specified Tag.n.Value is not valid.|指定的标签值不合法。|
|404|InvalidInstanceId.NotFound|The InstanceId provided does not exist in our records.|指定的实例不存在，请您检查实例ID是否正确。|
|403|InvalidStatus.Upgrading|The instance is upgrading; please try again later.|实例正在升级，请稍后重试。|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Ecs)

