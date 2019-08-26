# AuthorizeSecurityGroupEgress {#doc_api_Ecs_AuthorizeSecurityGroupEgress .reference}

调用AuthorizeSecurityGroupEgress增加一条安全组出方向规则。指定安全组出方向的访问权限，允许或者拒绝安全组里的实例发送出方向流量到其他设备。

## 接口说明 {#description .section}

本文中，出方向流量的发起端为源端（Source），数据传输的接收端为目的端（Destination）。

调用该接口时，您需要了解：

-   一个安全组的安全组规则最多为100条。
-   安全组规则分为接受访问（accept）和拒绝访问（drop）两类。
-   安全组规则优先级（Priority）可选范围为1~100。数字越小，代表优先级越高。
-   优先级相同的安全组规则，优先以拒绝访问（drop）的规则为准。
-   目的端设备可以是指定的IP地址范围（DestCidrIp），也可以是其他安全组（DestGroupId）。
-   以下任意一组参数可以确定一条安全组规则。如果匹配的安全组规则已存在，此次 AuthorizeSecurityGroupEgress调用失败。
    -   设置指定IP地址段的访问权限。经典网络类型安全组的网卡类型（NicType）可设置公网（internet）和内网（intranet）。VPC类型安全组的网卡类型（NicType）只可设置内网（intranet）。如以下请求示例：IpProtocol、PortRange、（可选）SourcePortRange、NicType、Policy、DestCidrIp和（可选）SourceCidrIp。

        ```
        
                https://ecs.aliyuncs.com/?Action=AuthorizeSecurityGroupEgress
                &SecurityGroupId=sg-94n63e80l
                &IpProtocol=icmp
                &DestCidrIp=10.0.0.0/8
                &PortRange=-1/-1
                &NicType=intranet
                &Policy=Allow
                &<公共请求参数>
                
        ```

    -   设置其他安全组的访问权限。网卡类型（NicType）只能为内网（intranet）。经典网络类型安全组之间互访时，可以设置同一地域中其他安全组对您的安全组的访问权限。这个安全组可以是您的也可以是其他阿里云账户（DestGroupOwnerAccount）的。VPC类型安全组之间互访时，可以设置同一VPC内其他安全组对该安全组的访问权限。。如以下请求示例：IpProtocol、PortRange、（可选）SourcePortRange、NicType、Policy、（可选）DestCidrIp、DestGroupOwnerAccount和DestGroupI。

        ```
        
                https://ecs.aliyuncs.com/?Action=AuthorizeSecurityGroupEgress
                &SecurityGroupId=sg-F876FF7BA
                &DestGroupId=sg-1651FBB64
                &DestGroupOwnerAccount=test@aliyun.com
                &IpProtocol=tcp
                &PortRange=22/22
                &NicType=intranet
                &Policy=Drop
                &<公共请求参数>
                
        ```


## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=AuthorizeSecurityGroupEgress&type=RPC&version=2014-05-26)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|IpProtocol|String|是|all|传输层协议。取值大小写敏感。取值范围：

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
|RegionId|String|是|cn-hangzhou|源端安全组所属地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。

 |
|SecurityGroupId|String|是|sg-securitygroupid1|源端安全组ID。

 |
|Action|String|否|AuthorizeSecurityGroupEgress|系统规定参数。取值：AuthorizeSecurityGroupEgress

 |
|ClientToken|String|否|123e4567-e89b-12d3-a456-426655440000|保证请求幂等性。从您的客户端生成一个参数值，确保不同请求间该参数值唯一。**ClientToken**只支持ASCII字符，且不能超过64个字符。更多详情，请参见[如何保证幂等性](~~25693~~)。

 |
|Description|String|否|FinanceJoshua|安全组规则的描述信息。长度为1~512个字符。

 |
|DestCidrIp|String|否|10.0.0.0/8|目的端IP地址范围。支持CIDR格式和IPv4格式的IP地址范围。

 默认值：无。

 |
|DestGroupId|String|否|sg-securitygroupid2|需要设置访问权限的目的端安全组ID。

 至少设置一项DestGroupId或者DestCidrIp参数。

 如果指定了DestGroupId没有指定参数DestCidrIp，则参数NicType取值只能为intranet。

 如果同时指定了DestGroupId和DestCidrIp，则默认以DestCidrIp为准。

 |
|DestGroupOwnerAccount|String|否|FinanceJoshua|跨账户设置安全组规则时，目的端安全组所属的阿里云账户。

 -   如果DestGroupOwnerAccount及DestGroupOwnerId均未设置，则认为是设置您其他安全组的访问权限。
-   如果已经设置参数DestCidrIp，则参数DestGroupOwnerAccount无效。

 |
|DestGroupOwnerId|Long|否|155780923770|跨账户设置安全组规则时，目的端安全组所属的阿里云账户ID。

 -   如果DestGroupOwnerId及DestGroupOwnerAccount均未设置，则认为是设置您其他安全组的访问权限。
-   如果您已经设置参数DestCidrIp，则参数DestGroupOwnerId无效。

 |
|Ipv6DestCidrIp|String|否|2001:db8:1233:1a00::\*\*\*|目的端IPv6 CIDR地址段。支持CIDR格式和IPv6格式的IP地址范围。

 默认值：无。

 **说明：** 仅支持VPC类型的IP地址。

 |
|Ipv6SourceCidrIp|String|否|2001:db8:1234:1a00::\*\*\*|源端IPv6 CIDR地址段。支持CIDR格式和IPv6格式的IP地址范围。

 默认值：无。

 **说明：** 仅支持VPC类型的IP地址。

 |
|NicType|String|否|intranet|网卡类型。取值范围：

 -   internet：公网网卡。
-   intranet：内网网卡。

 当设置安全组之间互相访问时，即指定了DestGroupId且没有指定DestCidrIp时，参数NicType取值只能为intranet。

 默认值：internet。

 |
|Policy|String|否|accept|设置访问权限。取值范围：

 -   accept：接受访问。
-   drop：拒绝访问，不返回拒绝信息。

 默认值：accept。

 |
|Priority|String|否|1|安全组规则优先级。取值范围：1~100

 默认值：1。

 |
|SourceCidrIp|String|否|10.0.0.0/8|源端IP地址范围。支持CIDR格式和IPv4格式的IP地址范围。

 默认值：无。

 |
|SourcePortRange|String|否|80/80|源端安全组开放的传输层协议相关的端口范围。取值范围：

 -   TCP/UDP协议：1~65535。使用斜线（/）隔开起始端口和终止端口。正确示范：1/200；错误示范：200/1。
-   ICMP协议：-1/-1。
-   GRE协议：-1/-1。
-   all：-1/-1。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=AuthorizeSecurityGroupEgress
&SecurityGroupId=sg-F876FF7**
&DestGroupId=sg-1651FBB**
&DestGroupOwnerAccount=test@aliyun.com
&IpProtocol=tcp
&PortRange=22/22
&NicType=intranet
&Policy=Drop
&<公共请求参数>
```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<AuthorizeSecurityGroupEgressResponse>
      <RequestId>CEF72CEB-54B6-4AE8-B225-F876FF7BA984</RequestId>
</AuthorizeSecurityGroupEgressResponse>
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
|400|InvalidPriority.Malformed|The parameter Priority is invalid.|无效的规则优先级。|
|400|InvalidPriority.ValueNotSupported|The parameter Priority is invalid.|无效的规则优先级。|
|400|InvalidDestCidrIp.Malformed|The specified parameter DestCidrIp is not valid.|指定的 DestCidrIp 无效，请您检查该参数是否正确。|
|500|InternalError|The request processing has failed due to some unknown error.|内部错误，请重试。如果多次尝试失败，请提交工单|
|403|InvalidNetworkType.Conflict|The specified SecurityGroup network type should be same with SourceGroup network type \(vpc or classic\).|指定的 SecurityGroup 的网络类型必须与 SouceGroup 的网络类型一致。|
|403|InvalidSecurityGroup.IsSame|The authorized SecurityGroupId should be different from the DestGroupId.|已授权的 SecurityGroupId 不能与 DestGroupId 相同。|
|400|InvalidDestCidrIp.Malformed|The parameter DestCidrIp is not valid.|指定的目的CIDR地址段无效。|
|403|InvalidNetworkType.Conflict|The parameter SecurityGroup network type should be same with SourceGroup network type \(vpc or classic\).|安全组网络类型必须和源安全组网络类型一致。|
|400|InvalidNicType.ValueNotSupported|The parameter NicType is not valid.|指定的NicType无效。|
|400|InvalidSecurityGroupDiscription.Malformed|The specified security group rule description is not valid.|指定的安全组规则描述不合法。|
|400|InvalidSecurityGroup.InvalidNetworkType|The specified security group network type is not support this operation, please check the security group network types. For VPC security groups, ClassicLink must be enabled.|无效的网络类型。|
|400|MissingParameter.Dest|Either DestCidrIp or DestGroupId must be specified.|DestCidrIp和DestGroupId不能同时为空。|
|400|InvalidParam.PortRange|Please specify the PortRange or SourcePortRange in integer, less than 65535, and separate the range with ?/?.|请指定目的端口范围或者源端口范围，端口号要小于65535，如果是端口范围需要使用"/"分隔。|
|400|InvalidIpProtocol.ValueNotSupported|The parameter IpProtocol must be specified with case insensitive TCP, UDP, ICMP, GRE or All.|协议类型只能是TCP， UDP， ICMP， GRE 或者 All。|
|400|InvalidParam.SourceIp|%s|无效的源IP。|
|400|InvalidParam.DestIp|%s|无效的目的IP。|
|400|InvalidParam.Ipv6DestCidrIp|%s|无效的目的IP\(v6格式\)。|
|400|InvalidParam.Ipv6SourceCidrIp|%s|无效的源IP\(v6格式\)。|
|400|InvalidParam.Ipv4ProtocolConflictWithIpv6Address|%s|IPv4和IPv6不能同时存在。|
|400|InvalidParam.Ipv6ProtocolConflictWithIpv4Address|%s|IPv6和IPv4不能同时存在。|
|400|ILLEGAL\_IPV6\_CIDR|%s|指定的IPv6地址段无效。|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

