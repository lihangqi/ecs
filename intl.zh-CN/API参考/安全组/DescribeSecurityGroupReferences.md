# DescribeSecurityGroupReferences {#doc_api_1031572 .reference}

查询一个安全组和其他哪些安全组有安全组级别的授权行为。

## 接口说明 {#description .section}

调用该接口时，您需要注意：

-   授权行为包括入方向授权和出方向授权。
-   该接口单次最多返回 100 条记录。
-   当您无法删除某一安全组（[DeleteSecurityGroup](~~25558~~)）时，可以调用该接口查看指定的安全组是否已被其他安全组授权。如果指定的安全组已被授权，您需要在删除该安全组之前解除授权行为。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=DescribeSecurityGroupReferences)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|RegionId|String|是|cn-hangzhou|安全组所属地域。

 |
|SecurityGroupId.N|RepeatList|是|sg-securitygroupid1|要查询的第 n 个 SecurityGroupId，n 的取值范围为 1~10。

 |
|Action|String|否|DescribeSecurityGroupReferences|系统规定参数。取值：DescribeSecurityGroupReferences

 |
|OwnerAccount|String|否|ECSforCloud@Alibaba.com|RAM用户的账号登录名称。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。

 |
|SecurityGroupReferences| | |所有用户指定的安全组被引用的完整信息

 |
|└ReferencingSecurityGroups| | |正在引用这个安全组的其他安全组信息

 |
|└AliUid|String|155780923770|这个安全组所属用户 ID

 |
|└SecurityGroupId|String|sg-securitygroupid1|安全组 ID

 |
|└SecurityGroupId|String|sg-securitygroupid2|对应用户要查询的一个安全组

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

https://ecs.aliyuncs.com/?Action=DescribeSecurityGroupReferences
&RegionId=cn-hangzhou
&SecurityGroupId.1=sg-1133aa
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeSecurityGroupReferencesResponse>
  <RequestId>CEF72CEB-54B6-4AE8-B225-F876FF7BA984</RequestId>
  <SecurityGroupReferences>
    <SecurityGroupReference>
      <SecurityGroupId>sg-1133aa</SecurityGroupId>
      <ReferencingSecurityGroups>
        <ReferencingSecurityGroup>
          <SecurityGroupId>sg-2255cc</SecurityGroupId>
          <AliUid>123</AliUid>
        </ReferencingSecurityGroup>
        <ReferencingSecurityGroup>
          <SecurityGroupId>sg-2255dd</SecurityGroupId>
          <AliUid>123</AliUid>
        </ReferencingSecurityGroup>
      </ReferencingSecurityGroups>
    </SecurityGroupReference>
  </SecurityGroupReferences>
</DescribeSecurityGroupReferencesResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"CEF72CEB-54B6-4AE8-B225-F876FF7BA984",
	"SecurityGroupReferences":[
		{
			"SecurityReferencingGroups":[
				{
					"SecurityGroupId":"sg-2255cc",
					"AliUid":123
				},
				{
					"SecurityGroupId":"sg-2255dd",
					"AliUid":123
				}
			],
			"SecurityGroupId":"sg-1133aa"
		}
	]
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InvalidSecurityGroupId.Malformed|The specified parameter SecurityGroupId is essential and size should less than 10|无效的安全组ID。|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Ecs)

