# ModifySecurityGroupPolicy {#doc_api_1031578 .reference}

修改安全组内网连通策略。

## 接口说明 {#description .section}

调用该接口时，您需要注意：

-   参数 InnerAccessPolicy 的值为 Accept 时，安全组内的实例之间的网络是互通的。此时，遵循 Accept 优先原则，即，安全组内的实例之间的网络一直保持互通，不受用户自定义安全组规则影响。
-   参数 InnerAccessPolicy 的值为 Drop 时，安全组内的实例之间的网络是隔离的。此时，遵循用户自定义安全组规则优先原则，即，安全组内的实例之间的网络虽然是隔离的，但您可以自定义安全组规则改变内网状态，例如，您可以通过 [AuthorizeSecurityGroup](~~25554~~) 使安全组内的两台 ECS 实例网络互通。
-   您可以通过 [DescribeSecurityGroupAttribute](~~25555~~) 查询当前安全组内网连通策略。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=ModifySecurityGroupPolicy)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|InnerAccessPolicy|String|是|Accept|当前安全组内网连通策略。取值范围：

 -   Accept：安全组内的实例之间的网络是互通的。
-   Drop：安全组内的实例之间的网络是隔离的。

 以上取值，不区分大小写。

 |
|RegionId|String|是|cn-hangzhou|安全组所属地域 ID。您可以调用 [DescribeRegions](~~25609~~) 查看最新的阿里云地域列表。

 |
|SecurityGroupId|String|是|sg-securitygroupid1|安全组的 ID。

 |
|Action|String|否|ModifySecurityGroupPolicy|系统规定参数。取值：ModifySecurityGroupPolicy

 |
|ClientToken|String|否|123e4567-e89b-12d3-a456-426655440000|保证请求幂等性。从您的客户端生成一个参数值，确保不同请求间该参数值唯一。**ClientToken** 只支持 ASCII 字符，且不能超过 64 个字符。更多详情，请参阅 [如何保证幂等性](~~25693~~)。

 |
|OwnerAccount|String|否|ECSforCloud@Alibaba.com|RAM用户的账号登录名称。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

https://ecs.aliyuncs.com/?Action=ModifySecurityGroupPolicy
&RegionId=cn-hangzhou
&SecurityGroupId=sg-1133aa
&InnerAccessPolicy=Drop
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ModifySecurityGroupPolicyResponse>
  <RequestId>CEF72CEB-54B6-4AE8-B225-F876xxxxxxxx</RequestId>
</ModifySecurityGroupPolicyResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"CEF72CEB-54B6-4AE8-B225-F876FF7BA984"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InvalidSecurityGroupId.Malformed|The SecurityGroupId is invalid. Only letters, numbers and underscores are supported. Maximum length is 100 characters.|无效的安全组ID。|
|400|InvalidPolicy.Malformed|The Policy is invalid. Only 'Accept' and 'Drop' are supported. Ignore case.|指定的Policy参数无效。|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Ecs)

