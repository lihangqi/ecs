# ModifySecurityGroupRule {#ModifySecurityGroupRule .reference}

修改安全组入方向规则的描述信息。如果您还没有增加过安全组规则，可以调用 [AuthorizeSecurityGroup](intl.zh-CN/API 参考/安全组/AuthorizeSecurityGroup.md#) 增加。

## 描述 {#section_vqh_lhn_ydb .section}

以下任意一组参数可以确定一条安全组入方向规则，只指定一个参数无法确定一条安全组规则。

-   授权指定 IP 地址段的访问权限：`IpProtocol`、`PortRange`、（可选）`SourcePortRange`、`NicType`、`Policy`、`DestCiderIp` 和 （可选）`SourceCidrIp`

-   授权其他安全组的访问权限：`IpProtocol`、`PortRange`、（可选）`SourcePortRange`、`NicType`、`Policy`、（可选）`DestCiderIp`、`DestGroupOwnerAccount` 和 `DestGroupId`


## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：ModifySecurityGroupRule|
|RegionId|String|是|目标安全组所属地域 ID。您可以调用 [DescribeRegions](intl.zh-CN/API 参考/地域/DescribeRegions.md#) 查看最新的阿里云地域列表。|
|SecurityGroupId|String|是|目标安全组 ID。|
|Description|String|是|安全组规则的描述信息。长度为 \[1, 512\] 个字符。|
|IpProtocol|String|是|传输层协议。不区分大小写。取值范围：-   icmp
-   gre
-   tcp
-   udp
-   all：支持所有协议

|
|PortRange|String|是|目的端安全组开放的传输层协议相关的端口范围。取值范围：-   TCP/UDP 协议：取值范围为 \[1, 65535\] 。使用斜线（/）隔开起始端口和终止端口。正确示范：`1/200`；错误示范：`200/1`。
-   ICMP 协议：-1/-1 。
-   GRE 协议：-1/-1。
-   all：-1/-1 。

|
|SourcePortRange|String|否|源端安全组开放的传输层协议相关的端口范围。取值范围：-   TCP/UDP 协议：取值范围为 \[1, 65535\] 。使用斜线（/）隔开起始端口和终止端口。正确示范：`1/200`；错误示范：`200/1`。
-   ICMP 协议：-1/-1。
-   GRE 协议：-1/-1。
-   all：-1/-1。

|
|NicType|String|否|网卡类型。取值范围：-   internet：公网网卡。
-   intranet：内网网卡。

当设置安全组之间互相访问时，即指定了 `DestGroupId`且没有指定 `DestCidrIp` 时，参数 `NicType` 取值只能为 `intranet`。 默认值：internet|
|Policy|String|否|访问权限。取值范围：-   accept：接受访问。
-   drop：拒绝访问，不发回拒绝信息。

默认值：accept|
|DestCidrIp|String|否|目的端 IP 地址范围。支持 CIDR 格式和 IPv4 格式的 IP 地址范围。默认值：0.0.0.0/0|
|SourceCidrIp|String|否|源端 IP 地址范围。支持 CIDR 格式和 IPv4 格式的 IP 地址范围。默认值：0.0.0.0/0|
|SourceGroupId|String|否|设置访问权限的源端安全组 ID。必须设置 `SourceGroupId` 或者 `SourceCidrIp` 参数。如果指定了 `SourceGroupId` 没有指定参数 `SourceCidrIp`，则参数 `NicType` 取值只能为 `intranet`。如果同时指定了 `SourceGroupId` 和 `SourceCidrIp`，则默认以 `SourceCidrIp` 为准。|
|SourceGroupOwnerAccount|String|否|跨账户设置安全组规则时，源端安全组所属的阿里云账户。-   如果 `SourceGroupOwnerAccount` 及 `SourceGroupOwnerID` 均未设置，则认为是设置您其他安全组的访问权限。
-   如果已经设置参数 `SourceCidrIp`，则参数 `SourceGroupOwnerAccount` 无效。

|
|SourceGroupOwnerId|String|否|跨账户设置安全组规则时，源端安全组所属的阿里云账户 ID。-   如果 `SourceGroupOwnerId` 及 `SourceGroupOwnerAccount` 均未设置，则认为是设置您其他安全组的访问权限。
-   如果您已经设置参数 `SourceCidrIp`，则参数 `SourceGroupOwnerId` 无效。

|
|Priority|String|否|安全组规则优先级。取值范围：\[1, 100\] 默认值：1|

## 返回参数 {#section_f54_lk5_xdb .section}

全是公共返回参数。参阅 [公共参数](intl.zh-CN/API 参考/快速入门/公共参数.md#)。

## 示例 { .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=ModifySecurityGroupRule
&SecurityGroupId=sg-F876FF7BA
&SourceGroupId=sg-1651FBB64
&SourceGroupOwnerAccount=test@aliyun.com
&IpProtocol=tcp
&PortRange=80/80
&Policy=allow
&Description=This is a new security group rule.
&<公共请求参数>
```

**返回示例** 

**XML 格式**

```
<ModifySecurityGroupRuleResponse>
    <RequestId>CEF72CEB-54B6-4AE8-B225-F876FF7BA984</RequestId>
</ModifySecurityGroupRuleResponse>
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
|InvalidIpProtocol.Malformed|The specified parameter “IpProtocol” is not valid.|400|指定的参数 `IpProtocol` 不合法。|
|InvalidNicType.Mismatch|Specified nic type conflicts with the authorization record.|400|指定网卡类型 `NicType` 与安全组规则不符合。|
|InvalidNicType.ValueNotSupported|The specified NicType does notexist.|400|指定的参数 `NicType`不存在。|
|InvalidPolicy.Malformed|The specified parameter “Policy” is not valid.|400|指定的参数 `Policy`不合法。|
|InvalidPriority.Malformed|The specified parameter “Priority” is not valid.|400|指定的参数 `Priority` 不合法。|
|InvalidPriority.ValueNotSupported|The specified Priority isinvalid.|400|指定的参数 `Priority` 不合法。|
|InvalidSecurityGroupDiscription.Malformed|The specified security group rule description is not valid.|400|安全组规则的描述 `Description` 不合法。|
|InvalidSourceCidrIp.Malformed|The specified parameter “SourceCidrIp” is not valid.|400|指定的参数 `SourceCidrIp` 不合法。|
|InvalidSourceGroup.NotFound|The specified SourceGroupId does not exist.|400|指定的源端安全组 `SourceGroupId` 不存在。|
|InvalidSourceGroupId.Mismatch|Specified security group and source group are not in the same VPC.|400|指定安全组的网络类型是 VPC，源端安全组必须在同一个 VPC 里。|
|OperationDenied|The specified IpProtocol does not exist or IpProtocol and PortRange do not match.|400|指定的参数 `IpProtocol` 不存在。或者指定的 IP 协议和端口范围不匹配。|
|InvalidNetworkType.Mismatch|The specified SecurityGroup network type should be same with SourceGroup network type \(vpc or classic\).|403|安全组规则中两个安全组的网络类型必须相同，即必须同时为经典网络或者 VPC。|
|InvalidParamter.Conflict|The specified SecurityGroupId should be different from the SourceGroupId.|403|参数 `SecurityGroupId`和 `SourceGroupId`取值不能相同。|
|InvalidSourceGroupId.Mismatch|NicType is required or NicType expects intranet.|403|需要明确 `NicType` 参数。或者 `NicType` 必须为 `intranet`。|
|MissingParameter|The input parameter “SourceGroupId” or “SourceCidrIp” cannot be both blank.|403|必须指定参数 `SourceGroupId` 或者 `SourceCidrIp`。|
|InvalidRegionId.NotFound|The specified RegionId does not exist.|404|指定的 `RegionId` 不存在。|
|InvalidSecurityGroupId.NotFound|The specified SecurityGroupId does not exist.|404|指定的 `SecurityGroupId`不存在。|
|InvalidSourceGroupId.NotFound|The SourceGroupId provided does not exist in our records.|404|指定的 `SourceGroupId` 不存在。|

