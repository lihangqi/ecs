# ModifySnapshotAttribute {#doc_api_Ecs_ModifySnapshotAttribute .reference}

调用ModifySnapshotAttribute修改一份快照的名称或描述。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=ModifySnapshotAttribute&type=RPC&version=2014-05-26)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|SnapshotId|String|是|s-923FE2B\*\*|快照ID。

 |
|Action|String|否|ModifySnapshotAttribute|接口名称。对于您自行拼凑HTTP/HTTPS URL发起的API请求，`Action`为必选参数。取值：ModifySnapshotAttribute

 |
|Description|String|否|NewSnapshotDescription-EcsGuideTest|快照的描述。长度为2~256个英文或中文字符，不能以http://和https://开头。

 |
|SnapshotName|String|否|NewSnapshotName-EcsGuideTest|快照的显示名称。长度为2~128个英文或中文字符。必须以大小字母或中文开头，不能以http://和https://开头。可以包含数字、半角冒号（:）、下划线（\_）或者连字符（-）。

 为防止和自动快照的名称冲突，不能以auto开头。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=ModifySnapshotAttribute
&SnapshotName=NewSnapshotName-EcsGuideTest
&Description=NewSnapshotDescription-EcsGuideTest
&<公共请求参数>
```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ModifySnapshotAttributeResponse>
            <RequestId>C8B26B44-0189-443E-9816-D951F59623A9</RequestId>
</ModifySnapshotAttributeResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"C8B26B44-0189-443E-9816-D951F59623A9"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|404|InvalidDescription.Malformed|The specified description is wrongly formed.|指定的资源描述格式不合法。长度为2-256个字符，不能以 http:// 和 https:// 开头。|
|400|InvalidSnapshotName.Malformed|The specified SnapshotName is wrongly formed.|快照名称格式不合法。长度为2-128个字符，以英文字母或中文开头，可包含数字，"."，"\_"或"-"。 不能以 http:// 和 https:// 开头。|
|400|NoAttributeToModify|No attribute to be modified in this request.|没有任何属性被修改。|
|404|InvalidSnapshotId.NotFound|The specified SnapshotId does not exist.|指定的快照不存在，请您检查快照是否正确。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ecs)查看更多错误码。

