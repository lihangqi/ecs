# DescribeSecurityGroupReferences {#DescribeSecurityGroupReferences .reference}

查询一个安全组和其他哪些安全组有安全组级别的授权行为。

## 描述 {#section_dcn_yyr_zdb .section}

调用该接口时，您需要注意：

-   授权行为包括入方向授权和出方向授权。

-   该接口单次最多返回 100 条记录。

-   当您无法删除某一安全组（[DeleteSecurityGroup](cn.zh-CN/API 参考/安全组/DeleteSecurityGroup.md#)）时，可以调用该接口查看指定的安全组是否已被其他安全组授权。如果指定的安全组已被授权，您需要在删除该安全组之前解除授权行为。


## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：DescribeSecurityGroupReferences|
|SecurityGroupId.n|String|是|要查询的第 n 个 `SecurityGroupId`，`n` 的取值范围为 \[1, 10\]。|
|RegionId|String|是|安全组所属地域。您可以调用 [DescribeRegions](cn.zh-CN/API 参考/地域/DescribeRegions.md#) 查看最新的阿里云地域列表。|

## 返回参数 {#ResponseParameter .section}

|名称|类型|描述|
|:-|:-|:-|
|SecurityGroupReferences|[SecurityGroupReference](cn.zh-CN/API 参考/数据类型/SecurityGroupReference.md#)|所有用户指定的安全组被引用的完整信息|

## 示例 { .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=DescribeSecurityGroupReferences
&RegionId=cn-hangzhou
&SecurityGroupId.1=sg-1133aa
&<公共请求参数>
```

**返回示例** 

**XML 格式**

```
<DescribeSecurityGroupReferencesResponse>
    <RequestId>CEF72CEB-54B6-4AE8-B225-F876FF7BA984</RequestId>
    <SecurityGroupReferences>
      <SecurityGroupReference>
        <SecurityGroupId>sg-1133aa</SecurityGroupId>
        <ReferencingSecurityGroups>
          <ReferencingSecurityGroup>
            <SecurityGroupId>sg-2255cc</SecurityGroupId>
            <AliUid>123</AliUid>
          </ReferencingSecurityGroup>
          <ReferencingSecurityGroup>
            <SecurityGroupId>sg-2255dd</SecurityGroupId>
            <AliUid>123</AliUid>
          </ReferencingSecurityGroup>
        </ReferencingSecurityGroups>
      </SecurityGroupReference>
    </SecurityGroupReferences>
</DescribeSecurityGroupReferencesResponse>
```

 **JSON 格式** 

```
{
    "RequestId": "CEF72CEB-54B6-4AE8-B225-F876FF7BA984"
    "SecurityGroupReferences":[
        {
            "SecurityGroupId":"sg-1133aa",
            "SecurityReferencingGroups":[
                {
                    "AliUid":123,
                    "SecurityGroupId":"sg-2255cc"
                },
                {
                    "AliUid":123,
                    "SecurityGroupId":"sg-2255dd"
                }
            ]
        }
    ]
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问 [API 错误中心](https://error-center.aliyun.com/status/product/Ecs)。

|错误代码|错误信息|HTTP 状态码|说明|
|:---|:---|:-------|:-|
|Abs.GroupNos.Malformed|The specified parameter SecurityGroupId is essential and size should less than 10.|400|您必须输入参数 `SecurityGroupId.n`。或者 `SecurityGroupId.n` 中 `n` 不能超过 10。|
|InvalidSecurityGroupId.NotFound|The specified SecurityGroupId does not exist.|400|指定的安全组 ID 不存在。|
|InvalidRegionId.NotFound|The specified RegionId does not exist.|404|指定的 `RegionId` 不存在。|

