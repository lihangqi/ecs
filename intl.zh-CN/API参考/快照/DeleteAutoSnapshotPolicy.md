# DeleteAutoSnapshotPolicy {#DeleteAutoSnapshotPolicy .reference}

删除一条自动快照策略。如果目标自动快照策略已经被应用到磁盘上，删除自动快照策略后，这些磁盘不再执行该策略。

## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：DeleteAutoSnapshotPolicy|
|RegionId|String|是|自动快照策略所在的地域 ID。您可以调用 [DescribeRegions](intl.zh-CN/API参考/地域/DescribeRegions.md#) 查看最新的阿里云地域列表。|
|AutoSnapshotPolicyId|String|是|自动快照策略的 ID。您可以调用 [DescribeAutoSnapshotPolicyEx](intl.zh-CN/API参考/快照/DescribeAutoSnapshotPolicyEx.md#) 查看您可用的自动快照策略。|

## 返回参数 {#section_byv_lyz_xdb .section}

全是公共返回参数。参阅 [公共参数](intl.zh-CN/API参考/调用方式/公共参数.md#commonResponseParameters)。

## 示例 { .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=DeleteAutoSnapshotPolicy
&RegionId=cn-hangzhou
&AutoSnapshotPolicyId=p-233e6ylv0
&<公共请求参数>
```

**返回示例** 

**XML 格式**

```
<DeleteAutoSnapshotPolicyResponse>
    <RequestId>F3CD6886-D8D0-4FEE-B93E-1B73239673DE</RequestId> 
</DeleteAutoSnapshotPolicyResponse>
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
|ParameterInvalid|The specified automatic snapshot policy does not exist.|404|指定的 `AutoSnapshotPolicyId`不存在。|
|ParameterInvalid|The specified automatic snapshot policy does not exist in the region.|404|指定的 `AutoSnapshotPolicyId`不在指定的地域中。|

