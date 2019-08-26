# ModifyImageAttribute {#ModifyImageAttribute .reference}

修改一份自定义镜像的名称和描述。

## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：ModifyImageAttribute|
|RegionId|String|是|自定义镜像所在的地域 ID。您可以调用 [DescribeRegions](intl.zh-CN/API参考/地域/DescribeRegions.md#) 查看最新的阿里云地域列表。|
|ImageId|String|是|自定义镜像的 ID。|
|ImageName|String|否|自定义镜像名称。-   能包含 \[2, 128\] 个英文或中文字符。
-   必须以大小字母或中文开头，可包含数字、半角冒号（:）、下划线（\_）或者连字符（-）。
-   不能以 http:// 和 https:// 开头。

|
|Description|String|否|自定义镜像的描述信息。-   能包含 \[0, 256\] 个字符。
-   不能以 http:// 和 https:// 开头。
-   不填则为空，默认为空。

|

## 返回参数 {#section_f54_lk5_xdb .section}

全是公共返回参数。参阅 [公共参数](intl.zh-CN/API参考/调用方式/公共参数.md#commonResponseParameters)

## 示例 { .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=ModifyImageAttribute
&ImageId=m-281234567
&RegionId=cn-qingdao
&ImageName=testImage123
&<公共请求参数>
```

**返回示例** 

**XML 格式**

```
<ModifyImageAttributeResponse>
    <RequestId>C8B26B44-0189-443E-9816-D951F59623A9</RequestId>
</ModifyImageAttributeResponse>
```

 **JSON 格式** 

```
{
    "RequestId": "C8B26B44-0189-443E-9816-D951F59623A9"
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问 [API 错误中心](https://error-center.alibabacloud.com/status/product/Ecs)。

|错误代码|错误信息|HTTP 状态码|说明|
|:---|:---|:-------|:-|
|InvalidDescription.Malformed|The specified description is wrongly formed.|400|指定的 `Description` 不合法。|
|InvalidImageName.Duplicated|The specified Image name has already bean used.|400|指定的 `ImageName` 已经被使用。|
|InvalidImageName.Malformed|The specified Image name is wrongly formed.|400|无效的 `ImageName` 取值，字符不支持或者超出长度。|
|MissingParameter|The input parameter “RegionId” that is mandatory for processing this request is not supplied.|400|缺少必填参数 `RegionId`。|
|InvalidImageId.NotFound|The specified ImageId does not exist.|403|指定的镜像不存在。|
|InvalidRegionId.NotFound|The specified region does not exist.|404|指定的 `RegionId` 不存在。|

