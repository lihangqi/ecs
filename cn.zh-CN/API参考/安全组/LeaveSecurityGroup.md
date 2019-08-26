# LeaveSecurityGroup {#doc_api_Ecs_LeaveSecurityGroup .reference}

调用LeaveSecurityGroup将一台实例移出指定的安全组。

## 接口说明 {#description .section}

调用该接口时，您需要注意：

-   移出安全组之前，实例必须处于 已停止（Stopped）或者 运行中（Running）状态。
-   一台实例必须至少加入一个安全组，当该实例只加入了一个安全组时，则 LeaveSecurityGroup 请求会失败。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=LeaveSecurityGroup)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|InstanceId|String|是|i-instanceid1|实例 ID。

 |
|SecurityGroupId|String|是|sg-securitygroupid1|安全组 ID。

 |
|Action|String|否|LeaveSecurityGroup|系统规定参数。取值：LeaveSecurityGroup

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

https://ecs.aliyuncs.com/?Action=LeaveSecurityGroup
&InstanceId=i-instance1
&SecurityGroupId=sg-F876FF7BA9**
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<LeaveSecurityGroupResponse>
  <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</LeaveSecurityGroupResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|404|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|指定的实例不存在，请您检查实例ID是否正确。|
|404|InvalidSecurityGroupId.NotFound|The specified SecurityGroupId does not exist.|指定的安全组在该用户账号下不存在，请您检查安全组id是否正确。|
|403|IncorrectInstanceStatus|The current status of the resource does not support this operation.|该资源目前的状态不支持此操作。|
|403|InstanceLockedForSecurity|The specified operation is denied as your instance is locked for security reasons.|实例被安全锁定，指定的操作无法完成。|
|403|InstanceNotInSecurityGroup|The instance not in the group.|指定的实例不在安全组内。|
|504|RequestTimeout|The request encounters an upstream server timeout.|上游服务器超时，请求被拒绝。|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

