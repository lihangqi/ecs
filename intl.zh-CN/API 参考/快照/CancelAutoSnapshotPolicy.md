# CancelAutoSnapshotPolicy {#CancelAutoSnapshotPolicy .reference}

取消一块或者多块磁盘的自动快照策略。

## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：CancelAutoSnapshotPolicy|
|RegionId|String|是|自动快照策略和磁盘所在的地域 ID。您可以调用 [DescribeRegions](intl.zh-CN/API参考/地域/DescribeRegions.md#) 查看最新的阿里云地域列表。|
|DiskIds|String|是|目标磁盘 ID。当您需要取消多块磁盘的自动快照策略时，多块磁盘 ID 用一个格式类似 \["d-xxxxxxxxx", "d-yyyyyyyyy", … "d-zzzzzzzzz"\] 的 JSON 数组表示，磁盘 ID 之间用半角逗号（`,`）隔开。|

## 返回参数 {#section_a3j_1yz_xdb .section}

全是公共返回参数。参阅 [公共参数](intl.zh-CN/API参考/调用方式/公共参数.md#commonResponseParameters)。

## 示例 { .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=CancelAutoSnapshotPolicy
&RegionId=cn-hangzhou
&DiskIds=["d-233e6ylv0", "d-23vbpbi03", "d-23vasz3ds"]
&<公共请求参数>
```

**返回示例** 

**XML 格式**

```
<CancelAutoSnapshotPolicyResponse>
    <RequestId>F3CD6886-D8D0-4FEE-B93E-1B73239673DE</RequestId>
</CancelAutoSnapshotPolicyResponse>
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
|ParameterInvalid|The specified DiskIds are invalid.|404|指定的 `DiskIds` 不合法。|
|ParameterInvalid|The specified RegionId parameter is invalid.|404|指定的 `RegionId` 不合法。|

