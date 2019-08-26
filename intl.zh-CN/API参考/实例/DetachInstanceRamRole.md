# DetachInstanceRamRole {#doc_api_1161585 .reference}

收回一台或多台ECS实例的实例RAM角色。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=DetachInstanceRamRole)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|InstanceIds|String|是|\["instanceId1", "instanceId2", "instanceId3"…\]|指定收回的实例ID的集合。最多支持一次查询100台实例。

 |
|RegionId|String|是|cn-hangzhou|地域 ID。您可以调用 [DescribeRegions](~~25609~~) 查看最新的阿里云地域列表。

 |
|Action|String|否|DetachInstanceRamRole|系统规定参数。取值：DetachInstanceRamRole

 |
|RamRoleName|String|否|RamRoleTest|收回赋予了某一实例RAM角色的所有ECS实例。您可以使用 RAM API [ListRoles](~~28713~~) 查询您已创建的实例 RAM 角色。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|DetachInstanceRamRoleResults| | |由实例RAM角色类型（DetachInstanceRamRoleResult）组成的信息集。

 |
|└Code|String|200|判断是否成功收回实例RAM角色。返回值为200表示成功收回，返回其他值表示收回失败，失败原因参阅错误码。

 |
|└InstanceId|String|i-instance1|准备收回实例RAM角色的ECS实例。

 |
|└InstanceRamRoleSets| | |实例的RAM角色集合。

 |
|└InstanceId|String|i-instance1|实例 ID。

 |
|└RamRoleName|String|RamRoleTest|收回实例RAM角色的名称。

 |
|└Message|String|Success|判断是否成功收回实例RAM角色。返回值为Success表示成功收回，返回其他值表示收回失败，失败原因参阅错误码。

 |
|└Success|Boolean|true|是否成功回收了指定的实例角色

 |
|FailCount|Integer|0|收回失败的实例RAM角色的个数。

 |
|RamRoleName|String|RamRoleTest|收回实例RAM角色的名称。

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。

 |
|TotalCount|Integer|1|收回的实例RAM角色的总个数。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

https://ecs.aliyuncs.com/?Action=DetachInstanceRamRole
&InstanceIds=i-instance1
&RegionId=cn-hangzhou
&RamRoleName=RamRoleTest
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DetachInstanceRamRoleResponse>
  <RequestId>E6352369-5C2B-41CD-AB50-471550C8F674</RequestId>
  <DetachInstanceRamRoleResults>
    <DetachInstanceRamRoleResult>
      <InstanceId>i-instance1</InstanceId>
      <Code>200</Code>
      <Message>success</Message>
    </DetachInstanceRamRoleResult>
  </DetachInstanceRamRoleResults>
  <TotalCount>1</TotalCount>
  <FailCount>0</FailCount>
  <RamRoleName>RamRoleTest</RamRoleName>
</DetachInstanceRamRoleResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"TotalCount":1,
	"DetachInstanceRamRoleResults":{
		"DetachInstanceRamRoleResult":[
			{
				"Message":"success",
				"InstanceId":"i-instance1",
				"Code":"200"
			}
		]
	},
	"RequestId":"E6352369-5C2B-41CD-AB50-471550C8F674",
	"RamRoleName":"RamRoleTest",
	"FailCount":0
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/Ecs)

