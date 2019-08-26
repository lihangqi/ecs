# JoinSecurityGroup {#doc_api_Ecs_JoinSecurityGroup .reference}

将一台实例加入到指定的安全组。

## 接口说明 {#description .section}

调用该接口时，您需要注意：

-   加入安全组之前，实例必须处于**已停止**（Stopped）或者**运行中**（Running）状态。
-   一台实例最多可以加入五个安全组。
-   您可以 [提交工单](https://workorder-intl.console.aliyun.com/#/ticket/createIndex) 申请将实例加入更多安全组，最多不能超过 16 个安全组。
-   每个安全组最多能管理 1000 台实例。
-   您的安全组和实例必须属于同一个阿里云地域。
-   您的安全组和实例的网络类型必须相同。如果网络类型为 [专有网络 VPC](~~34217~~)，则安全组和实例必须属于同一个 VPC。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=JoinSecurityGroup)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|InstanceId|String|是|i-instanceid1|实例 ID。您可以调用 [DescribeRegions](~~25609~~) 查看最新的阿里云地域列表。

 |
|SecurityGroupId|String|是|sg-securitygroupid1|安全组 ID。您可以调用 [DescribeSecurityGroups](~~25556~~) 查看您可用的安全组。

 |
|Action|String|否|JoinSecurityGroup|系统规定参数。取值：JoinSecurityGroup

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=JoinSecurityGroup
&InstanceId= i-instance1
&SecurityGroupId=F876FF7BA984
&<公共请求参数>
```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<JoinSecurityGroupResponse>
  <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</JoinSecurityGroupResponse>

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
|404|InvalidSecurityGroupId.NotFound|The specified SecurityGroupId does not exist.|指定的安全组在该用户账号下不存在，请您检查安全组id是否正确。|
|400|InstanceSecurityGroupLimitExceeded|Exceeding the allowed amount of security groups that an instance can be in.|加入安全组失败，该实例加入的安全组数量已达到上限。|
|403|IncorrectInstanceStatus|The current status of the resource does not support this operation.|该资源目前的状态不支持此操作。|
|403|InstanceLockedForSecurity|The specified operation is denied as your instance is locked for security reasons.|实例被安全锁定，指定的操作无法完成。|
|403|SecurityGroupInstanceLimitExceeded|The maximum number of instances in a security group is exceeded.|该安全组内已有的实例数量已超出最大限制。|
|404|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|指定的实例不存在，请您检查实例ID是否正确。|
|400|InvalidInstanceId.Mismatch|Specified instance and security group are not in the same VPC.|指定的实例和安全组不属于同一个虚拟专有网络（包含另外两种特殊情况：1.实例不属于vpc类型的，安全组属于vpc类型2.实例属于vpc类型，安全组不属于vpc类型）。|
|403|InvalidInstanceId.AlreadyExists|The specified instance already exists in the specified security group.|指定的实例已存在于该安全组内。|
|500|InternalError|The request processing has failed due to some unknown error.|内部错误，请重试。如果多次尝试失败，请提交工单|
|403|SecurityGroupInstanceLimitExceeded|%s|该安全组内已有的实例数量已超出最大限制。|
|403|AclLimitExceed|%s|AccessPoint已超出限额值。|
|403|InstanceSecurityGroupLimitExceeded|%s|实例能加入的安全组数量已达上限制。|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Ecs)

