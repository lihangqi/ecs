# JoinSecurityGroup {#JoinSecurityGroup .reference}

将一台实例加入到指定的安全组。

## 描述 {#section_xnq_ms1_ydb .section}

调用该接口时，您需要注意：

-   加入安全组之前，实例必须处于 **已停止**（`Stopped`）或者 **运行中**（`Running`）状态。

-   一台实例最多可以加入 5 个安全组。您可以 [申请](https://selfservice.console.aliyun.com/ticket/createIndex.htm) 将实例加入更多安全组，最多不能超过 16 个安全组。

-   每个安全组最多能管理 1000 台实例。

-   您的安全组和实例必须属于同一个阿里云地域。

-   您的安全组和实例的网络类型必须相同。如果网络类型为 [专有网络 VPC](../../../../../cn.zh-CN/产品简介/什么是专有网络.md#)，则安全组和实例必须属于同一个 VPC。


## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：JoinSecurityGroup|
|InstanceId|String|是|实例 ID。您可以调用 [DescribeRegions](cn.zh-CN/API 参考/地域/DescribeRegions.md#) 查看最新的阿里云地域列表。|
|SecurityGroupId|String|是|安全组 ID。您可以调用 [DescribeSecurityGroups](cn.zh-CN/API 参考/安全组/DescribeSecurityGroups.md#) 查看您可用的安全组。|

## 返回参数 {#section_f54_lk5_xdb .section}

全是公共返回参数。参阅 [公共返回参数](cn.zh-CN/API 参考/快速入门/公共参数.md#commonResponseParameters)。

## 示例 { .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=JoinSecurityGroup
&InstanceId= i-instance1
&SecurityGroupId=F876FF7BA984
&<公共请求参数>
```

**返回示例** 

**XML 格式**

```
<JoinSecurityGroupResponse>
    <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</JoinSecurityGroupResponse>
```

**JSON 格式** 

```
{
    "RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E"
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问 [API 错误中心](https://error-center.aliyun.com/status/product/Ecs)。

|错误代码|错误信息|HTTP 状态码|说明|
|:---|:---|:-------|:-|
|InvalidInstanceId.Mismatch|Specified instance and security group are not in the same VPC.|400|指定的实例和安全组必须属于同一个 VPC。|
|InstanceSecurityGroupLimitExceeded|Exceeding the allowed amount of security groups that an instance can be in.|400|一台实例最多可以加入 5 个安全组。|
|MissingParameter|The input parameter “InstanceId” that is mandatory for processing this request is not supplied.|400|您必须填入 `InstanceId` 参数。|
|MissingParameter|The input parameter “SecurityGroupId” that is mandatory for processing this request is not supplied.|400|您必须填入 `SecurityGroupId` 参数。|
|IncorrectInstanceStatus|The current status of the resource does not support this operation.|403|加入安全组之前，实例必须处于 **已停止**（`Stopped`）或者 **运行中**（`Running`）状态。|
|InstanceLockedForSecurity|The specified operation is denied as your instance is locked for security reasons.|403|该资源目前被 [安全控制](cn.zh-CN/API 参考/附录/安全锁定时的 API 行为.md#)，拒绝操作。|
|SecurityGroupInstanceLimitExceeded|The maximum number of instances in a security group is exceeded.|403|每个安全组最多能管理 1000 台实例。|
|InvalidInstanceId.AlreadyExists|The specified instance already exists in the specified security group.|403|指定的实例已经在指定的安全组中。|
|OperationDenied|The specified operation is denied as your instance is locked for security reasons.|403|该资源目前被 [安全控制](cn.zh-CN/API 参考/附录/安全锁定时的 API 行为.md#)，拒绝操作。|
|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|404|指定的 `InstanceId`不存在。|
|InvalidSecurityGroupId.NotFound|The specified SecurityGroupId does not exist.|404|指定的 `SecurityGroupId` 不存在。|

