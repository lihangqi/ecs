# ModifyAutoSnapshotPolicyEx {#doc_api_Ecs_ModifyAutoSnapshotPolicyEx .reference}

调用ModifyAutoSnapshotPolicyEx修改一条自动快照策略。修改自动快照策略后，之前已应用该策略的云盘随即执行修改后的自动快照策略。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=ModifyAutoSnapshotPolicyEx)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|autoSnapshotPolicyId|String|是|p-autopolicyid1|目标自动快照策略 ID。您可以调用 [DescribeAutoSnapshotPolicyEx](~~25530~~) 查看您可用的自动快照策略。

 |
|regionId|String|是|cn-hangzhou|自动快照策略所在的地域 ID。您可以调用 [DescribeRegions](~~25609~~) 查看最新的阿里云地域列表。

 |
|Action|String|否|ModifyAutoSnapshotPolicyEx|系统规定参数。取值：ModifyAutoSnapshotPolicyEx

 |
|autoSnapshotPolicyName|String|否|FinanceJoshua|自动快照策略的名称。如果参数为空则代表不修改。

 |
|repeatWeekdays|String|否|\["1", "7"\]|自动快照的重复日期，单位为天，周期为星期。取值范围：1~7，如 1 表示周一。当一星期内需要创建多次自动快照时，可以传入多个时间点：

 -   最多传入 7 个时间点。
-   多个时间点用一个格式类似 "1", "2", … "7" 的 JSON 数组表示，时间点之间用半角逗号（,）隔开。

 |
|retentionDays|Integer|否|30|自动快照的保留时间，单位为天。取值范围：

 -   -1（默认）：永久保存。
-   1~65536：指定保存天数。

 |
|timePoints|String|否|\["0", "1"\]|自动快照的创建时间点，单位为小时。取值范围：0~23，代表 00:00 至 23:00 共 24 个时间点，如 1 表示 01:00。当一天内需要创建多次自动快照时，可以传入多个时间点：

 -   最多传入 24 个时间点。
-   多个时间点用一个格式类似 "0", "1", … "23" 的 JSON 数组表示，时间点之间用半角逗号（,）隔开。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

https://ecs.aliyuncs.com/?Action=ModifyAutoSnapshotPolicyEx
&autoSnapshotPolicyId=p-autopolicyid1
&regionId=cn-hangzhou
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ModifyAutoSnapshotPolicyResponse>
  <RequestId>F3CD6886-D8D0-4FEE-B93E-1B73239673DE</RequestId>
</ModifyAutoSnapshotPolicyResponse>

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
|403|ParameterInvalid|The specified RegionId parameter is invalid.|指定的地域 ID 无效，请您检查该地域是否正确。|
|403|ParameterInvalid|The specified RepeatWeekDays parameter is invalid.|指定的日期无效，请您检查该日期是否正确。|
|403|ParameterInvalid|The specified TimePoints parameter is invalid.|指定的时间点不合法，请您查看该时间点是否填写正确。|
|403|ParameterInvalid|The specified AutoSnapshotPolicyId is invalid.|指定的自动快照规则 ID 不合法。|
|403|ParameterInvalid|The specified RetentionDays parameter is invalid.|指定的保持天数 ID 不合法。|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

