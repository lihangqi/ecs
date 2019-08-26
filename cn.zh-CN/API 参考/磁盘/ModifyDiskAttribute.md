# ModifyDiskAttribute {#ModifyDiskAttribute .reference}

修改您的磁盘的属性或者明细。

## 描述 {#section_ntk_xp5_xdb .section}

当您调用该接口时设置了 **不随实例释放**（`DeleteWithInstance=false`）属性，一旦磁盘挂载的 ECS 实例被 [安全控制](intl.zh-CN/API参考/附录/安全锁定时的 API 行为.md#)且 `OperationLocks` 中标记了 `"LockReason" : "security"` 的锁定状态，释放实例时会忽略磁盘的 `DeleteWithInstance` 属性而被同时释放。

## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：ModifyDiskAttribute|
|DiskId|String|是|待修改明细的磁盘 ID。|
|DiskName|String|否|磁盘名称。-   长度为 \[2, 128\] 位英文或中文字符，必须以大小字母或中文开头，可以包含数字、点号（.）、半角冒号（:）、下划线（\_）或者连字符（-）。
-   不能以 http:// 和 https:// 开头。
-   不填则使用原值，默认值为空。

|
|Description|String|否|磁盘描述。-   长度为 \[2, 256\] 位英文或中文字符，必须以大小字母或中文开头，可以包含数字、点号（.）、半角冒号（:）、下划线（\_）或者连字符（-）。
-   不能以 http:// 和 https:// 开头。
-   不填则使用原值，默认值为空。

|
|DeleteWithInstance|String|否|磁盘是否随实例释放。取值范围：-   true：释放实例时，这块磁盘随实例一起释放。
-   false：释放实例时，保留磁盘，不随实例一起释放。

默认值：无，无表示不改变当前的值在下列两种情况下，将参数 `DeleteWithInstance` 设置成 `false` 时会报错。-   磁盘的种类（`category`）为本地盘（`ephemeral`）时。
-   磁盘的种类（`category`）为普通云盘（`cloud`），且不可以卸载（`Portable=false`）时。

|
|DeleteAutoSnapshot|String|否|删除磁盘时，是否同时删除其自动快照。取值范围：-   true：删除自动快照。
-   false：保留自动快照。

默认值：无，无表示不改变当前的值|
|EnableAutoSnapshot|String|否|如果您已经创建了自动快照策略，是否应用于该磁盘。取值范围：-   true：磁盘执行自动快照策略。
-   false：磁盘不执行自动快照策略。

默认值：无，无表示不改变当前的值|

## 返回参数 {#section_b5k_xp5_xdb .section}

全是公共返回参数。参阅 [公共参数](intl.zh-CN/API参考/调用方式/公共参数.md#commonResponseParameters)

## 示例 { .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=ModifyDiskAttribute
&DiskId=d-23jbf2v5m
&DiskName=MyDiskName
&<公共请求参数>
```

**返回示例** 

**XML 格式**

```
<ModifyDiskAttributeResponse>
    <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</ModifyDiskAttributeResponse>
```

 **JSON 格式** 

```
{
    "RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E"
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问 [API 错误中心](https://error-center.alibabacloud.com/status/product/Ecs)。

|错误代码|错误信息|HTTP 状态码|说明|
|:---|:---|:-------|:-|
|InvalidDiskName.Malformed|The specified disk name is wrongly formed.|400|指定的参数 DiskName 格式有误。|
|NoAttributeToModify|No attribute to be modified in this request.|400|您此次请求没有修改任何属性。|
|DiskNotPortable|The specified disk is not a portable disk.|403|设置 `DeleteWithInstance=false`属性时，磁盘的 `Portable` 属性不能为 `false`。|
|IncorrectDiskStatus|The operation is not supported in this status.|403|磁盘状态不正确。磁盘状态参阅 [普通云盘状态表](intl.zh-CN/API参考/附录/普通云盘状态表.md#)。|
|InvalidDescription.Malformed|The specified description is wrongly formed.|404|参数 Description 的格式有误。|
|InvalidDiskId.NotFound|The specified disk does not exist.|404|指定的磁盘不存在。|

