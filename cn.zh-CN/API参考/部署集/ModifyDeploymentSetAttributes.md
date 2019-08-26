# ModifyDeploymentSetAttributes {#ModifyDeploymentSetAttributes .reference}

修改一个部署集的名称和描述信息。

## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数，取值：ModifyDeploymentSetAttributes|
|RegionId|String|是|部署集所属地域ID。您可以调用[DescribeRegions](../cn.zh-CN/API参考/地域/DescribeRegions.md#)查看最新的阿里云地域列表。|
|DeploymentSetId|String|是|部署集ID。|
|DeploymentSetName|String|否|新的部署集名称。长度为 \[2, 128\] 个英文或中文字符。必须以大小字母或中文开头，不能以 http:// 和 https:// 开头。可以包含数字、半角冒号（:）、下划线（\_）或者连字符（-）。|
|Description|String|否|新的部署集描述信息。长度为 \[2, 256\] 个英文或中文字符，不能以 http:// 和 https:// 开头。|

## 返回参数 {#ResponseParameter .section}

全是公共返回参数。参阅[公共返回参数](../cn.zh-CN/API参考/HTTP调用方式/公共参数.md#commonResponseParameters)。

## 示例 {#section_g4q_shf_2fb .section}

**请求示例**

```
https://ecs.aliyuncs.com/?Action=ModifyDeploymentSetAttributes
&RegionId=cn-hangzhou
&Strategy=Availability
&DeploymentSetId=ds-bp1frxuzdg87zh4pzqkc
&DeploymentSetName=AvailMySet
&<公共请求参数>
```

**返回示例**

**XML格式**

```
<ModifyDeploymentSetAttributesResponse>
	<RequestId>04F0F334-1335-436C-A1D7-6C044FE73368</RequestId>
</ModifyDeploymentSetAttributesResponse>
```

**JSON格式**

```
{
	"RequestId": "04F0F334-1335-436C-A1D7-6C044FE73368"
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问[API错误中心](https://error-center.aliyun.com/status/product/Ecs)。

|错误代码|错误信息|HTTP状态码|说明|
|:---|:---|:------|:-|
|InvalidDescription.Malformed|The specified parameter “Description” is not valid.|400|指定的Description无效。|
|InvalidParameter.Strategy|The specified parameter Strategy is not valid|400|指定部署策略无效。|
|MissingParameter|The input parameter “RegionId” that is mandatory for processing this request is not supplied.|400|您需要指定RegionId参数。或者您暂时无法使用指定地域中的资源。|
|InvalidRegionId.NotFound|The RegionId provided does not exist in our records.|404|指定的RegionId不存在。|

