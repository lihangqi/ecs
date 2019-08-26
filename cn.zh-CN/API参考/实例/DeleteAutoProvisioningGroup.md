# DeleteAutoProvisioningGroup {#doc_api_Ecs_DeleteAutoProvisioningGroup .reference}

调用DeleteAutoProvisioningGroup接口删除一个弹性供应组。

删除弹性供应组时，您可以通过 **TerminateInstances** 指定供应组内实例的行为。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=DeleteAutoProvisioningGroup)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
| AutoProvisioningGroupId |String|是|apg-uf6jel2bbl62wh13\*\*\*\*| 弹性供应组的ID。

 |
| RegionId |String|是|cn-hangzhou| 弹性供应组所在地域的ID。

 |
| TerminateInstances |Boolean|是|true| 删除弹性供应组时是否释放组内实例，可选值：

 -    **true** ：释放组内实例。
-    **false** ：组内实例继续运行。

 |
| Action |String|否|DeleteAutoProvisioningGroup| 系统规定参数，取值： **DeleteAutoProvisioningGroup** 。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|B48A12CD-1295-4A38-A8F0-0E92C937\*\*\*\*| 请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://ecs.aliyuncs.com/?Action=DeleteAutoProvisioningGroup
&AutoProvisioningGroupId=fleet-uf6jel2bbl62wh13****
&RegionId=cn-hangzhou
&TerminateInstances=true
&<公共请求参数>

```

正常返回示例

 `XML` 格式

``` {#xml_return_success_demo}
<DeleteAutoProvisioningGroupResponse>
  <RequestId>928E2273-5715-46B9-A730-238DC996****</RequestId>
</DeleteAutoProvisioningGroupResponse>

```

 `JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"B48A12CD-1295-4A38-A8F0-0E92C937****"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|403|Forbidden.RAM|User not authorized to operate on the specified resource, or this API doesn't support RAM.|子账号鉴权不通过。|

 [查看本产品错误码](https://error-center.aliyun.com/status/product/Ecs) 

