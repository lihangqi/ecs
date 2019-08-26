# ModifyAutoSnapshotPolicyEx {#ModifyAutoSnapshotPolicyEx .reference}

修改一条自动快照策略。修改自动快照策略后，之前已应用该策略的磁盘随即执行修改后的自动快照策略。

## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：ModifyAutoSnapshotPolicyEx|
|RegionId|String|是|自动快照策略所在的地域 ID。您可以调用 [DescribeRegions](cn.zh-CN/API 参考/地域/DescribeRegions.md#) 查看最新的阿里云地域列表。|
|AutoSnapshotPolicyId|String|是|目标自动快照策略 ID。您可以调用 [DescribeAutoSnapshotPolicyEx](cn.zh-CN/API 参考/快照/DescribeAutoSnapshotPolicyEx.md#) 查看您可用的自动快照策略。|
|AutoSnapshotPolicyName|String|否|自动快照策略的名称。如果参数为空则代表不修改。|
|TimePoints|String|否|自动快照的创建时间点，单位为小时。取值范围：\[0, 23\]，代表 00:00 至 23:00 共 24 个时间点，如 `1` 表示 01:00。当一天内需要创建多次自动快照时，可以传入多个时间点：-   最多传入 24 个时间点。
-   多个时间点用一个格式类似 \["0", "1", … "23"\] 的 JSON 数组表示，时间点之间用半角逗号（`,`）隔开。

|
|RepeatWeekdays|String|否|自动快照的重复日期，单位为天，周期为星期。取值范围：\[1, 7\]，如 `1` 表示周一。当一星期内需要创建多次自动快照时，可以传入多个时间点：-   最多传入 7 个时间点。
-   多个时间点用一个格式类似 \["1", "2", … "7"\] 的 JSON 数组表示，时间点之间用半角逗号（`,`）隔开。

|
|RetentionDays|Integer|否|自动快照的保留时间，单位为天。取值范围：-   -1：永久保存。
-   \[1, 65536\]：指定保存天数。

默认值：-1|
|ClientToken|String|否|用于保证请求的幂等性。由客户端生成该参数值，要保证在不同请求间唯一。只支持 ASCII 字符，且不能超过 64 个字符。更多详情，请参阅 [如何保证幂等性](cn.zh-CN/API 参考/附录/如何保证幂等性.md#)。|

## 返回参数 {#section_ajy_hd1_ydb .section}

全是公共返回参数。参阅 [公共参数](cn.zh-CN/API 参考/快速入门/公共参数.md#commonResponseParameters)。

## 示例 { .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=ModifyAutoSnapshotPolicyEx
&RegionId=cn-hangzhou
&AutoSnapshotPolicyId=p-233e6ylv0
&SettingTimePoints=[“0”, “11”, “21”]
&SettingRepeatWeekdays=[“1”, “2”, “4”, “7”]
&RetentionDays=30
&<公共请求参数>
```

**返回示例** 

**XML 格式**

```
<ModifyAutoSnapshotPolicyResponse>
    <RequestId>F3CD6886-D8D0-4FEE-B93E-1B73239673DE</RequestId>
</ModifyAutoSnapshotPolicyResponse>
```

 **JSON 格式** 

```
{
    "RequestId":"F3CD6886-D8D0-4FEE-B93E-1B73239673DE"
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问 [API 错误中心](https://error-center.aliyun.com/status/product/Ecs)。

|错误代码|错误信息|HTTP 状态码|说明|
|:---|:---|:-------|:-|
|ParameterInvalid|The specified automatic snapshot policy does not exist.|404|指定的 `AutoSnapshotPolicyId`不存在。|
|ParameterInvalid|The specified automatic snapshot policy does not exist in the region.|404|指定的 `AutoSnapshotPolicyId`不在指定的地域中。|
|ParameterInvalid|The specified AutoSnapshotPolicyId is invalid.|404|指定的参数 `AutoSnapshotPolicyId`不合法。|
|ParameterInvalid|The specified RegionId parameter is invalid.|404|指定的参数 `RegionId` 不合法。|

