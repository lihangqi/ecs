# DescribeInstanceRamRole {#DescribeInstanceRamRole .reference}

查询一台或者多台 ECS 实例上的已赋予的 [实例 RAM 角色](../intl.zh-CN/用户指南/实例/实例RAM角色/什么是实例 RAM 角色.md#)。

## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：DescribeInstanceRamRole|
|InstanceIds|String|是|指定查询的实例 ID 的集合。最多支持一次查询 100 台实例，格式为 \["instanceId1", "instanceId2", "instanceId3"…\]。|
|RamRoleName|String|否|查询赋予了某一实例 RAM 角色的所有 ECS 实例。您可以使用 *RAM* API [ListRoles](../../../../../intl.zh-CN/API参考/API 参考（RAM）/角色管理接口/ListRoles.md#) 查询您已创建的实例 RAM 角色。|
|PageNumber|Integer|否|当前页码，起始值：1默认值：1

|
|PageSize|Integer|否|分页查询时设置的每页行数，最大值：50默认值：10

|

## 返回参数 {#ResponseParameter .section}

|名称|类型|描述|
|:-|:-|:-|
|InstanceRamRoleSets|Array|由实例 RAM 角色类型（[InstanceRamRoleSetType](intl.zh-CN/API 参考/数据类型/InstanceRamRoleSetType.md#)）组成的信息集|

## 示例 { .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=DescribeInstanceRamRole
&RegionId=cn-hangzhou
&InstanceIds=["i-instance1"]
&<公共请求参数>

```

**返回示例** 

**XML 格式**

```
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

 **JSON 格式** 

```
{
    "RequestId": "8F4CAE3F-7892-4662-83A5-2C2FFD639553",
    "InstanceRamRoleSets": {
        "InstanceRamRoleSet": [
            {
                "InstanceId": "i-instance1",
                "RamRoleName": "RamRoleTest"
            }
        ]
    },
    "TotalCount": 1
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问 [API 错误中心](https://error-center.alibabacloud.com/status/product/Ecs)。

|错误代码|错误信息|HTTP 状态码|说明|
|:---|:---|:-------|:-|
|InvalidInstanceIds.Malformed|The specified InstanceIds is not valid.|400|指定的 `InstanceIds` 不合法。|
|InvalidNetworkType.MismatchRamRole|Ram role cannot be attached to instances of Classic network type.|403|您指定的参数 `InstanceIds` 中包含了经典网络实例，实例 RAM 角色不支持经典网络类型。|
|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|404|指定的实例 ID 不存在。|
|InvalidRamRole.NotFound|The specified RamRoleName does not exist.|404|指定的 `RamRoleName` 不存在。|

