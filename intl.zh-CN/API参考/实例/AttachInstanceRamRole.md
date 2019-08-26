# AttachInstanceRamRole {#doc_api_1161570 .reference}

为一台或多台 ECS 实例授予 实例 RAM 角色。如果实例已有 RAM 角色，则报错提示您不能附加新的角色。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=AttachInstanceRamRole)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|InstanceIds|String|是|\[“instanceId1”, “instanceId2”, “instanceId3”…\]|实例ID的集合，最多支持100台实例。

 |
|RamRoleName|String|是|RamRoleTest|实例RAM角色名称。您可以使用 RAM API [ListRoles](~~28713~~) 查询您已创建的实例 RAM 角色。

 |
|RegionId|String|是|cn-hangzhou|地域ID。您可以调用 [DescribeRegions](~~25609~~) 查看最新的阿里云地域列表。

 |
|Action|String|否|AttachInstanceRamRole|系统规定参数。取值：AttachInstanceRamRole

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|AttachInstanceRamRoleResults| | |由实例RAM角色类型（AttachInstanceRamRoleResult）组成的信息集。

 |
|└Code|String|200|判断是否成功收回实例RAM角色。返回值为200表示成功收回，返回其他值表示收回失败，失败原因参阅错误码。

 |
|└InstanceId|String|i-instanceid1|实例 ID。

 |
|└Message|String|success|判断是否成功收回实例RAM角色。返回值为Success表示成功收回，返回其他值表示收回失败，失败原因参阅错误码。

 |
|└Success|Boolean|true|是否成功授予实例RAM角色。

 |
|FailCount|Integer|0|授予实例RAM角色的失败个数。

 |
|RamRoleName|String|RamRoleTest|实例RAM角色的名称。

 |
|RequestId|String|D9553E4C-6C3A-4D66-AE79-9835AF705639|请求 ID。无论调用接口成功与否，我们都会返回请求 ID。

 |
|TotalCount|Integer|1|授予的实例 RAM 角色总个数。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

https://ecs.aliyuncs.com/?Action=AttachInstanceRamRole
&InstanceIds=["i-instance1"]
&RamRoleName=RamRoleTest
&RegionId=cn-hangzhou
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<AttachInstanceRamRoleResponse>
  <RequestId>E6352369-5C2B-41CD-AB50-471550C8F674</RequestId>
  <AttachInstanceRamRoleResults>
    <AttachInstanceRamRoleResult>
      <InstanceId>i-instance1</InstanceId>
      <Code>200</Code>
      <Message>success</Message>
    </AttachInstanceRamRoleResult>
  </AttachInstanceRamRoleResults>
  <TotalCount>1</TotalCount>
  <FailCount>0</FailCount>
  <RamRoleName>RamRoleTest</RamRoleName>
</AttachInstanceRamRoleResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"TotalCount":1,
	"RequestId":"D9553E4C-6C3A-4D66-AE79-9835AF705639",
	"AttachInstanceRamRoleResults":{
		"AttachInstanceRamRoleResult":[
			{
				"Message":"success",
				"InstanceId":"i-instance1",
				"Code":"200"
			}
		]
	},
	"RamRoleName":"RamRoleTest",
	"FailCount":0
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|404|InvalidRamRole.NotEcsRole|The specified ram role is not authorized for ecs, please check your role policy.|RAM角色不具备访问ECS的权限。|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Ecs)

