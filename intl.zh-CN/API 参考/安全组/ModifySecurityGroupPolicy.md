# ModifySecurityGroupPolicy {#reference_fps_ngn_ydb .reference}

修改安全组内网连通策略。

## 描述 {#section_m51_pgn_ydb .section}

调用该接口时，您需要注意：

-   参数 `InnerAccessPolicy` 的值为 `Accept` 时，安全组内的实例之间的网络是互通的。此时，遵循 `Accept` 优先原则，即，安全组内的实例之间的网络一直保持互通，不受用户自定义安全组规则影响。

-   参数 `InnerAccessPolicy` 的值为 `Drop` 时，安全组内的实例之间的网络是隔离的。此时，遵循用户自定义安全组规则优先原则，即，安全组内的实例之间的网络虽然是隔离的，但您可以自定义安全组规则改变内网状态，例如，您可以通过 [AuthorizeSecurityGroup](cn.zh-CN/API 参考/安全组/AuthorizeSecurityGroup.md#) 使安全组内的两台 ECS 实例网络互通。

-   您可以通过 [DescribeSecurityGroupAttribute](cn.zh-CN/API 参考/安全组/DescribeSecurityGroupAttribute.md#) 查询当前安全组内网连通策略。


## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：ModifySecurityGroupPolicy|
|SecurityGroupId|String|是|安全组的 ID。|
|RegionId|String|是|安全组所属地域 ID。您可以调用 [DescribeRegions](cn.zh-CN/API 参考/地域/DescribeRegions.md#) 查看最新的阿里云地域列表。|
|InnerAccessPolicy|String|是|当前安全组内网连通策略。取值范围：-   Accept：安全组内的实例之间的网络是互通的。
-   Drop：安全组内的实例之间的网络是隔离的。

以上取值，不区分大小写。|

## 返回参数 {#section_f54_lk5_xdb .section}

全是公共返回参数。参阅 [公共参数](cn.zh-CN/API 参考/快速入门/公共参数.md#commonResponseParameters)。

## 示例 { .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=ModifySecurityGroupPolicy
&RegionId=cn-hangzhou
&SecurityGroupId=sg-1133aa
&InnerAccessPolicy=Drop
&<公共请求参数>
```

**返回示例** 

**XML 格式**

```
<ModifySecurityGroupPolicyResponse>
    <RequestId>CEF72CEB-54B6-4AE8-B225-F876xxxxxxxx</RequestId>
</ModifySecurityGroupPolicyResponse>
```

 **JSON 格式** 

```
{
    "RequestId": "CEF72CEB-54B6-4AE8-B225-F876FF7BA984"
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问 [API 错误中心](https://error-center.aliyun.com/status/product/Ecs)。

|错误代码|错误信息|HTTP 状态码|说明|
|:---|:---|:-------|:-|
|InvalidPolicy.Malformed|The InnerAccessPolicy is invalid. Only Accept and Drop are supported.|400|缺少参数 `InnerAccessPolicy`或者参数不合法。|
|InvalidSecurityGroupId.Malformed|The SecurityGroupId is invalid. Only letters, numbers and underscores are supported. Maximum length is 100 characters.|400|缺少参数 `SecurityGroupId` 或者参数不合法。|
|InvalidRegionId.NotFound|The RegionId provided does not exist.|404|指定的 `RegionId` 不存在。|

