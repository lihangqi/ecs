# ModifyStorageSetAttribute {#doc_api_Ecs_ModifyStorageSetAttribute .reference}

（Beta）调用ModifyStorageSetAttribute修改一个存储集的名称或描述信息。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=ModifyStorageSetAttribute&type=RPC&version=2014-05-26)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|RegionId|String|是|cn-hangzhou|存储集所属地域。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。

 |
|StorageSetId|String|是|ss-StorageSetId|存储集ID。

 |
|Action|String|否|ModifyStorageSetAttribute|系统规定参数。取值：ModifyStorageSetAttribute

 |
|Description|String|否|storageSetTest|存储集描述信息。长度为2~256个英文或中文字符，不能以http://和https://开头。

 |
|StorageSetName|String|否|storageSetTest|存储集名称。长度为2~128个英文或中文字符。必须以大小字母或中文开头，不能以http://和https://开头。可以包含数字、半角冒号（:）、下划线（\_）或者连字符（-）。

 |
|ClientToken|String|否|123e4567-e89b-12d3-a456-426655440000|保证请求幂等性。从您的客户端生成一个参数值，确保不同请求间该参数值唯一。**ClientToken**只支持ASCII字符，且不能超过64个字符。更多详情，请参见[如何保证幂等性](~~25693~~)。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|04F0F334-1335-436C-A1D7-6C044FE73369|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=ModifyStorageSetAttribute
&RegionId=cn-hangzhou
&StorageSetId=ss-StorageSetId
&StorageSetName=storageSetTest
&Description=xxxxxxxx
&<公共请求参数>
```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ModifyStorageSetAttributeResponse>
    <RequestId>04F0F334-1335-436C-A1D7-6C044FE73368</RequestId>
</ModifyStorageSetAttributeResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"04F0F334-1335-436C-A1D7-6C044FE73368"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InvalidClientToken.ValueNotSupported|clienttoken is not valid.|指定的 ClientToken 不合法。|
|403|InvalidParameter|%s|参数格式不正确。|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

