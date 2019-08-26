# ApplyAutoSnapshotPolicy {#ApplyAutoSnapshotPolicy .reference}

为一块或者多块磁盘应用自动快照策略。目标磁盘已经应用了自动快照策略时，调用 ApplyAutoSnapshotPolicy 可以更换磁盘当前应用的自动快照策略。

## 描述 {#section_idr_vwz_xdb .section}

调用该接口时，您需要注意：

-   一块磁盘只能应用一条自动快照策略。

-   一条自动快照策略能应用到多块磁盘。

-   如果某一时间点有大量自动快照任务，会有短暂的排队等待时间，大约为零至三分钟，因此不能保证该时间点的自动快照任务能同时进行。


## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：ApplyAutoSnapshotPolicy|
|RegionId|String|是|自动快照策略和磁盘所在的地域 ID。您可以调用 [DescribeRegions](intl.zh-CN/API参考/地域/DescribeRegions.md#) 查看最新的阿里云地域列表。|
|AutoSnapshotPolicyId|String|是|目标自动快照策略 ID。|
|DiskIds|String|是|目标磁盘 ID。当您需要将自动快照策略应用于多块磁盘时，多块磁盘 ID 用一个格式类似 \["d-xxxxxxxxx", "d-yyyyyyyyy", … "d-zzzzzzzzz"\] 的 JSON 数组表示，磁盘 ID 之间用半角逗号（`,`）隔开。|

## 返回参数 {#section_odr_vwz_xdb .section}

全是公共返回参数。参阅 [公共参数](intl.zh-CN/API参考/调用方式/公共参数.md#commonResponseParameters)。

## 示例 { .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=ApplyAutoSnapshotPolicy
&RegionId=cn-hangzhou
&AutoSnapshotPolicyId=p-233e6ylv0
&DiskIds=["d-233e6ylv0", "d-23vbpbi03", "d-23vasz3ds"]
&<公共请求参数>
```

**返回示例** 

**XML 格式**

```
<ApplyAutoSnapshotPolicyResponse>
    <RequestId>F3CD6886-D8D0-4FEE-B93E-1B73239673DE</RequestId>
</ApplyAutoSnapshotPolicyResponse>
```

 **JSON 格式** 

```
{
    "RequestId":"F3CD6886-D8D0-4FEE-B93E-1B73239673DE"
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问 [API 错误中心](https://error-center.alibabacloud.com/status/product/Ecs)。

|错误代码|错误信息|HTTP 状态码|说明|
|:---|:---|:-------|:-|
|DiskCategory.OperationNotSupported|The type of the specified disk does not support creating a snapshot.|400|本地盘无法创建快照。更多详情，请参阅 [本地存储](../intl.zh-CN/产品简介/块存储/本地存储.md#)。|
|DiskCategory.OperationNotSupported|The types of some disks in the disk list do not support creating snapshots.|400|指定的磁盘列表 `DiskIds` 中含有本地盘，无法创建快照。|
|ParameterInvalid|The specified automatic snapshot policy does not exist.|404|指定的 `AutoSnapshotPolicyId`不存在。|
|ParameterInvalid|The specified automatic snapshot policy does not exist in the region.|404|指定的 `AutoSnapshotPolicyId`在指定地域中不存在。|
|ParameterInvalid|The specified AutoSnapshotPolicyId parameter is invalid.|404|指定的 `AutoSnapshotPolicyId`不合法。|
|ParameterInvalid|The specified DiskIds are invalid.|404|指定的 `DiskIds` 不合法。|
|ParameterInvalid|The specified RegionId parameter is invalid.|404|指定的 `RegionId` 不合法。|

