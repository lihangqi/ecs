# CancelAutoSnapshotPolicy {#doc_api_999639 .reference}

取消一块或者多块磁盘的自动快照策略。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=CancelAutoSnapshotPolicy)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|diskIds|String|是|\["d-233e6ylv0", "d-23vbpbi03", "d-23vasz3ds"\]|目标磁盘 ID。当您需要取消多块磁盘的自动快照策略时，多块磁盘 ID 用一个格式类似 "d-xxxxxxxxx", "d-yyyyyyyyy", … "d-zzzzzzzzz" 的 JSON 数组表示，磁盘 ID 之间用半角逗号（,）隔开。

 |
|regionId|String|是|cn-hangzhou|自动快照策略和磁盘所在的地域 ID。您可以调用 [DescribeRegions](~~25609~~) 查看最新的阿里云地域列表。

 |
|Action|String|否|CancelAutoSnapshotPolicy|系统规定参数。取值：CancelAutoSnapshotPolicy

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。无论调用接口成功与否，我们都会返回请求 ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

https://ecs.aliyuncs.com/?Action=CancelAutoSnapshotPolicy
&diskIds=["d-233e6ylv0", "d-23vbpbi03", "d-23vasz3ds"]
&regionId=cn-hangzhou
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<CancelAutoSnapshotPolicyResponse>
  <RequestId>F3CD6886-D8D0-4FEE-B93E-1B73239673DE</RequestId>
</CancelAutoSnapshotPolicyResponse>

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
|403|ParameterInvalid|The specified RegionId parameter is invalid.|指定的地域 ID 无效，请您检查该地域是否正确。|
|403|ParameterInvalid|The specified DiskIds are invalid.|指定的磁盘 ID 不合法，请您检查磁盘 ID 是否正确，且存在。|
|404|InvalidDiskId.NotFound|The specified DiskIds are not found.|指定的磁盘ID不存在。|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Ecs)

