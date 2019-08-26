# DeleteSecurityGroup {#DeleteSecurityGroup .reference}

删除一个安全组。删除安全组之前，请确保安全组内不存在实例，并且没有其他安全组与该安全组有授权行为（[DescribeSecurityGroupReferences](intl.zh-CN/API参考/安全组/DescribeSecurityGroupReferences.md#)），否则 `DeleteSecurityGroup` 请求失败。

## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：DeleteSecurityGroup|
|SecurityGroupId|String|是|安全组 ID。|
|RegionId|String|是|地域 ID。您可以调用 [DescribeRegions](intl.zh-CN/API参考/地域/DescribeRegions.md#) 查看最新的阿里云地域列表。|

## 返回参数 {#section_f54_lk5_xdb .section}

全是公共返回参数。参阅 [公共参数](intl.zh-CN/API参考/调用方式/公共参数.md#commonResponseParameters)。

## 示例 { .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=DeleteSecurityGroup
&RegionId=cn-hangzhou
&SecurityGroupId=sg-F876FF7BA
&<公共请求参数>
```

**返回示例** 

**XML 格式**

```
<DeleteSecurityGroupResponse>
     <RequestId>CEF72CEB-54B6-4AE8-B225-F876FF7BA984</RequestId>
</DeleteSecurityGroupResponse>
```

 **JSON 格式** 

```
{
    "RequestId":"CEF72CEB-54B6-4AE8-B225-F876FF7BA984"
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问 [API 错误中心](https://error-center.alibabacloud.com/status/product/Ecs)。

|错误代码|错误信息|HTTP 状态码|说明|
|:---|:---|:-------|:-|
|DependencyViolation|There is still instance\(s\) in the specified security group.|403|指定的安全组仍在管理实例。|
|DependencyViolation|The specified security group has been authorized in another one.|403|指定安全组被其他安全组授权。|
|InvalidRegionId.NotFound|The specified RegionId does not exist.|404|指定的 `RegionId` 不存在。|

