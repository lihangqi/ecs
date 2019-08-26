# ResizeDisk {#doc_api_Ecs_ResizeDisk .reference}

调用ResizeDisk扩容一块云盘，支持扩容系统盘和数据盘。

## 接口说明 {#description .section}

**说明：** 扩容前，请务必查询云盘采用的分区格式。如果是MBR格式，不支持扩容到2TiB以上，否则会造成数据丢失。对于MBR分区扩容，建议您重新创建并挂载一块数据盘，采用GPT分区格式后，再将已有数据拷贝至新的数据盘上。更多详情，请参见[扩容云盘容量](~~44986~~)。

-   支持扩容的云盘类型包括普通云盘（cloud）、高效云盘（cloud\_efficiency）、SSD云盘（cloud\_ssd）和ESSD（cloud\_essd）云盘。
-   当云盘正在创建快照时，不允许扩容。
-   云盘挂载的实例的状态必须为运行中（Running）或者已停止（Stopped）。
-   扩容时，不会修改云盘分区和文件系统，您需要在扩容后自行分配存储空间。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=ResizeDisk&type=RPC&version=2014-05-26)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|DiskId|String|是|d-diskid|云盘ID。

 |
|NewSize|Integer|是|1900|希望扩容到的云盘容量大小。单位为GiB。取值范围：

 -   普通云盘（cloud）：5~2000
-   高效云盘（cloud\_efficiency）：20~6144
-   SSD云盘（cloud\_ssd）：20~6144
-   ESSD云盘（cloud\_essd）：20~32768

 指定的新云盘容量必须比原云盘容量大。且6TiB以下的云盘不能扩容到6TiB以上。

 |
|Action|String|否|ResizeDisk|系统规定参数。对于您自行拼凑HTTP/HTTPS URL发起的API请求，`Action`为必选参数。取值：ResizeDisk

 |
|Type|String|否|offline|扩容云盘的方式。取值范围：

 -   offline（默认）：离线扩容。扩容后，您需要在控制台[重启实例](~~25440~~)或者调用API [RebootInstance](~~25502~~)使操作生效。
-   online：在线扩容，无需重启实例即可完成扩容。云盘类型支持高效云盘和SSD云盘。

 |
|ClientToken|String|否|123e4567-e89b-12d3-a456-426655440000|保证请求幂等性。从您的客户端生成一个参数值，确保不同请求间该参数值唯一。**ClientToken**只支持ASCII字符，且不能超过64个字符。更多详情，请参见[如何保证幂等性](~~25693~~)。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=ResizeDisk
&DiskId=d-diskid
&NewSize=1900
&ClientToken=123e4567-e89b-12d3-a456-426655440000
&<公共请求参数>
```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ResizeDiskResponse>
      <RequestId>F3CD6886-D8D0-4FEE-B93E-1B73239673DE</RequestId>
</ResizeDiskResponse>
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
|403|InvalidDataDiskSize.ValueNotSupported|The specified DataDisk.n.Size beyond the permitted range, or the capacity of snapshot exceeds the size limit of the specified disk category.|指定的数据盘大小已超过最大允许值。|
|404|InvalidDiskId.NotFound|The specified disk does not exist.|指定的磁盘不存在。请您检查磁盘 ID 是否正确。|
|404|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|指定的实例不存在，请您检查实例ID是否正确。|
|403|OperationDenied|The type of the disk does not support the operation.|此磁盘种类不支持指定的操作。|
|403|OperationDenied|The status of the disk or the instance that the disk is attaching with does not support the operation.|此磁盘或实例状态无法执行指定的操作。|
|403|InvalidDiskSize.TooSmall|Specified new disk size is less than the original disk size.|指定的新磁盘小于原始磁盘。|
|403|InvalidDiskSize.TooLarge|Specified new disk size is beyond the permitted range.|指定的新磁盘大小超过限制。|
|403|InstanceExpiredOrInArrears|The specified operation is denied as your prepay instance is expired \(prepay mode\) or in arrears \(afterpay mode\).|包年包月实例已过期，请您续费后再进行操作。|
|403|DiskError|IncorrectDiskStatus|指定的磁盘状态不合法。|
|403|DiskInArrears|The specified operation is denied as your disk owing fee.|指定的磁盘已欠费。|
|403|IncorrectInstanceStatus|The current status of the resource does not support this operation.|该资源目前的状态不支持此操作。|
|500|InternalError|The request processing has failed due to some unknown error.|内部错误，请重试。如果多次尝试失败，请提交工单|
|403|DiskCreatingSnapshot|The operation is denied due to a snapshot of the specified disk is not completed yet.|指定的磁盘正在创建快照。|
|400|InvalidDataDiskCategory.ValueNotSupported|%s|参数不支持。|
|400|InvalidParameter.Conflict|%s|参数冲突。|
|400|InvalidDataDiskSize.ValueNotSupported|%s|参数不支持。|
|403|InvalidDiskSize|Specified new disk size is less than or equal the original disk size.|指定的新磁盘大小必须要小于或等于原始磁盘大小。|
|400|IncompleteParamter|Some fields can not be null in this request.|请求中缺失参数。|
|403|Operation.Conflict|The operation may conflicts with others.|该操作与其他操作冲突。|
|403|InstanceLockedForSecurity|The instance is locked due to security.|您的资源被安全锁定，拒绝操作。|
|403|IncorrectDiskStatus|The current disk status does not support this operation.|当前的磁盘不支持此操作，请您确认磁盘处于正常使用状态，是否欠费。|
|403|UserNotInTheWhiteList|The user is not in disk white list.|您暂时不能使用该磁盘服务。|
|400|InvalidRegionId.MalFormed|The specified RegionId is not valid|指定的 RegionId 不合法。|
|403|InvalidDiskCategory.NotSupported|The specified disk category is not supported.|该云盘类型不支持。|
|400|InvalidParam.Type|The specified type is not supported.|指定的参数无效。|
|403|InvalidRegion.NotSupport|The specified region does not support resize online.|该地域不支持在线扩容。|
|403|InvalidDiskCategory.NotSupported|The specified disk category does not support resize online.|指定的磁盘类型不支持在线扩容。|
|403|IncorrectInstanceStatus|The current status of the resource does not support resize online.|资源的当前状态不支持该操作。|
|403|IncorrectDiskStatus|The current status of the resource does not support resize online|该资源的状态不支持在线扩容磁盘。|
|403|InvalidOperation.InstanceTypeNotSupport|The instance type of the specified instance does not support resize online.|磁盘挂载的实例不支持磁盘在线扩容操作。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ecs)查看更多错误码。

