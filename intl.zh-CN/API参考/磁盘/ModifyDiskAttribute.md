# ModifyDiskAttribute {#doc_api_999555 .reference}

修改您的磁盘的属性或者明细。

## 描述 {#description .section}

当您调用该接口时设置了 不随实例释放（DeleteWithInstance=false）属性，一旦磁盘挂载的 ECS 实例被 安全控制且 OperationLocks 中标记了 "LockReason" : "security" 的锁定状态，释放实例时会忽略磁盘的 DeleteWithInstance 属性而被同时释放。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=ModifyDiskAttribute)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|DiskId|String|是|d-diskid1|待修改明细的磁盘 ID。

 |
|Action|String|否|ModifyDiskAttribute|系统规定参数。取值：ModifyDiskAttribute

 |
|DeleteAutoSnapshot|Boolean|否|false|删除磁盘时，是否同时删除其自动快照。默认值：无，无表示不改变当前的值。

 |
|DeleteWithInstance|Boolean|否|false|磁盘是否随实例释放。默认值：无，无表示不改变当前的值。

 在下列两种情况下，将参数 DeleteWithInstance 设置成 false 时会报错。

 -   磁盘的种类（category）为本地盘（ephemeral）时。
-   磁盘的种类（category）为普通云盘（cloud），且不可以卸载（Portable=false）时。

 |
|Description|String|否|FinanceDeptJoshua|磁盘描述。 长度为 2~256 个英文或中文字符，不能以 http:// 和 https:// 开头。

 |
|DiskName|String|否|FinanceJoshua|磁盘名称。长度为 2~128 个英文或中文字符。必须以大小字母或中文开头，不能以 http:// 和 https:// 开头。可以包含数字、半角冒号（:）、下划线（\_）或者连字符（-）。

 |
|EnableAutoSnapshot|Boolean|否|true|如果您已经创建了自动快照策略，是否应用于该磁盘。默认值：无，无表示不改变当前的值。

 |
|OwnerAccount|String|否|ECSforCloud@Alibaba.com|RAM 用户的账号登录名称。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

https://ecs.aliyuncs.com/?Action=ModifyDiskAttribute
&DiskId=d-23jbf2v5m
&DiskName=MyDiskName
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ModifyDiskAttributeResponse>
  <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</ModifyDiskAttributeResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|404|InvalidDescription.Malformed|The specified description is wrongly formed.|指定的资源描述格式不合法。长度为2-256个字符，不能以 http:// 和 https:// 开头。|
|403|QuotaExceed.Snapshot|The snapshot quota exceeds.|快照额度超过限制，若要存储新快照，在不影响业务的情况下，请您删除已有的老快照。|
|400|IncompleteParamter|Some fields can not be null in this request.|请求中缺失参数。|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Ecs)

