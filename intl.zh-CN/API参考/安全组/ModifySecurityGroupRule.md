# ModifySecurityGroupRule {#doc_api_Ecs_ModifySecurityGroupRule .reference}

修改安全组入方向规则的描述信息。如果您还没有增加过安全组规则，可以调用 AuthorizeSecurityGroup 增加。

## 接口说明 {#description .section}

以下任意一组参数可以确定一条安全组入方向规则，只指定一个参数无法确定一条安全组规则。

-   授权指定 IP 地址段的访问权限：IpProtocol、PortRange、（可选）SourcePortRange、NicType、Policy、DestCidrIp 和 （可选）SourceCidrIp
-   授权其他安全组的访问权限：IpProtocol、PortRange、（可选）SourcePortRange、NicType、Policy、（可选）DestCidrIp、DestGroupOwnerAccount 和 DestGroupId

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=ModifySecurityGroupRule)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|IpProtocol|String|是|all|传输层协议。不区分大小写。取值范围：

 -   icmp
-   gre
-   tcp
-   udp
-   all：支持所有协议

 |
|PortRange|String|是|80/80|目的端安全组开放的传输层协议相关的端口范围。取值范围：

 -   TCP/UDP 协议：取值范围为 1~65535。使用斜线（/）隔开起始端口和终止端口。正确示范：1/200；错误示范：200/1。
-   ICMP 协议：-1/-1 。
-   GRE 协议：-1/-1。
-   all：-1/-1 。

 |
|RegionId|String|是|cn-hangzhou|目标安全组所属地域 ID。您可以调用 [DescribeRegions](~~25609~~) 查看最新的阿里云地域列表。

 |
|SecurityGroupId|String|是|sg-securitygroupid1|目标安全组 ID。

 |
|Action|String|否|ModifySecurityGroupRule|系统规定参数。取值：ModifySecurityGroupRule

 |
|ClientToken|String|否|123e4567-e89b-12d3-a456-426655440000|保证请求幂等性。从您的客户端生成一个参数值，确保不同请求间该参数值唯一。**ClientToken** 只支持 ASCII 字符，且不能超过 64 个字符。更多详情，请参阅 [如何保证幂等性](~~25693~~)。

 |
|Description|String|否|FinanceDept|安全组规则的描述信息。长度为 1~512 个字符。

 |
|DestCidrIp|String|否|10.0.0.0/8|目的端 IP 地址范围。支持 CIDR 格式和 IPv4 格式的 IP 地址范围。

 默认值：0.0.0.0/0

 |
|Ipv6DestCidrIp|String|否|2001:db8:1234:1a00::XXX|目的端 IPv6 CIDR 地址段。支持CIDR格式和IPv6格式的IP地址范围。

 **说明：** 仅支持 VPC 类型的 IP 地址。

 默认值：无。

 |
|Ipv6SourceCidrIp|String|否|2001:db8:1234:1a00::XXX|源端 IPv6 CIDR 地址段。支持CIDR格式和IPv6格式的IP地址范围。

 **说明：** 仅支持 VPC 类型的 IP 地址。

 默认值：无。

 |
|NicType|String|否|intranet|网卡类型。取值范围：

 -   internet：公网网卡。
-   intranet：内网网卡。

 当设置安全组之间互相访问时，即指定了 DestGroupId且没有指定 DestCidrIp 时，参数 NicType 取值只能为 intranet。 默认值：internet

 |
|Policy|String|否|accept|访问权限。取值范围：

 -   accept：接受访问。
-   drop：拒绝访问，不发回拒绝信息。

 默认值：accept

 |
|Priority|String|否|1|安全组规则优先级。取值范围：1~100

 默认值：1

 |
|SourceCidrIp|String|否|10.0.0.0/8|源端 IP 地址范围。支持 CIDR 格式和 IPv4 格式的 IP 地址范围。默认值：0.0.0.0/0

 |
|SourceGroupId|String|否|sg-securitygroupid2|设置访问权限的源端安全组 ID。必须设置 SourceGroupId 或者 SourceCidrIp 参数。

 如果指定了 SourceGroupId 没有指定参数 SourceCidrIp，则参数 NicType 取值只能为 intranet。如果同时指定了 SourceGroupId 和 SourceCidrIp，则默认以 SourceCidrIp 为准。

 |
|SourceGroupOwnerAccount|String|否|FinanceJoshua|跨账户设置安全组规则时，源端安全组所属的阿里云账户。

 -   如果 SourceGroupOwnerAccount 及 SourceGroupOwnerID 均未设置，则认为是设置您其他安全组的访问权限。
-   如果已经设置参数 SourceCidrIp，则参数 SourceGroupOwnerAccount 无效。

 |
|SourceGroupOwnerId|Long|否|155780923770|跨账户设置安全组规则时，源端安全组所属的阿里云账户 ID。

 -   如果 SourceGroupOwnerId 及 SourceGroupOwnerAccount 均未设置，则认为是设置您其他安全组的访问权限。
-   如果您已经设置参数 SourceCidrIp，则参数 SourceGroupOwnerId 无效。

 |
|SourcePortRange|String|否|80/80|源端安全组开放的传输层协议相关的端口范围。取值范围：

 -   TCP/UDP 协议：取值范围为 1~65535 。使用斜线（/）隔开起始端口和终止端口。正确示范：1/200；错误示范：200/1。
-   ICMP 协议：-1/-1。
-   GRE 协议：-1/-1。
-   all：-1/-1。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

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

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ModifySecurityGroupRuleResponse>
  <RequestId>CEF72CEB-54B6-4AE8-B225-F876FF7BA984</RequestId>
</ModifySecurityGroupRuleResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"CEF72CEB-54B6-4AE8-B225-F876FF7BA984"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|404|InvalidSecurityGroupId.NotFound|The specified SecurityGroupId does not exist.|指定的安全组在该用户账号下不存在，请您检查安全组id是否正确。|
|404|InvalidSourceGroupId.NotFound|The SourceGroupId provided does not exist in our records.|指定的入方向安全组不存在|
|400|OperationDenied|The specified IpProtocol does not exist or IpProtocol and PortRange do not match.|指定的 IP 协议不存在，或与端口范围不匹配。|
|400|InvalidIpProtocol.Malformed|The specified parameter "PortRange" is not valid.|IP协议参数格式不正确。|
|403|InvalidSourceGroupId.Mismatch|NicType is required or NicType expects intrnet.|需要明确IP段类型参数或者网络类型必须为内网。|
|400|InvalidSourceCidrIp.Malformed|The specified parameter "SourceCidrIp" is not valid.|源IP地址范围参数格式不正确。|
|403|MissingParameter|The input parameter "SourceGroupId" or "SourceCidrIp" cannot be both blank.|源ip或者源安全组不能同时为空。|
|400|InvalidPolicy.Malformed|The specified parameter "Policy" is not valid.|指定的参数无效，请您检查该参数是否正确。|
|400|InvalidNicType.ValueNotSupported|The specified NicType does not exist.|指定的网络类型不存在，请您检查网络类型是否正确。|
|400|InvalidNicType.Mismatch|Specified nic type conflicts with the authorization record.|指定的 NIC 类型不存在。|
|403|AuthorizationLimitExceed|The limit of authorization records in the security group reaches.|安全组授权规则数达到上限，请您检查授权规则是否合理。|
|403|InvalidParamter.Conflict|The specified SecurityGroupId should be different from the SourceGroupId.|授权与被授权安全组必须不同|
|400|InvalidSourceGroupId.Mismatch|Specified security group and source group are not in the same VPC.|指定的安全组和源安全组不在一个 VPC 内。|
|400|InvalidSourceGroup.NotFound|Specified source security group does not exist.|指定的入方向安全组不存在|
|400|VPCDisabled|Can't use the SecurityGroup in VPC.|VPC 不支持安全组。|
|400|InvalidPriority.Malformed|The parameter Priority is invalid.|无效的规则优先级。|
|400|InvalidPriority.ValueNotSupported|The parameter Priority is invalid.|无效的规则优先级。|
|500|InternalError|The request processing has failed due to some unknown error.|内部错误，请重试。如果多次尝试失败，请提交工单|
|403|InvalidNetworkType.Mismatch|The specified SecurityGroup network type should be same with SourceGroup network type \(vpc or classic\).|指定的 SecurityGroup 的网络类型必须与 SouceGroup 的网络类型一致。|
|400|InvalidSecurityGroupDiscription.Malformed|The specified security group rule description is not valid.|指定的安全组规则描述不合法。|
|404|SecurityGroupRule.NotFound|The target security group rule not exist.|目标安全组规则不存在。|
|400|MissingParameter.Source|Either SourceCidrIp or SourceGroupId must be specified.|源ip或者源安全组不能同时为空。|
|400|InvalidParam.PortRange|Please specify the PortRange or SourcePortRange in integer, less than 65535, and separate the range with ?/?.|请指定目的端口范围或者源端口范围，端口号要小于65535，如果是端口范围需要使用"/"分隔。|
|400|InvalidIpProtocol.ValueNotSupported|The parameter IpProtocol must be specified with case insensitive TCP, UDP, ICMP, GRE or All.|协议类型只能是TCP， UDP， ICMP， GRE 或者 All。|
|400|InvalidParam.SourceIp|%s|无效的源IP。|
|400|InvalidParam.DestIp|%s|无效的目的IP。|
|400|InvalidParam.Ipv6DestCidrIp|%s|无效的目的IP\(v6格式\)。|
|400|InvalidParam.Ipv6SourceCidrIp|%s|无效的源IP\(v6格式\)。|
|400|InvalidParam.Ipv4ProtocolConflictWithIpv6Address|%s|IPv4和IPv6不能同时存在。|
|400|InvalidParam.Ipv6ProtocolConflictWithIpv4Address|%s|IPv6和IPv4不能同时存在。|
|400|ILLEGAL\_IPV6\_CIDR|%s|指定的IPv6地址段无效。|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Ecs)

