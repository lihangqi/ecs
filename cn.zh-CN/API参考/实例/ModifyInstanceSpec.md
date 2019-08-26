# ModifyInstanceSpec {#doc_api_1161587 .reference}

调整一台按量付费实例的实例规格和公网带宽大小。

## 接口描述 {#description .section}

调用该接口时，您需要注意：

-   实例必须处于无欠费状态。
-   实例状态必须为 **运行中**（`Running`）或者 **已停止**（`Stopped`）时才能调节公网带宽大小。
-   升级或者降低按量付费实例规格前，您可以通过 [DescribeResourcesModification](~~66187~~) 查询当前实例支持变配的实例规格。
-   实例状态必须为 **已停止**（`Stopped`）时才能变更实例规格。
-   单次只能升级单项配置，即单次只能修改实例规格，或者只能调整公网带宽大小。
-   单台实例每成功操作一次，5分钟内不能继续操作。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=ModifyInstanceSpec)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|InstanceId|String|是|i-instanceid1|指定的实例 ID。

 |
|Action|String|否|ModifyInstanceSpec|接口名称。取值：**ModifyInstanceSpec**

 |
|AllowMigrateAcrossZone|Boolean|否|false|是否支持跨集群升级实例规格。默认值：**False**

 当参数 **AllowMigrateAcrossZone** 取值为 **True** 时，一旦您根据返回信息升级了云服务器，请留意以下注意事项：

 经典网络类型实例：

 -   对于 [已停售的实例规格](~~55263~~)，非I/O优化实例变配到I/O优化实例时，实例私网IP地址、磁盘设备名和软件授权码会发生变化。对于Linux实例，普通云盘（**cloud**）会被识别为 **xvda** 或者 **xvdb** 等，高效云盘（**cloud\_efficiency**）和SSD云盘（**cloud\_ssd**）会被识别为 **vda** 或者 **vdb** 等。
-   对于 [正常售卖的实例规格族](~~25378~~)，实例的私网 IP 地址会发生变化。

 专有网络VPC类型实例：对于 [已停售的实例规格](~~55263~~)，非 I/O 优化实例变配到 I/O 优化实例时，云服务器磁盘设备名和软件授权码会发生变化。Linux 实例的普通云盘（**cloud**）会被识别为 **xvda** 或者 **xvdb** 等，高效云盘（**cloud\_efficiency**） 和SSD云盘（`**cloud_ssd**`）会被识别为 **vda** 或者 **vdb** 等。

 |
|Async|Boolean|否|false|是否提交异步请求。

 默认值：false

 |
|InstanceType|String|否|ecs.g5.large|实例的目标规格。更多详情，请参阅 [实例规格族](~~25378~~)，也可以调用 [DescribeInstanceTypes](~~25620~~) 接口获得最新的规格表。

 |
|InternetMaxBandwidthIn|Integer|否|200|公网入带宽最大值，单位为 Mbps \(Megabit per second\)。取值范围：1~200

 |
|InternetMaxBandwidthOut|Integer|否|10|公网出带宽最大值，单位为 Mbps \(Megabit per second\)。取值范围：0~100

 |
|OwnerAccount|String|否|ECSforCloud|RAM用户的账号登录名称。

 |
|SystemDisk.Category|String|否|cloud\_ssd|更换系统盘类型。该参数只有在从 [已停售的实例规格](~~55263~~) 升级到 [正常售卖的实例规格族](~~25378~~)，并将非 I/O 优化实例规格升级为 I/O 优化实例规格时有效。取值范围：

 -   cloud\_efficiency：高效云盘
-   cloud\_ssd：SSD云盘

 |
|Temporary.EndTime|String|否|2017-12-05T22:40:00Z|临时提升带宽的截止时间点。按照 [ISO8601](~~25696~~) 标准表示，并需要使用UTC时间，格式为yyyy-MM-ddTHH:mm:ssZ。

 **说明：** 该参数即将被弃用，为提高兼容性，请尽量使用其他参数。

 |
|Temporary.InternetMaxBandwidthOut|Integer|否|50|临时公网出带宽的最大值。取值范围：1~100

 **说明：** 该参数即将被弃用，为提高兼容性，请尽量使用其他参数。

 |
|Temporary.StartTime|String|否|2017-12-05T22:40:00Z|临时提升带宽的起始时间点。按照 [ISO8601](~~25696~~) 标准表示，并需要使用UTC时间，格式为yyyy-MM-ddTHH:mm:ssZ。

 **说明：** 该参数即将被弃用，为提高兼容性，请尽量使用其他参数。

 |
|ClientToken|String|否|0c593ea1-3bea-11e9-b96b-88e9fe637760|保证请求幂等性。从您的客户端生成一个参数值，确保不同请求间该参数值唯一。**ClientToken** 只支持 ASCII 字符，且不能超过 64 个字符。更多详情，请参阅 [如何保证幂等性](~~25693~~)。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

https://ecs.aliyuncs.com/?Action=ModifyInstanceSpec
&InstanceId=i-xxxxx1
&InstanceType=ecs.s1.large
&InternetMaxBandwidthOut=10
&InternetMaxBandwidthIn=100
&ClientToken=xxxxxxxxx
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ModifyInstanceSpecResponse>
  <RequestId>04F0F334-1335-436C-A1D7-6C044FE73368</RequestId>
</ModifyInstanceSpecResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"04F0F334-1335-436C-A1D7-6C044FE73368"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InvalidInternetChargeType.ValueNotSupported|The specified InternetChargeType is not valid.|指定的实例升降配规格不存在。|
|400|InvalidInstanceType.ValueUnauthorized|The specified InstanceType does not exist or beyond the permitted range.|不支持指定的实例规格。|
|400|InvalidInstanceType.ValueNotSupported|The specified InstanceType does not exist or beyond the permitted range.|指定的实例规格不支持。|
|400|InvalidParameter.Mismatch|Too many parameters in one request.|请求中包含的参数过多。|
|403|CategoryViolation|The specified instance does not support this operation because of its disk category.|挂载有本地磁盘的实例不支持升降配。|
|403|InvalidStatus.ValueNotSupported|The current status of the resource does not support this operation.|资源当前状态不支持该操作。|
|500|InternalError|The request processing has failed due to some unknown error, exception or failure.|发生未知错误。|
|403|InvalidAccountStatus.NotEnoughBalance|Your account does not have enough balance.|账号余额不足，请您先充值再进行该操作。|
|403|ChargeTypeViolation|The operation is not permitted due to charge type of the instance.|付费方式不支持该操作，请您检查实例的付费类型是否与该操作冲突。|
|400|BandwidthUpgradeDenied.EipBoundInstance|The specified VPC instance has bound EIP, temporary bandwidth upgrade is denied.|该实例已经绑定EIP，不能进行临时升级。|
|404|MissingTemporary.StartTime|Temporary.StartTime is not specified.|未指定临时升级开始时间。|
|404|MissingTemporary.EndTime|Temporary.EndTime is not specified.|未指定临时升级结束时间。|
|400|InvalidTemporary.StartTime|The specifed Temporary.StartTime is not valid.|临时升级开始时间无效。|
|400|InvalidTemporary.EndTime|The specifed Temporary.EndTime is not valid.|临时升级结束时间无效。|
|400|Downgrade.NotSupported|Downgrade operation is not supported.|不支持降配。|
|400|DependencyViolation.InstanceType|The current InstanceType cannot be changed to the specified InstanceType.|不支持变配到指定实例规格。|
|403|InvalidInstanceType.ValueNotSupported|The specified zone does not offer the specified instancetype.|不支持指定的实例规格。|
|400|Account.Arrearage|Your account has an outstanding payment.|账号存在未支付款项。|
|400|InvalidParameter.AllowMigrateAcrossZone|The specified parameter CanMigrateAcrossZone is not valid.|跨可用区参数设置无效。|
|400|InvalidParam.SystemDiskCategory|The specified param SystemDisk.Category is not valid.|系统盘类型参数设置无效。|
|403|InstanceType.Offline|The specified InstanceType has been offline|该实例规格已下线。|
|400|IdempotenceParamNotMatch|There is a idempotence signature mismatch between this and last request.|幂等签名不一致。|
|403|InvalidParameter.NotMatch|%s|参数冲突。|
|403|InvalidInstance.EipNotSupport|The specified instance with eip is not supported, please unassociate eip first.|已绑定EIP的实例不支持该操作，请优先解绑。|
|400|InvalidAction.NotSupport|The ecs on dedicatedHost not support modify instanceType.|专用宿主机上的实例不支持变更实例规格。|
|403|InvalidOperation.Ipv4CountExceeded|%s|IPv4 个数达到上限。|
|403|InvalidOperation.Ipv6CountExceeded|%s|IPv6 个数达到上限。|
|403|InvalidOperation.Ipv6NotSupport|%s|实例规格不支持 IPv6。|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Ecs)

