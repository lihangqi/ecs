# CreateSecurityGroup {#CreateSecurityGroup .reference}

新建一个安全组。新建的安全组，默认只允许安全组内实例互相访问，安全组外的一切通信请求会被拒绝。若您想允许其他安全组实例的通信请求，或者来自互联网的访问请求，需要授权安全组权限（[AuthorizeSecurityGroup](intl.zh-CN/API 参考/安全组/AuthorizeSecurityGroup.md#)）。

## 描述 {#section_w5n_p21_ydb .section}

调用该接口时，您需要注意：

-   在一个阿里云地域下，您最多可创建100个安全组。

-   创建专有网络VPC类型的安全组时，您必须指定参数`VpcId`。


## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：CreateSecurityGroup|
|RegionId|String|是|安全组所属地域ID。您可以调用[DescribeRegions](../intl.zh-CN/API 参考/地域/DescribeRegions.md#)查看最新的阿里云地域列表。|
|SecurityGroupName|String|否|安全组名称。长度为\[2, 128\]个英文或中文字符。必须以大小字母或中文开头，不能以http://和https://开头。可以包含数字、半角冒号（:）、下划线（\_）或者连字符（-）。默认值：空。

|
|Description|String|否|安全组描述信息。长度为\[2, 256\]个英文或中文字符，不能以http://和https://开头。默认值：空。

|
|VpcId|String|否|安全组所属VPC ID。|
|Tag.n.Key|String|否|安全组的标签键。n的取值范围：\[1, 20\]。一旦传入该值，则不允许为空字符串。最多支持64个字符，不能以aliyun、acs:、http://或者https://开头。|
|Tag.n.Value|String|否|安全组的标签值。n的取值范围：\[1, 20\]。一旦传入该值，可以为空字符串。最多支持128个字符，不能以aliyun、acs:、http://或者https://开头。|
|ClientToken|String|否| 保证请求幂等性。从您的客户端生成一个参数值，确保不同请求间该参数值唯一。只支持ASCII字符，且不能超过64个字符。更多详情，请参阅[如何保证幂等性](../intl.zh-CN/API 参考/附录/如何保证幂等性.md#)。

 |

## 返回参数 {#ResponseParameter .section}

|名称|类型|描述|
|:-|:-|:-|
|SecurityGroupId|String|安全组ID|

## 示例 { .section}

**请求示例**

```
https://ecs.aliyuncs.com/?Action=CreateSecurityGroup
&RegionId=cn-hangzhou
&Description=for_demo
&<公共请求参数>
```

**返回示例**

**XML格式** 

```
<CreateSecurityGroupResponse>
    <RequestId>CEF72CEB-54B6-4AE8-B225-F876FF7BA984</RequestId>
    <SecurityGroupId>sg-F876FF7BA</SecurityGroupId>
</CreateSecurityGroupResponse>
```

**JSON格式** 

```
{
    "RequestId":"CEF72CEB-54B6-4AE8-B225-F876FF7BA984",
    "SecurityGroupId":"sg-F876FF7BA"
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问[API错误中心](https://error-center.alibabacloud.com/status/product/Ecs)。

|错误代码|错误信息|HTTP状态码|说明|
|:---|:---|:------|:-|
|IncorrectVpcStatus|Current VPC status does not support this operation.|400|指定的VPC正在被创建、编辑或者删除，请稍后再试。|
|InvalidDescription.Malformed|The specified parameter “Description” is not valid.|400|指定的`Description`不合法。|
|InvalidSecurityGroupDiscription.Malformed|Specified security group description is not valid.|400|指定的`Description`不合法。|
|InvalidSecurityGroupName.Malformed|Specified security group name is not valid.|400|指定的`SecurityGroupName`不合法。|
|InvalidVpcId.NotFound|vpc id must not empty when only support vpc vm.|403|参数`VpcId`不能为空。|
|QuotaExceed.SecurityGroup|The maximum number of security groups is reached.|403|在指定地域下，您最多可以创建100个安全组。|
|InvalidRegionId.NotFound|The specified RegionId does not exist.|404|指定的`RegionId`不存在。|
|InvalidVpcId.NotFound|Specified VPC does not exist.|404|指定的VPC不存在。|

