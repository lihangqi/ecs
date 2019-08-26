# DescribeSecurityGroupAttribute {#DescribeSecurityGroupAttribute .reference}

查询安全组详情。

## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：DescribeSecurityGroupAttribute|
|RegionId|String|是|安全组所属地域 ID。您可以调用 [DescribeRegions](intl.zh-CN/API参考/地域/DescribeRegions.md#) 查看最新的阿里云地域列表。|
|SecurityGroupId|String|是|安全组 ID。|
|NicType|String|否|网卡类型。取值范围：-   internet：公网
-   intranet：内网

默认值：internet|
|Direction|String|否|安全组规则授权方向。取值范围：-   egress：安全组出方向
-   ingress：安全组入方向
-   all：不区分方向

默认值：all|

## 返回参数 {#ResponseParameter .section}

|名称|类型|描述|
|:-|:-|:-|
|SecurityGroupId|String|目标安全组 ID|
|SecurityGroupName|String|目标安全组名称|
|RegionId|String|地域 ID|
|Description|String|安全组描述信息|
|InnerAccessPolicy|String|安全组内网络连通策略。可能值：-   Accept：内网互通
-   Drop：内网隔离

|
|Permissions|[PermissionType](intl.zh-CN/API参考/数据类型/PermissionType.md#)|安全组权限规则集合|
|VpcId|String|VPC ID。如果返回 VPC ID，表示该安全组网络类型为 VPC。否则，表示是经典网络类型安全组。|

## 示例 { .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=DescribeSecurityGroupAttribute
&RegionId=cn-hangzhou
&SecurityGroupId=sg-F876FF7BA
&<公共请求参数>
```

**返回示例** 

**XML 格式**

```
<DescribeSecurityGroupAttributeResponse>
     <RequestId>1651FBB6-4FBF-49FF-A9F5-DF5D696C7EC6</RequestId>
     <RegionId>cn-hangzhou</RegionId>
     <SecurityGroupId>C0003E8B-B930-4F59-ADC0-0E209A9012B0</SecurityGroupId>
     <Description>for demo</Description>
     <InnerAccessPolicy>Accept</InnerAccessPolicy>
        <Permissions>
         <Permission>
              <IpProtocol>ALL</IpProtocol>
              <PortRange>-1/-1</PortRange>
                <SourceGroupId>8dsmf982</SourceGroupId>
                <SourceGroupOwnerAccount>test@aliyun.com</SourceGroupOwnerAccount>
              <Policy>Accept</Policy>
              <NicType>intranet</NicType>
         </Permission>
          <Permission>
              <IpProtocol>tcp</IpProtocol>
              <PortRange>1/65535</PortRange>
              <SourceCidrIp>0.0.0.0/0</SourceCidrIp>
              <Policy>accept</Policy>
              <NicType>internet</NicType>
         </Permission>
     </Permissions>
</DescribeSecurityGroupAttributeResponse>
```

 **JSON 格式** 

```
{
    "RequestId": "1651FBB6-4FBF-49FF-A9F5-DF5D696C7EC6",
    "RegionId": "cn-hangzhou",
    "SecurityGroupId": "C0003E8B-B930-4F59-ADC0-0E209A9012B0",
    "Description": "for demo",
    "Permissions": {
        "Permission": [{
            "IpProtocol": "ALL",
            "PortRange": "-1/-1",
            "SourceGroupId": "8dsmf982",
            "SourceGroupOwnerAccount": "test@aliyun.com"
            "Policy": "Accept",
            "NicType": "intranet"
        },
        {
            "IpProtocol": "tcp",
            "PortRange": "1/65535",
            "SourceCidrIp": "0.0.0.0/0",
            "Policy": "accept",
            "NicType": "internet"
        }]
    }
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问 [API 错误中心](https://error-center.alibabacloud.com/status/product/Ecs)。

|错误代码|错误信息|HTTP 状态码|说明|
|:---|:---|:-------|:-|
|InvalidNicType.ValueNotSupported|The specified NicType does not exist.|400|指定的 `NicType` 不存在。|
|InvalidRegionId.NotFound|The specified RegionId does not exist.|404|指定的 `RegionId` 不存在。|
|InvalidSecurityGroupId.NotFound|The specified SecurityGroupId does not exist.|404|指定的 `SecurityGroupId` 不存在。|

