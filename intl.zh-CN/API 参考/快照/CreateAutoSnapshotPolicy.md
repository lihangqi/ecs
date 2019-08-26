# CreateAutoSnapshotPolicy {#CreateAutoSnapshotPolicy .reference}

创建一条自动快照策略。创建的自动快照策略可以应用到任一磁盘（[ApplyAutoSnapshotPolicy](intl.zh-CN/API参考/快照/ApplyAutoSnapshotPolicy.md#)），成功创建的自动快照策略可以后续修改策略内容（[ModifyAutoSnapshotPolicyEx](intl.zh-CN/API参考/快照/ModifyAutoSnapshotPolicyEx.md#)）。

## 描述 {#section_qjr_yvz_xdb .section}

调用该接口时，您需要注意：

-   一个阿里云账户在一个地域最多能创建 100 条自动快照策略。

-   如果磁盘数据较多，单次创建自动快照的时长超过两个时间点间隔，则自动跳过下一时间点。

    **示例**：您设置了 09:00、10:00、11:00 和 12:00 为自动快照时间点。由于磁盘数据较多，09:00 开始创建快照，10:20 完成创建快照，实际耗时 80 分钟。系统会跳过 10:00 时间点，等到 11:00 继续为您创建自动快照。


## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：CreateAutoSnapshotPolicy|
|RegionId|String|是|自动快照策略所属的地域。您可以调用 [DescribeRegions](intl.zh-CN/API参考/地域/DescribeRegions.md#) 查看最新的阿里云地域列表。|
|TimePoints|String|是|自动快照的创建时间点，单位为小时。取值范围：\[0, 23\]，代表 00:00 至 23:00 共 24 个时间点，如 `1` 表示 01:00。当一天内需要创建多次自动快照时，可以传入多个时间点：-   最多传入 24 个时间点。
-   多个时间点用一个格式类似 \["0", "1", … "23"\] 的 JSON 数组表示，时间点之间用半角逗号（`,`）隔开。

|
|RepeatWeekdays|String|是|自动快照的重复日期，单位为天，周期为星期。取值范围：\[1, 7\]，如 `1` 表示周一。当一星期内需要创建多次自动快照时，可以传入多个时间点：-   最多传入 7 个时间点。
-   多个时间点用一个格式类似 \["1", "2", … "7"\] 的 JSON 数组表示，时间点之间用半角逗号（`,`）隔开。

|
|RetentionDays|integer|是|自动快照的保留时间，单位为天。取值范围：-   -1：永久保存。
-   \[1, 65536\]：指定保存天数。

默认值：-1|
|AutoSnapshotPolicyName|String|否|自动快照策略的名称。-   长度为 \[2, 128\] 个英文或中文字符。
-   必须以大小字母或中文开头，可包含数字、半角冒号（:）、下划线（\_）或连字符（-）。
-   不能以 http:// 和 https:// 开头。

默认值：空|
|ClientToken|String|否|用于保证请求的幂等性。由客户端生成该参数值，要保证在不同请求间唯一。只支持 ASCII 字符，且不能超过 64 个字符。更多详情，请参阅 [如何保证幂等性](intl.zh-CN/API参考/附录/如何保证幂等性.md#)。|

## 返回参数 {#ResponseParameter .section}

|名称|类型|描述|
|:-|:-|:-|
|AutoSnapshotPolicyId|String|自动快照策略 ID|

## 示例 { .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=CreateAutoSnapshotPolicy
&RegionId=cn-hangzhou
&TimePoints=[“0”, “11 ”, “21 ”]
&RepeatWeekdays=[“1” ，“2” ，“4” ，“7”]
&RetentionDays=30
&<公共请求参数>
```

**返回示例** 

**XML 格式**

```
<CreateAutoSnapshotPolicyResponse>
    <RequestId>F3CD6886-D8D0-4FEE-B93E-1B73239673DE</RequestId>
    <AutoSnapshotPolicyId>p-233e6ylv0</AutoSnapshotPolicyId>
</CreateAutoSnapshotPolicyResponse>
```

 **JSON 格式** 

```
{
    "RequestId":"F3CD6886-D8D0-4FEE-B93E-1B73239673DE"
    "AutoSnapshotPolicyId":"p-233e6ylv0"
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问 [API 错误中心](https://error-center.alibabacloud.com/status/product/Ecs)。

|错误代码|错误信息|HTTP 状态码|说明|
|:---|:---|:-------|:-|
|AutoSnapshotPolicy.QuotaExceed|The maximum number of automatic snapshot policy has been reached.|403|一个阿里云账户在一个地域最多能创建 100 条自动快照策略。|
|ParameterInvalid|The specified RegionId parameter is invalid.|404|指定的参数 `RegionId`无效。|
|ParameterInvalid|The specified RepeatWeekDays parameter is invalid.|404|指定的参数 `RepeatWeekDays` 不合法。|
|ParameterInvalid|The specified RetentionDays parameter is invalid.|404|指定的参数 `RetentionDays` 不合法。|
|ParameterInvalid|The specified TimePoints parameter is invalid.|404|指定的参数 `TimePoints` 不合法。|

