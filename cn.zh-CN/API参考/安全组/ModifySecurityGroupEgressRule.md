# ModifySecurityGroupEgressRule {#doc_api_Ecs_ModifySecurityGroupEgressRule .reference}

修改安全组出方向规则的描述信息。如果您还没有增加过安全组规则，可以调用 AuthorizeSecurityGroupEgress 增加。

## 接口说明 {#description .section}

以下任意一组参数可以确定一条安全组出方向规则，只指定一个参数无法确定一条安全组规则。

-   授权指定 IP 地址段的访问权限：IpProtocol、PortRange、（可选）SourcePortRange、NicType、Policy、DestCiderIp 和 （可选）SourceCidrIp
-   授权其他安全组的访问权限：IpProtocol、PortRange、（可选）SourcePortRange、NicType、Policy、（可选）DestCiderIp、DestGroupOwnerAccount 和 DestGroupId

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=ModifySecurityGroupEgressRule)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|IpProtocol|String|是|tcp|传输层协议。不区分大小写。取值范围：

 -   icmp
-   gre
-   tcp
-   udp
-   all：支持所有协议

 |
|PortRange|String|是|80/80|源端安全组开放的传输层协议相关的端口范围。取值范围：

 -   TCP/UDP 协议：取值范围为 1~65535。使用斜线（/）隔开起始端口和终止端口。正确示范：1/200；错误示范：200/1。
-   ICMP 协议：-1/-1 。
-   GRE 协议：-1/-1。
-   all：-1/-1 。

 |
|RegionId|String|是|cn-hangzhou|源端安全组所属地域 ID。您可以调用 [DescribeRegions](~~25609~~) 查看最新的阿里云地域列表。

 |
|SecurityGroupId|String|是|sg-securitygroupid1|源端安全组 ID。

 |
|Action|String|否|ModifySecurityGroupEgressRule|系统规定参数。取值：ModifySecurityGroupRule

 |
|ClientToken|String|否|123e4567-e89b-12d3-a456-426655440000|保证请求幂等性。从您的客户端生成一个参数值，确保不同请求间该参数值唯一。**ClientToken** 只支持 ASCII 字符，且不能超过 64 个字符。更多详情，请参阅 [如何保证幂等性](~~25693~~)。

 |
|Description|String|否|Thisisanewsecuritygrouprule|安全组规则的描述信息。长度为 1~512 个字符。

 |
|DestCidrIp|String|否|XXX.XX.XXX.XX|目的端 IP 地址范围。支持 CIDR 格式和 IPv4 格式的 IP 地址范围。默认值：0.0.0.0/0

 |
|DestGroupId|String|否|sg-securitygroupid22|目的端安全组ID。

 |
|DestGroupOwnerAccount|String|否|EcsforCloud@Alibaba.com|目的端安全组所属的账号ID，亦即UID。

 |
|DestGroupOwnerId|Long|否|155780923770|目的端安全组所属的账号登录名称。

 |
|Ipv6DestCidrIp|String|否|2001:db8:1234:1a00::XXX|目的端 IP 地址范围。支持 CIDR 格式和 IPv6 格式的 IP 地址范围。

 |
|Ipv6SourceCidrIp|String|否|2001:db8:1234:1a00::XXX|源端 IP 地址范围。支持 CIDR 格式和 IPv6 格式的 IP 地址范围。

 |
|NicType|String|否|internet|网卡类型。取值范围：

 -   internet：公网网卡。
-   intranet：内网网卡。

 当设置安全组之间互相访问时，即指定了 DestGroupId且没有指定 DestCidrIp 时，参数 NicType 取值只能为 intranet。

 |
|Policy|String|否|accept|访问权限。取值范围：

 -   accept：接受访问。
-   drop：拒绝访问，不发回拒绝信息。

 默认值：accept

 |
|Priority|String|否|1|安全组规则优先级。取值范围：1~100

 默认值：1

 |
|SourceCidrIp|String|否|XXX.XX.XXX.XX|源端 IP 地址范围。支持 CIDR 格式和 IPv4 格式的 IP 地址范围。

 |
|SourcePortRange|String|否|80/80|源端安全组开放的传输层协议相关的端口范围。取值范围：

 -   TCP/UDP 协议：取值范围为 1~65535。使用斜线（/）隔开起始端口和终止端口。正确示范：1/200；错误示范：200/1。
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

https://ecs.aliyuncs.com/?Action=ModifySecurityGroupEgressRule
&SecurityGroupId=sg-F876FF7BA
&SourceGroupId=sg-1651FBB64
&SourceGroupOwnerAccount=test@aliyun.com
&IpProtocol=tcp
&PortRange=80/80
&Policy=allow
&Description=Thisisanewsecuritygrouprule.
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ModifySecurityGroupEgressRuleResponse>
  <RequestId>CEF72CEB-54B6-4AE8-B225-F876FF7BA984</RequestId>
</ModifySecurityGroupEgressRuleResponse>

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
|404|InvalidDestGroupId.NotFound|The DestGroupId provided does not exist in our records.|指定的出方向安全组不存在|
|400|OperationDenied|The specified IpProtocol does not exist or IpProtocol and PortRange do not match.|指定的 IP 协议不存在，或与端口范围不匹配。|
|400|InvalidIpProtocol.Malformed|The specified parameter "PortRange" is not valid.|IP协议参数格式不正确。|
|403|InvalidDestGroupId.Mismatch|NicType is required or NicType expects intranet.|请指定 NicType，或使用内网模式。|
|400|InvalidDestCidrIp.Malformed|The specified parameter "DestCidrIp" is not valid.|指定的 DestCidrIp 无效，请您检查该参数是否正确。|
|403|MissingParameter|The input parameter "DestGroupId" or "DestCidrIp" cannot be both blank.|参数 DestGroupId 和 DestCidrIp 不得为空。|
|400|InvalidPolicy.Malformed|The specified parameter "Policy" is not valid.|指定的参数无效，请您检查该参数是否正确。|
|400|InvalidNicType.ValueNotSupported|The specified NicType does not exist.|指定的网络类型不存在，请您检查网络类型是否正确。|
|400|InvalidNicType.Mismatch|Specified nic type conflicts with the authorization record.|指定的 NIC 类型不存在。|
|403|AuthorizationLimitExceed|The limit of authorization records in the security group reaches.|安全组授权规则数达到上限，请您检查授权规则是否合理。|
|403|InvalidParamter.Conflict|The specified SecurityGroupId should be different from the SourceGroupId.|授权与被授权安全组必须不同|
|400|InvalidDestGroupId.Mismatch|Specified security group and destination group are not in the same VPC.|指定的安全组和目标组不在同一个 VPC 下。|
|400|InvalidDestGroup.NotFound|Specified destination security group does not exist.|指定的出方向安全组不存在|
|400|VPCDisabled|Can't use the SecurityGroup in VPC.|VPC 不支持安全组。|
|400|InvalidPriority.Malformed|The specified parameter "Priority" is not valid.|指定的 Priority 参数不合法。|
|400|InvalidPriority.ValueNotSupported|The specified Priority is invalid.|无效的规则优先级。|
|400|InvalidDestCidrIp.Malformed|The specified parameter DestCidrIp is not valid.|指定的 DestCidrIp 无效，请您检查该参数是否正确。|
|500|InternalError|The request processing has failed due to some unknown error.|内部错误，请重试。如果多次尝试失败，请提交工单|
|403|InvalidNetworkType.Conflict|The specified SecurityGroup network type should be same with SourceGroup network type \(vpc or classic\).|指定的 SecurityGroup 的网络类型必须与 SouceGroup 的网络类型一致。|
|403|InvalidSecurityGroup.IsSame|The authorized SecurityGroupId should be different from the DestGroupId.|已授权的 SecurityGroupId 不能与 DestGroupId 相同。|
|400|InvalidNicType.ValueNotSupported|The specified NicType is not valid.|指定的网络类型不存在，请您检查网络类型是否正确。|
|400|InvalidSecurityGroupDiscription.Malformed|The specified security group rule description is not valid.|指定的安全组规则描述不合法。|
|404|SecurityGroupRule.NotFound|The target security group rule do not exist.|目标安全组规则不存在。|
|400|InvalidSecurityGroup.InvalidNetworkType|The specified security group network type is not support this operation, please check the security group network types. For VPC security groups, ClassicLink must be enabled.|无效的网络类型。|
|400|MissingParameter.Dest|The parameter DestCidrIp or DestGroupId is essential.|DestCidrIp和DestGroupId不能同时为空。|
|400|InvalidParam.PortRange|The specified param PortRange or SourcePortRange is not valid. should be integer and less than 65535, range separator is '/'.|指定的参数无效。|
|400|InvalidIpProtocol.ValueNotSupported|The specified parameter IpProtocol should not be null and only tcp, udp, icmp, gre or all is supported. Ignore case.|协议类型只能是TCP, UDP, ICMP, GRE 或者 All.。|
|400|InvalidPriority.ValueNotSupported|The parameter Priority is invalid.|无效的规则优先级。|
|400|InvalidParam.SourceIp|%s|无效的源IP。|
|400|InvalidParam.DestIp|%s|无效的目的IP。|
|400|InvalidParam.Ipv6DestCidrIp|%s|无效的目的IP\(v6格式\)。|
|400|InvalidParam.Ipv6SourceCidrIp|%s|无效的源IP\(v6格式\)。|
|400|InvalidParam.Ipv4ProtocolConflictWithIpv6Address|%s|IPv4和IPv6不能同时存在。|
|400|InvalidParam.Ipv6ProtocolConflictWithIpv4Address|%s|IPv6和IPv4不能同时存在。|
|400|ILLEGAL\_IPV6\_CIDR|%s|指定的IPv6地址段无效。|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Ecs)

