# ModifySecurityGroupAttribute {#ModifySecurityGroupAttribute .reference}

修改指定安全组的属性，包括修改安全组名称和描述。

## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：ModifySecurityGroupAttribute|
|RegionId|String|是|地域 ID。您可以调用 [DescribeRegions](intl.zh-CN/API参考/地域/DescribeRegions.md#) 查看最新的阿里云地域列表。|
|SecurityGroupId|String|是|安全组 ID。|
|SecurityGroupName|String|否|安全组名称。-   长度为 \[2, 128\] 个英文或中文字符，必须以大小字母或中文开头，可包含数字、半角冒号（:）、点号（.）、下划线（\_）或短横线（-）。
-   安全组名称会显示在控制台。
-   不能以 http:// 和 https:// 开头。

|
|Description|String|否|安全组描述信息。-   长度为 \[2, 256\] 个英文或中文字符。
-   不能以 http:// 和 https:// 开头。
-   取值不能为空字符串，否则会忽略 `Description` 参数的取值。

|

## 返回参数 {#section_f54_lk5_xdb .section}

全是公共返回参数。参阅 [公共参数](intl.zh-CN/API参考/调用方式/公共参数.md#commonResponseParameters)。

## 示例 { .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=ModifySecurityGroupAttribute
&SecurityGroupId=sg-F876FF7BA
&RegionId=cn-hangzhou
&SecurityGroupName=NewName
&<公共请求参数>
```

**返回示例** 

**XML 格式**

```
<ModifySecurityGroupAttributeResponse>
     <RequestId>CEF72CEB-54B6-4AE8-B225-F876FF7BA984</RequestId>
</ModifySecurityGroupAttributeResponse>
```

 **JSON 格式** 

```
{
    "RequestId":"CEF72CEB-54B6-4AE8-B225-F876FF7BA984"
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问 [API 错误中心](https://error-center.alibabacloud.com/status/product/Ecs)。

|错误代码|错误信息|HTTP 状态码|说明|
|:---|:---|:-------|:-|
|InvalidSecurityGroupDiscription.Malformed|Specified security group description is not valid.|400|指定的 `Description`不合法。|
|InvalidSecurityGroupName.Malformed|Specified security group name is not valid.|400|指定的 `SecurityGroupName`不合法。|
|InvalidSecurityGroupId.NotFound|The specified SecurityGroupId does not exist.|404|指定的 `SecurityGroupId` 不存在。|

