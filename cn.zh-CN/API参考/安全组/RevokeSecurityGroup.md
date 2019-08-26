# RevokeSecurityGroup {#doc_api_Ecs_RevokeSecurityGroup .reference}

删除一条安全组入方向规则，撤销安全组入方向的权限设置。

## 接口说明 {#description .section}

本文定义出方向流量的发起端为源端（Source），数据传输的接收端为目的端（Destination）。

以下任意一组参数可以确定一条安全组入方向规则，只指定一个参数无法确定一条安全组规则。

-   撤销指定 IP 地址段的权限设置：IpProtocol、PortRange、（可选）SourcePortRange、NicType、Policy、DestCidrIp 和 （可选）SourceCidrIp。
-   撤销其他安全组的权限设置：IpProtocol、PortRange、（可选）SourcePortRange、NicType、Policy、（可选）DestCidrIp、DestGroupOwnerAccount 和 DestGroupId。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=RevokeSecurityGroup)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|IpProtocol|String|是|all|传输层协议。参数值大小写敏感。取值范围：

 -   icmp
-   gre
-   tcp
-   udp
-   all：支持所有协议

 |
|PortRange|String|是|1/200|目的端安全组开放的传输层协议相关的端口范围。取值范围：

 -   TCP/UDP协议：取值范围为1~65535。使用斜线（/）隔开起始端口和终止端口。正确示范：1/200；错误示范：200/1。
-   ICMP协议：-1/-1。
-   GRE协议：-1/-1。
-   all：-1/-1。

 |
|RegionId|String|是|cn-hangzhou|目的端安全组所属地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。

 |
|SecurityGroupId|String|是|sg-securitygroupid1|目的端安全组ID。

 |
|Action|String|否|RevokeSecurityGroup|系统规定参数。对于您自行拼凑HTTP/HTTPS URL发起的API请求，`Action`为必选参数。取值：RevokeSecurityGroup

 |
|ClientToken|String|否|123e4567-e89b-12d3-a456-426655440000|保证请求幂等性。从您的客户端生成一个参数值，确保不同请求间该参数值唯一。**ClientToken**只支持ASCII字符，且不能超过64个字符。更多详情，请参见[如何保证幂等性](~~25693~~)。

 |
|Description|String|否|FinanceJoshuaTest|安全组规则描述。

 |
|DestCidrIp|String|否|10.0.0.0/8|目的端IP地址范围。支持CIDR格式和IPv4格式的IP地址范围。默认值：0.0.0.0/0

 |
|Ipv6DestCidrIp|String|否|2001:db8:1234:1a00::XXX|目的端IPv6 CIDR地址段。支持CIDR格式和IPv6格式的IP地址范围。

 **说明：** 仅支持VPC类型的IP地址。

 默认值：无。

 |
|Ipv6SourceCidrIp|String|否|2001:db8:1234:1a00::XXX|源端IPv6 CIDR地址段。支持CIDR格式和IPv6格式的IP地址范围。

 **说明：** 仅支持VPC类型的IP地址。

 默认值：无。

 |
|NicType|String|否|intranet|网卡类型。取值范围：

 -   internet：公网网卡。
-   intranet：内网网卡。

 当撤销安全组之间互相访问时，即指定了SourceGroupId且没有指定SourceCidrIp时，参数NicType取值只能为intranet。 默认值：internet

 |
|Policy|String|否|accept|访问权限。取值范围：

 -   accept：接受访问。
-   drop：拒绝访问，不发回拒绝信息。

 默认值：accept

 |
|Priority|String|否|1|安全组规则优先级。取值范围：1~100

 默认值：1

 |
|SourceCidrIp|String|否|10.0.0.0/8|源端IP地址范围。支持CIDR格式和IPv4格式的IP地址范围。默认值：0.0.0.0/0

 |
|SourceGroupId|String|否|sg-securitygroupid2|需要撤销访问权限的源端安全组ID。

 必须设置SourceGroupId或者SourceCidrIp参数。

 如果指定了SourceGroupId没有指定参数SourceCidrIp，则参数NicType取值只能为intranet。如果同时指定了SourceGroupId和SourceCidrIp，则默认以SourceCidrIp为准。

 |
|SourceGroupOwnerAccount|String|否|FinanceJoshua|跨账户删除安全组规则时，源端安全组所属的阿里云账户。

 -   如果SourceGroupOwnerAccount及SourceGroupOwnerId均未设置，则认为是撤销您其他安全组的访问权限。
-   如果已经设置参数SourceCidrIp，则参数SourceGroupOwnerAccount无效。

 |
|SourceGroupOwnerId|Long|否|155780923770|跨账户删除安全组规则时，源端安全组所属的阿里云账户ID。

 -   如果SourceGroupOwnerId及SourceGroupOwnerAccount均未设置，则认为是撤销您其他安全组的访问权限。
-   如果您已经设置参数SourceCidrIp，则参数SourceGroupOwnerId无效。

 |
|SourcePortRange|String|否|1/200|源端安全组开放的传输层协议相关的端口范围。取值范围：

 -   TCP/UDP协议：取值范围为1~65535。使用斜线（/）隔开起始端口和终止端口。正确示范：1/200；错误示范：200/1。
-   ICMP协议：-1/-1。
-   GRE协议：-1/-1。
-   all：-1/-1。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=RevokeSecurityGroup
&SecurityGroupId=C0003E8B-B930-4F59-ADC0-0E209A9012B0
&SourceGroupId=sg-F876FF7BA
&SourceGroupOwnerAccount=test@aliyun.com
&IpProtocol=tcp
&PortRange=1/65535
&Priority=1
&<公共请求参数>
```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<RevokeSecurityGroupResponse>
  <RequestId>CEF72CEB-54B6-4AE8-B225-F876FF7BA984</RequestId>
</RevokeSecurityGroupResponse>

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
|400|InvalidSecurityGroupId.Malformed|The specified SecurityGroupId is not valid.|指定的 SecurityGroupId 不合法。|
|400|InvalidIpProtocol.ValueNotSupported|The specified IpProtocol does not exist.|IP协议参数指定的值不支持。|
|400|InvalidIpPortRange.Malformed|The specified parameter "PortRange" is not valid.|IP协议相关的端口号范围格式不正确。|
|404|InvalidSourceGroupId.NotFound|The SourceGroupId provided does not exist in our records.|指定的入方向安全组不存在|
|403|InvalidNicType.Mismatch|Specified nic type conflicts with the authorization record.|指定的 NIC 类型不存在。|
|403|InvalidGroupAuthItem.NotFound|Specified group authorized item does not exist in our records.|指定的组授权条目不存在。|
|400|InvalidSourceCidrIp.Malformed|The specified parameter "SourceCidrIp" is not valid.|源IP地址范围参数格式不正确。|
|400|MissingParameter|The input parameter "SourceGroupId" or "SourceCidrIp" cannot be both blank.|源ip或者源安全组不能同时为空。|
|400|InvalidPolicy.Malformed|The specified parameter "Policy" is not valid.|指定的参数无效，请您检查该参数是否正确。|
|400|InvalidNicType.ValueNotSupported|The specified NicType does not exist.|指定的网络类型不存在，请您检查网络类型是否正确。|
|400|InvalidSourceGroupId.Mismatch|Specified security group and source group are not in the same VPC.|指定的安全组和源安全组不在一个 VPC 内。|
|400|VPCDisabled|Can't use the SecurityGroup in VPC.|VPC 不支持安全组。|
|500|InternalError|The request processing has failed due to some unknown error.|内部错误，请重试。如果多次尝试失败，请提交工单|
|400|MissingParameter.Source|Either SourceCidrIp or SourceGroupId must be specified.|源ip或者源安全组不能同时为空。|
|400|InvalidParam.PortRange|Please specify the PortRange or SourcePortRange in integer, less than 65535, and separate the range with ?/?.|请指定目的端口范围或者源端口范围，端口号要小于65535，如果是端口范围需要使用"/"分隔。|
|400|InvalidIpProtocol.ValueNotSupported|The parameter IpProtocol must be specified with case insensitive TCP, UDP, ICMP, GRE or All.|协议类型只能是TCP， UDP， ICMP， GRE 或者 All。|
|400|InvalidPriority.Malformed|The parameter Priority is invalid.|无效的规则优先级。|
|400|InvalidPriority.ValueNotSupported|The parameter Priority is invalid.|无效的规则优先级。|
|400|InvalidParamter.Conflict|The specified SecurityGroupId should be different from the SourceGroupId.|授权与被授权安全组必须不同|
|400|InvalidParam.SourceIp|%s|无效的源IP。|
|400|InvalidParam.DestIp|%s|无效的目的IP。|
|400|InvalidParam.Ipv6DestCidrIp|%s|无效的目的IP\(v6格式\)。|
|400|InvalidParam.Ipv6SourceCidrIp|%s|无效的源IP\(v6格式\)。|
|400|InvalidParam.Ipv4ProtocolConflictWithIpv6Address|%s|IPv4和IPv6不能同时存在。|
|400|InvalidParam.Ipv6ProtocolConflictWithIpv4Address|%s|IPv6和IPv4不能同时存在。|
|400|ILLEGAL\_IPV6\_CIDR|%s|指定的IPv6地址段无效。|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Ecs)

