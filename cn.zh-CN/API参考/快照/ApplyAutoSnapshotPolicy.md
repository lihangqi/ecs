# ApplyAutoSnapshotPolicy {#doc_api_Ecs_ApplyAutoSnapshotPolicy .reference}

为一块或者多块磁盘应用自动快照策略。目标磁盘已经应用了自动快照策略时，调用 ApplyAutoSnapshotPolicy 可以更换磁盘当前应用的自动快照策略。

## 接口说明 {#description .section}

-   一块磁盘只能应用一条自动快照策略。
-   一条自动快照策略能应用到多块磁盘。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=ApplyAutoSnapshotPolicy)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|regionId|String|是|cn-hangzhou|自动快照策略和磁盘所在的地域 ID。您可以调用 [DescribeRegions](~~25609~~) 查看最新的阿里云地域列表。

 |
|autoSnapshotPolicyId|String|是|p-233e6ylv0|目标自动快照策略 ID。

 |
|diskIds|String|是|\["d-233e6ylv0", "d-23vbpbi03", "d-23vasz3ds"\]|目标磁盘 ID。当您需要将自动快照策略应用于多块磁盘时，磁盘 ID 之间用半角逗号（,）隔开。

 |
|Action|String|否|ApplyAutoSnapshotPolicy|系统规定参数。取值：ApplyAutoSnapshotPolicy

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

https://ecs.aliyuncs.com/?Action=ApplyAutoSnapshotPolicy
&autoSnapshotPolicyId=p-233e6ylv0
&diskIds=["d-233e6ylv0", "d-23vbpbi03", "d-23vasz3ds"]
&regionId=cn-hangzhou
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ApplyAutoSnapshotPolicyResponse>
  <RequestId>F3CD6886-D8D0-4FEE-B93E-1B73239673DE</RequestId>
</ApplyAutoSnapshotPolicyResponse>

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
|404|ParameterInvalid|The specified automatic snapshot policy does not exist.|指定的自动快照策略不存在，请您检查自动快照策略是否正确。|
|404|ParameterInvalid|The specified automatic snapshot policy does not exist in the region.|指定的自动快照策略不存在，请您检查自动快照策略是否正确。|
|404|InvalidDiskId.NotFound|The specified disk does not exist in the region.|当前区域不存在该磁盘。|
|403|ParameterInvalid|The specified RegionId parameter is invalid.|指定的地域 ID 无效，请您检查该地域是否正确。|
|403|ParameterInvalid|The specified AutoSnapshotPolicyId parameter is invalid.|指定的参数自动快照 ID 不合法。|
|403|ParameterInvalid|The specified DiskIds are invalid.|指定的磁盘 ID 不合法，请您检查磁盘 ID 是否正确，且存在。|
|400|DiskCategory.OperationNotSupported|The type of the specified disk does not support creating a snapshot.|当前磁盘类型不支持此操作|
|400|PartofDiskCategory.OperationNotSupported|The types of some disks in the disk list do not support creating snapshots.|部分指定的磁盘不支持此操作|
|403|InvalidAccountStatus.NotEnoughBalance|Your account does not have enough balance.|账号余额不足，请您先充值再进行该操作。|
|403|InvalidAccountStatus.SnapshotServiceUnavailable|Snapshot service has not been opened yet.|快照服务未开通，操作无法执行。|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Ecs)

