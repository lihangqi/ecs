# ModifyImageAttribute {#doc_api_Ecs_ModifyImageAttribute .reference}

调用ModifyImageAttribute修改一份自定义镜像的名称或描述信息。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=ModifyImageAttribute&type=RPC&version=2014-05-26)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|ImageId|String|是|m-imageid1|自定义镜像的ID。

 |
|RegionId|String|是|cn-hangzhou|自定义镜像所在的地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。

 |
|Action|String|否|ModifyImageAttribute|系统规定参数。对于您自行拼凑HTTP/HTTPS URL发起的API请求，`Action`为必选参数。取值：ModifyImageAttribute

 |
|Description|String|否|FinanceDept|自定义镜像的描述信息。能包含0~256个字符。不能以http://和https://开头。

 默认值：空，表示保持原有描述信息不变。

 |
|ImageName|String|否|FinanceJoshua|自定义镜像的名称。能包含2~128个字符。必须以大小字母或中文开头，可包含数字、半角冒号（:）、下划线（\_）或者连字符（-）。不能以http://和https://开头。

 默认值：空，表示保持原有名称不变。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=ModifyImageAttribute
&ImageId=m-imageid1
&RegionId=cn-hangzhou
&ImageName=FinanceJoshua
&Description=FinanceDept
&<公共请求参数>
```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ModifyImageAttributeResponse>
      <RequestId>C8B26B44-0189-443E-9816-D951F59623A9</RequestId>
</ModifyImageAttributeResponse>
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
|400|InvalidImageName.Malformed|The specified Image name is wrongly formed.|镜像名称不合法。长度为2-128个字符，以英文字母或中文开头，可包含数字，"."，"\_"或"-"。 不能以 http:// 和 https:// 开头。|
|400|MissingParameter|The input parameter "RegionId" that is mandatory for processing this request is not supplied.|区域ID不得为空。|
|400|InvalidImageName.Duplicated|The specified Image name has already bean used.|镜像名称已经重复。|
|400|InvalidDescription.Malformed|The specified description is wrongly formed.|指定的资源描述格式不合法。长度为2-256个字符，不能以 http:// 和 https:// 开头。|
|404|InvalidImageId.NotFound|The specified ImageId does not exist.|指定的镜像在该用户账号下不存在，请您检查镜像id是否正确。|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

