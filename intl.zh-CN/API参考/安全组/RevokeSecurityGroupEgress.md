# RevokeSecurityGroupEgress {#doc_api_1032052 .reference}

删除一条安全组出方向规则，撤销安全组出方向的访问权限。

## 接口说明 {#description .section}

本文定义出方向流量的发起端为源端（Source），数据传输的接收端为目的端（Destination）。

-   撤销对指定 IP 地址段的访问权限，如以下请求示例：IpProtocol、PortRange、（可选）SourcePortRange、NicType、Policy、DestCidrIp 和 （可选）SourceCidrIp

    ```
    
        https://ecs.aliyuncs.com/?Action=RevokeSecurityGroupEgress
        &SecurityGroupId=sg-94n63e80l
        &IpProtocol=all
        &DestCidrIp=10.0.0.0/8
        &PortRange=-1/-1
        &NicType=intranet
        &Policy=Allow
        &<公共请求参数>
        
    ```

-   撤销对其他安全组的访问权限，如以下请求示例：IpProtocol、PortRange、（可选）SourcePortRange、NicType、Policy、（可选）DestCidrIp、DestGroupOwnerAccount 和 DestGroupId

    ```
    
    https://ecs.aliyuncs.com/?Action=RevokeSecurityGroupEgress
    &SecurityGroupId=sg-F876FF7BA
    &DestGroupId=sg-1651FBB64
    &DestGroupOwnerAccount=test@aliyun.com
    &IpProtocol=tcp
    &PortRange=22/22
    &NicType=intranet
    &Policy=Drop
    &<公共请求参数>
    
    ```


## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=RevokeSecurityGroupEgress)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

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
|PortRange|String|是|1/200|目的端安全组开放的传输层协议相关的端口范围。取值范围：

 -   TCP/UDP 协议：取值范围为 1~65535。使用斜线（/）隔开起始端口和终止端口。正确示范：1/200；错误示范：200/1。
-   ICMP 协议：-1/-1。
-   GRE 协议：-1/-1。
-   all：-1/-1。

 |
|RegionId|String|是|cn-hangzhou|源端安全组所属地域 ID。您可以调用 [DescribeRegions](~~25609~~) 查看最新的阿里云地域列表。

 |
|SecurityGroupId|String|是|sg-securitygroupid1|源端安全组 ID。

 |
|Action|String|否|RevokeSecurityGroupEgress|系统规定参数。取值：RevokeSecurityGroupEgress

 |
|ClientToken|String|否|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|保证请求幂等性。从您的客户端生成一个参数值，确保不同请求间该参数值唯一。**ClientToken** 只支持 ASCII 字符，且不能超过 64 个字符。更多详情，请参阅 [如何保证幂等性](~~25693~~)。

 |
|Description|String|否|FinanceJoshuaTest|安全组规则的描述。

 |
|DestCidrIp|String|否|0.0.0.0/0|目的端 IP 地址范围。支持 CIDR 格式和 IPv4 格式的 IP 地址范围。默认值：无。

 |
|DestGroupId|String|否|sg-securitygroupid2|需要撤销访问权限的目的端安全组 ID。

 必须设置 DestGroupId 或者 DestCidrIp 参数。

 如果指定了 DestGroupId 没有指定参数 DestCidrIp，则参数 NicType 取值只能为 intranet。如果同时指定了 DestGroupId 和 DestCidrIp，则默认以 DestCidrIp 为准。

 |
|DestGroupOwnerAccount|String|否|FinanceJoshua|跨账户删除安全组规则时，目的端安全组所属的阿里云账户。

 -   如果 DestGroupOwnerAccount 及 DestGroupOwnerId 均未设置，则认为是撤销您其他安全组的访问权限。
-   如果已经设置参数 DestCidrIp，则参数 DestGroupOwnerAccount 无效。

 |
|DestGroupOwnerId|Long|否|155780923770|跨账户删除安全组规则时，目的端安全组所属的阿里云账户 ID。

 -   如果 DestGroupOwnerId 及 DestGroupOwnerAccount 均未设置，则认为是撤销您其他安全组的访问权限。
-   如果您已经设置参数 DestCidrIp，则参数 DestGroupOwnerId 无效。

 |
|Ipv6DestCidrIp|String|否|2001:db8:1234:1a00::XXX|目的端 IPv6 CIDR 地址段。支持 CIDR 格式和 IPv6 格式的 IP 地址范围。

 默认值：无。

 **说明：** 仅支持 VPC 类型的 IP 地址。

 |
|Ipv6SourceCidrIp|String|否|2001:db8:1234:1a00::XXX|源端 IPv6 CIDR 地址段。支持 CIDR 格式和 IPv6 格式的 IP 地址范围。

 默认值：无。

 **说明：** 仅支持 VPC 类型的 IP 地址。

 |
|NicType|String|否|intranet|网卡类型。取值范围：

 -   internet：公网网卡。
-   intranet：内网网卡。

 当撤销安全组之间互相访问时，即指定了 DestGroupId 且没有指定 DestCidrIp 时，参数 NicType 取值只能为 intranet。 默认值：internet

 |
|OwnerAccount|String|否|ECSforCloud@Alibaba.com|RAM用户的账号登录名称。

 |
|Policy|String|否|accept|访问权限。取值范围：

 -   accept：接受访问。
-   drop：拒绝访问，不发回拒绝信息。

 默认值：accept

 |
|Priority|String|否|1|安全组规则优先级。取值范围：1~100 默认值：1

 |
|SourceCidrIp|String|否|0.0.0.0/0|源端 IP 地址范围。支持 CIDR 格式和 IPv4 格式的 IP 地址范围。默认值：无。

 |
|SourcePortRange|String|否|1/200|源端安全组开放的传输层协议相关的端口范围。取值范围：

 -   TCP/UDP 协议：取值范围为 1~65535。使用斜线（/）隔开起始端口和终止端口。正确示范：1/200；错误示范：200/1。
-   ICMP 协议：-1/-1。
-   GRE 协议：-1/-1。
-   all：-1/-1。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。无论调用接口成功与否，我们都会返回请求 ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

https://ecs.aliyuncs.com/?Action=RevokeSecurityGroupEgress
&SecurityGroupId=sg-94n63e80l
&IpProtocol=all
&DestCidrIp=10.0.0.0/8
&PortRange=-1/-1
&NicType=intranet
&Policy=Allow
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<RevokeSecurityGroupEgressResponse>
  <RequestId>CEF72CEB-54B6-4AE8-B225-F876FF7BA984</RequestId>
</RevokeSecurityGroupEgressResponse>

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
|400|InvalidIpProtocol.ValueNotSupported|The specified IpProtocol does not exist.|IP协议参数指定的值不支持。|
|404|InvalidDestGroupId.NotFound|The DestGroupId provided does not exist in our records.|指定的出方向安全组不存在|
|403|InvalidNicType.Mismatch|Specified nic type conflicts with the authorization record.|指定的 NIC 类型不存在。|
|403|InvalidGroupAuthItem.NotFound|Specified group authorized item does not exist in our records.|指定的组授权条目不存在。|
|400|InvalidPolicy.Malformed|The specified parameter "Policy" is not valid.|指定的参数无效，请您检查该参数是否正确。|
|400|InvalidDestCidrIp.Malformed|The specified parameter "DestCidrIp" is not valid.|指定的 DestCidrIp 无效，请您检查该参数是否正确。|
|400|MissingParameter.Dest|Either DestCidrIp or DestGroupId must be specified.|DestCidrIp和DestGroupId不能同时为空。|
|400|InvalidParam.PortRange|Please specify the PortRange or SourcePortRange in integer, less than 65535, and separate the range with ?/?.|请指定目的端口范围或者源端口范围，端口号要小于65535，如果是端口范围需要使用"/"分隔。|
|400|InvalidIpProtocol.ValueNotSupported|The parameter IpProtocol must be specified with case insensitive TCP, UDP, ICMP, GRE or All.|协议类型只能是TCP， UDP， ICMP， GRE 或者 All。|
|400|InvalidPriority.Malformed|The parameter Priority is invalid.|无效的规则优先级。|
|400|InvalidPriority.ValueNotSupported|The parameter Priority is invalid.|无效的规则优先级。|
|400|InvalidParam.SourceIp|%s|无效的源IP。|
|400|InvalidParam.DestIp|%s|无效的目的IP。|
|400|InvalidParam.Ipv6DestCidrIp|%s|无效的目的IP\(v6格式\)。|
|400|InvalidParam.Ipv6SourceCidrIp|%s|无效的源IP\(v6格式\)。|
|400|InvalidParam.Ipv4ProtocolConflictWithIpv6Address|%s|IPv4和IPv6不能同时存在。|
|400|InvalidParam.Ipv6ProtocolConflictWithIpv4Address|%s|IPv6和IPv4不能同时存在。|
|400|ILLEGAL\_IPV6\_CIDR|%s|指定的IPv6地址段无效。|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Ecs)

