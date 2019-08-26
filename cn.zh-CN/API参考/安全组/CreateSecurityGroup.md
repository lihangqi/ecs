# CreateSecurityGroup {#doc_api_Ecs_CreateSecurityGroup .reference}

调用CreateSecurityGroup新建一个安全组。新建的安全组，默认只允许安全组内实例互相访问，安全组外的一切通信请求会被拒绝。若您想允许其他安全组实例的通信请求，或者来自互联网的访问请求，需要授权安全组权限（AuthorizeSecurityGroup）。

## 接口说明 {#description .section}

调用该接口时，您需要注意：

-   在一个阿里云地域下，您最多可创建100个安全组。
-   创建专有网络VPC类型的安全组时，您必须指定参数VpcId。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=CreateSecurityGroup)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|RegionId|String|是|cn-hangzhou|安全组所属地域ID。您可以调用 [DescribeRegions](~~25609~~) 查看最新的阿里云地域列表。

 |
|Action|String|否|CreateSecurityGroup|系统规定参数。取值：CreateSecurityGroup

 |
|ClientToken|String|否|123e4567-e89b-12d3-a456-426655440000|保证请求幂等性。从您的客户端生成一个参数值，确保不同请求间该参数值唯一。**ClientToken**只支持ASCII字符，且不能超过64个字符。更多详情，请参见[如何保证幂等性](~~25693~~)。

 |
|Description|String|否|FinanceDept|安全组描述信息。长度为2~256个英文或中文字符，不能以 http:// 和 https:// 开头。默认值：空。

 |
|ResourceGroupId|String|否|rg-resourcegrouid|安全组所在的企业资源组ID。

 |
|SecurityGroupName|String|否|FinanceJoshua|安全组名称。长度为2~128个英文或中文字符。必须以大小字母或中文开头，不能以 http:// 和 https:// 开头。可以包含数字、半角冒号（:）、下划线（\_）或者连字符（-）。默认值：空。

 |
|SecurityGroupType|String|否|enterprise|安全组类型，分为普通安全组与企业安全组。取值范围：

 -   normal：普通安全组。
-   enterprise：企业安全组。更多详情，请参见 [企业安全组概述](~~120621~~)。

 |
|Tag.N.Key|String|否|FinanceDept|安全组的标签键。N 的取值范围：1~20。一旦传入该值，则不允许为空字符串。最多支持 64 个字符，不能以 aliyun 和 acs: 开头，不能包含 http:// 或者 https:// 。

 |
|Tag.N.Value|String|否|FinanceDeptJoshua|安全组的标签值。N 的取值范围：1~20。一旦传入该值，可以为空字符串。最多支持 128 个字符，不能以 aliyun 和 acs: 开头，不能包含 http:// 或者 https:// 。

 |
|Tag.N.key|String|否|FinanceDept|安全组的标签键。

 **说明：** 为提高兼容性，建议您尽量使用Tag.N.Key参数。

 |
|Tag.N.value|String|否|FinanceDeptJoshua|安全组的标签值。

 **说明：** 为提高兼容性，建议您尽量使用Tag.N.Value参数。

 |
|VpcId|String|否|vpc-vpcid1|安全组所属VPC ID。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。

 |
|SecurityGroupId|String|sg-F876FF7\*\*|安全组 ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=CreateSecurityGroup
&RegionId=cn-hangzhou
&Description=for_demo
&<公共请求参数>
```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<CreateSecurityGroupResponse>
  <RequestId>CEF72CEB-54B6-4AE8-B225-F876FF7BA984</RequestId>
  <SecurityGroupId>sg-securitygroupid</SecurityGroupId>
</CreateSecurityGroupResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"SecurityGroupId":"sg-securitygroupid",
	"RequestId":"CEF72CEB-54B6-4AE8-B225-F876FF7BA984"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InvalidDescription.Malformed|The specified parameter "Description" is not valid.|指定的资源描述格式不合法。长度为2-256个字符，不能以 http:// 和 https:// 开头。|
|403|QuotaExceed.SecurityGroup|The maximum number of security groups is reached.|安全组个数超过额度限制，请您提交工单申请白名单。|
|404|InvalidVpcId.NotFound|Specified VPC does not exist.|指定的专有网络 VPC ID 不存在，请您检查 regionId 是否存在。|
|400|InvalidSecurityGroupName.Malformed|Specified security group name is not valid.|指定的安全组名称格式不合法，请您按照规则进行配置：默认值是空，填写\[2, 128\]的英文或中文字符，必须以大小字母或中文开头，可包含数字，”.”，”\_”或”-”，安全组名称会展示在控制台。不能以 http:// 和 https:// 开头。|
|400|InvalidSecurityGroupDiscription.Malformed|Specified security group description is not valid.|指定的安全组描述不合法。|
|500|InternalError|The request processing has failed due to some unknown error.|内部错误，请重试。如果多次尝试失败，请提交工单|
|403|InvalidVpcId.NotFound|vpc id must not empty when only support vpc vm.|指定的 VPC ID 不能为空。|
|400|IncorrectVpcStatus|Current VPC status does not support this operation.|当前专有网络VPC的状态无法支持这个操作。|
|400|InvalidTagKey.Malformed|Specified tag key is not valid.|指定的标签键无效。|
|400|InvalidTagValue.Malformed|Specified tag value is not valid.|指定的标签值无效。|
|404|InvalidResourceGroup.NotFound|The ResourceGroup provided does not exist in our records.|资源组并不在记录中。|
|400|Duplicate.TagKey|The Tag.N.Key contain duplicate key.|标签键中存在重复的键。|
|400|InvalidTagKey.Malformed|The specified Tag.n.Key is not valid.|指定的标签键不合法。|
|400|InvalidTagValue.Malformed|The specified Tag.n.Value is not valid.|指定的标签值不合法。|
|403|IdempotentProcessing|The previous idempotent request\(s\) is still processing.|同样clienttoken的请求正在处理中。|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

