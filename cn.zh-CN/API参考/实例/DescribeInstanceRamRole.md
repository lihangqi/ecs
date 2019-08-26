# DescribeInstanceRamRole {#doc_api_Ecs_DescribeInstanceRamRole .reference}

调用DescribeInstanceRamRole查询一台或者多台ECS实例上的已赋予的实例RAM角色。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=DescribeInstanceRamRole&type=RPC&version=2014-05-26)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|RegionId|String|是|cn-hangzhou|实例RAM角色所在的地域。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。

 |
|Action|String|否|DescribeInstanceRamRole|接口名称。对于您自行拼凑HTTP/HTTPS URL发起的API请求，`Action`为必选参数。取值：DescribeInstanceRamRole

 |
|InstanceIds|String|否|\["instanceId1", "instanceId2", "instanceId3"…\]|指定查询的实例ID的集合。最多支持一次查询100台实例。

 |
|PageNumber|Integer|否|1|查询接口返回资源信息列表的页码。

 起始值：1。

 默认值：1。

 |
|PageSize|Integer|否|10|分页展示响应信息时设置的每页行数，单位：行。

 最大值：50。

 默认值：10。

 |
|RamRoleName|String|否|FinanceDeptOnly|查询赋予了某一实例RAM角色的所有ECS实例。您可以使用RAM API [ListRoles](~~28713~~)查询您已创建的实例RAM角色。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|InstanceRamRoleSets| | |由实例RAM角色类型（**InstanceRamRoleSetType**）组成的信息集。

 |
|InstanceId|String|i-instance1|实例ID。

 |
|RamRoleName|String|FinanceDeptOnly|实例RAM角色名称列表。

 |
|RegionId|String|cn-hangzhou|实例RAM角色所在的地域。

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。

 |
|TotalCount|Integer|1|返回的RAM角色数量。

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
|400|InvalidInstanceIds.Malformed|The specified instanceIds are not valid.|指定的多个 InstanceId 不合法。|
|404|InvalidInstanceId.NotFound|The specified instanceId does not exist|指定的实例不存在，请您检查实例ID是否正确。|
|403|InvalidNetworkType.MismatchRamRole|Ram role cannot be applied to instances of Classic network type.|实例 RAM 角色不能被用于经典网络实例，RAM 角色只能使用在 VPC 实例上。|
|403|InvalidParameter.AllEmpty|%s|缺失必需参数。|
|500|InternalError|The request processing has failed due to some unknown error.|内部错误，请重试。如果多次尝试失败，请提交工单|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

