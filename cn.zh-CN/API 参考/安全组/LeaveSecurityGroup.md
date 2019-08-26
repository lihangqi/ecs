# LeaveSecurityGroup {#LeaveSecurityGroup .reference}

将一台实例移出指定的安全组。

## 描述 {#section_zp1_jt1_ydb .section}

调用该接口时，您需要注意：

-   移出安全组之前，实例必须处于 **已停止**（`Stopped`）或者 **运行中**（`Running`）状态。

-   一台实例必须至少加入一个安全组，当该实例只加入了一个安全组时，则 `LeaveSecurityGroup` 请求会失败。


## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：LeaveSecurityGroup|
|InstanceId|String|是|实例 ID。|
|SecurityGroupId|String|是|安全组 ID。|

## 返回参数 {#section_f54_lk5_xdb .section}

全是公共返回参数。参阅 [公共参数](intl.zh-CN/API参考/调用方式/公共参数.md#commonResponseParameters)。

## 示例 { .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=LeaveSecurityGroup
&InstanceId=i-instance1
&SecurityGroupId=F876FF7BA984
&<公共请求参数>
```

**返回示例** 

**XML 格式**

```
<LeaveSecurityGroupResponse>
    <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</LeaveSecurityGroupResponse>
```

 **JSON 格式** 

```
{
    "RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E"
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问 [API 错误中心](https://error-center.alibabacloud.com/status/product/Ecs)。

|错误代码|错误信息|HTTP 状态码|说明|
|:---|:---|:-------|:-|
|IncorrectInstanceStatus|The current status of the resource does not support this operation.|403|移出安全组之前，实例必须处于 **已停止**（`Stopped`）或者 **运行中**（`Running`）状态。|
|InstanceLastSecurityGroup|The specified security group is the last security group for the instance.|403|该安全组是该实例唯一的安全组，一台实例必须至少加入一个安全组。|
|InstanceLockedForSecurity|The specified operation is denied as your instance is locked for security reasons.|403|被 [安全控制](intl.zh-CN/API参考/附录/安全锁定时的 API 行为.md#) 的实例的 `OperationLocks` 中标记了 `"LockReason" : "security"` 时，无法移出安全组。|
|InstanceNotInSecurityGroup|The instance not in the group.|403|指定实例不在指定安全组中。|
|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|404|指定的 `InstanceId` 不存在。|
|InvalidSecurityGroupId.NotFound|The specified SecurityGroupId does not exist.|404|指定的 `SecurityGroupId` 不存在。|

