# DescribeInstanceRamRole {#doc_api_1161572 .reference}

查询一台或者多台 ECS 实例上的已赋予的实例 RAM 角色。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=DescribeInstanceRamRole)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|RegionId|String|是|cn-hangzhou|实例 RAM 角色所在的地域。您可以调用 [DescribeRegions](~~25609~~) 查看最新的阿里云地域列表。

 |
|Action|String|否|DescribeInstanceRamRole|接口名称，取值：**DescribeInstanceRamRole**

 |
|InstanceIds|String|否|\["instanceId1", "instanceId2", "instanceId3"…\]|指定查询的实例 ID 的集合。最多支持一次查询 100 台实例。

 |
|PageNumber|Integer|否|1|查询接口返回资源信息列表的页码。

 起始值：1。

 默认值：1。

 |
|PageSize|Integer|否|10|分页展示响应信息时设置的每页行数，单位：行。

 最大值：100。

 默认值：10。

 |
|RamRoleName|String|否|FinanceDeptOnly|查询赋予了某一实例 RAM 角色的所有 ECS 实例。您可以使用 RAM API [ListRoles](~~28713~~) 查询您已创建的实例 RAM 角色。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|InstanceRamRoleSets| | |由实例 RAM 角色类型（**InstanceRamRoleSetType**）组成的信息集。

 |
|└InstanceId|String|i-instance1|实例 ID

 |
|└RamRoleName|String|FinanceDeptOnly|实例的 RAM 角色名称列表

 |
|RegionId|String|cn-hangzhou|实例 RAM 角色所在的地域。您可以调用 [DescribeRegions](~~25609~~) 查看最新的阿里云地域列表。

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。

 |
|TotalCount|Integer|1|返回的 RAM 角色数量。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

https://ecs.aliyuncs.com/?Action=DescribeInstanceRamRole
&RegionId=cn-hangzhou
&InstanceIds=["i-instance1"]
&PageNumber=1
&PageSize=10
&RamRoleName=FinanceDeptOnly
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeInstanceRamRoleResponse>
  <RequestId>8F4CAE3F-7892-4662-83A5-2C2FFD639553</RequestId>
  <InstanceRamRoleSets>
    <InstanceRamRoleSet>
      <InstanceId>i-instance1</InstanceId>
      <RamRoleName>RamRoleTest</RamRoleName>
    </InstanceRamRoleSet>
  </InstanceRamRoleSets>
  <TotalCount>1</TotalCount>
</DescribeInstanceRamRoleResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"TotalCount":1,
	"RequestId":"8F4CAE3F-7892-4662-83A5-2C2FFD639553",
	"InstanceRamRoleSets":{
		"InstanceRamRoleSet":[
			{
				"InstanceId":"i-instance1",
				"RamRoleName":"RamRoleTest"
			}
		]
	}
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|403|InvalidParameter.AllEmpty|%s|缺失必需参数。|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Ecs)

