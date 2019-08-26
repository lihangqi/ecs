# AuthorizeSecurityGroup {#AuthorizeSecurityGroup .reference}

增加一条安全组入方向规则。指定安全组入方向的访问权限，允许或者拒绝其他设备发送入方向流量到安全组里的实例。

## 描述 {#Description .section}

我们定义入方向流量的发起端为源端（Source），数据传输的接收端为目的端（Destination），如下图所示。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9917/15395031993982_zh-CN.png)

调用该接口时，您需要了解：

-   一个安全组的安全组规则最多为 100 条。

-   安全组规则分为接受访问（`accept`）和拒绝访问（`drop`）两类。

-   安全组规则优先级（`Priority`）可选范围为 \[1, 100\]。数字越小，代表优先级越高。

-   优先级相同的安全组规则，以拒绝访问（`drop`）的规则优先。

-   源端设备可以是指定 IP 地址范围（`SourceCidrIp`），也可以是其他安全组（`SourceGroupId`）中的实例。

-   以下任意一组参数可以确定一条安全组规则，只指定一个参数无法确定一条安全组规则。如果匹配的安全组规则已存在，此次 `AuthorizeSecurityGroup` 调用失败。

    -   设置指定 IP 地址段的访问权限，如 [请求示例一](#Sample1)：`IpProtocol`、`PortRange`、（可选）`SourcePortRange`、`NicType`、`Policy`、（可选）`DestCiderIp` 和 `SourceCidrIp`

    -   设置其他安全组的访问权限，如 [请求示例二](#Sample2) ：`IpProtocol`、`PortRange`、（可选）`SourcePortRange`、`NicType`、`Policy`、（可选）`DestCiderIp`、`SourceGroupOwnerAccount`和 `SourceGroupId`


## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：AuthorizeSecurityGroup|
|RegionId|String|是|安全组所属地域 ID。您可以调用 [DescribeRegions](cn.zh-CN/API 参考/地域/DescribeRegions.md#) 查看最新的阿里云地域列表。|
|SecurityGroupId|String|是|目的端安全组 ID。|
|IpProtocol|String|是|传输层协议。取值大小写敏感。取值范围：-   tcp
-   udp
-   icmp
-   gre
-   all：支持所有协议

|
|PortRange|String|是|`SecurityGroupId` 方开放的传输层协议相关的端口范围。取值范围：-   TCP/UDP 协议：取值范围为 \[1, 65535\] 。使用斜线（/）隔开起始端口和终止端口。正确示范：`1/200`；错误示范：`200/1`。
-   ICMP 协议：-1/-1
-   GRE 协议：-1/-1
-   `IpProtocol` 取值为 `all`：-1/-1

|
|SourcePortRange|String|否|源端安全组开放的传输层协议相关的端口范围。取值范围：-   TCP/UDP 协议：取值范围为 \[1, 65535\] 。使用斜线（/）隔开起始端口和终止端口。正确示范：`1/200`；错误示范：`200/1`。
-   ICMP 协议：-1/-1。
-   GRE 协议：-1/-1。
-    `IpProtocol` 取值为 `all`：-1/-1。

|
|NicType|String|否|网卡类型。取值范围：-   internet：公网网卡。
-   intranet：内网网卡。

当设置安全组之间互相访问时，即指定了 `SourceGroupId` 且没有指定 `SourceCidrIp` 时，参数 `NicType` 取值只能为 `intranet`。 默认值：internet|
|Policy|String|否|设置访问权限。取值范围：-   accept：接受访问。
-   drop：拒绝访问，不发回拒绝信息。

默认值：accept|
|DestCidrIp|String|否|目的端 IP 地址范围。支持 CIDR 格式和 IPv4 格式的 IP 地址范围。默认值：0.0.0.0/0

|
|SourceCidrIp|String|否|源端 IP 地址范围。支持 CIDR 格式和 IPv4 格式的 IP 地址范围。默认值：0.0.0.0/0

|
|SourceGroupId|String|否|需要设置访问权限的源端安全组 ID。至少设置一项 `SourceGroupId` 或者 `SourceCidrIp` 参数。如果指定了 `SourceGroupId` 没有指定参数 `SourceCidrIp`，则参数 `NicType` 取值只能为 `intranet`。

如果同时指定了 `SourceGroupId` 和 `SourceCidrIp`，则默认以 `SourceCidrIp` 为准。

|
|SourceGroupOwnerAccount|String|否|跨账户设置安全组规则时，源端安全组所属的阿里云账户。-   如果 `SourceGroupOwnerAccount` 及 `SourceGroupOwnerID` 均未设置，则认为是设置您其他安全组的访问权限。
-   如果已经设置参数 `SourceCidrIp`，则参数 `SourceGroupOwnerAccount` 无效。

|
|SourceGroupOwnerId|String|否|跨账户设置安全组规则时，源端安全组所属的阿里云账户 ID。-   如果 `SourceGroupOwnerId` 及 `SourceGroupOwnerAccount` 均未设置，则认为是设置您其他安全组的访问权限。
-   如果您已经设置参数 `SourceCidrIp`，则参数 `SourceGroupOwnerId` 无效。

|
|Priority|String|否|安全组规则优先级。取值范围：\[1, 100\] 默认值：1

|
|Description|String|否|安全组规则的描述信息。长度为 \[1, 512\] 个字符。|

## 返回参数 {#section_px3_2g1_ydb .section}

全是公共返回参数。参阅 [公共返回参数](cn.zh-CN/API 参考/快速入门/公共参数.md#commonResponseParameters)。

## 示例 { .section}

更多关于安全组规则的设置示例，请参阅 [应用案例](../cn.zh-CN/用户指南/安全组/应用案例.md#)、[安全组规则的典型应用](../cn.zh-CN/用户指南/安全组/安全组规则的典型应用.md#) 和 [安全组五元组规则介绍](https://yq.aliyun.com/articles/272107)。

**请求示例一** 

设置指定 IP 地址段的访问权限。此时，经典网络类型安全组的网卡类型（`NicType`）可设置公网（`internet`）和 [内网](../cn.zh-CN/产品简介/网络和安全性/内网.md#)（`intranet`）。VPC 类型安全组的网卡类型（`NicType`）只可设置内网（`intranet`）。

```
https://ecs.aliyuncs.com/?Action=AuthorizeSecurityGroup
&SecurityGroupId=sg-F876FF7BA
&SourceCidrIp=0.0.0.0/0
&IpProtocol=tcp
&PortRange=1/65535
&NicType=intranet
&Policy=accept
&<公共请求参数>
```

 **请求示例二** 

设置其他安全组的访问权限。此时，网卡类型（`NicType`）只能为内网（`intranet`）。经典网络类型安全组之间互访时，可以设置同一地域中其他安全组对您的安全组的访问权限。这个安全组可以是您的也可以是其他阿里云账户（`SourceGroupOwnerAccount`）的。VPC 类型安全组之间互访时，可以设置同一 VPC 内其他安全组访问该安全组的访问权限。

```
https://ecs.aliyuncs.com/?Action=AuthorizeSecurityGroup
&SecurityGroupId=sg-F876FF7BA
&SourceGroupId=sg-1651FBB64
&SourceGroupOwnerAccount=test@aliyun.com
&IpProtocol=tcp
&PortRange=1/65535
&NicType=intranet
&Policy=drop
&<公共请求参数>
```

**返回示例** 

**XML 格式**

```
<AuthorizeSecurityGroupResponse>
    <RequestId>CEF72CEB-54B6-4AE8-B225-F876FF7BA984</RequestId>
</AuthorizeSecurityGroupResponse>
```

**JSON 格式** 

```
{
    "RequestId":"CEF72CEB-54B6-4AE8-B225-F876FF7BA984"
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问 [API 错误中心](https://error-center.aliyun.com/status/product/Ecs)。

|错误代码|错误信息|HTTP 状态码|说明|
|:---|:---|:-------|:-|
|InvalidIpProtocol.Malformed|The specified parameter “PortRange” is not valid.|400|指定的参数 `IpProtocol` 不合法。|
|InvalidPriority.Malformed|The specified parameter “Priority” is not valid.|400|指定的参数 `Priority` 不合法。|
|InvalidSourceCidrIp.Malformed|The specified parameter “SourceCidrIp” is not valid.|400|指定的参数 `SourceCidrIp` 不合法。|
|InvalidDestCidrIp.Malformed|The specified parameter “DestCidrIp” is not valid.|400|指定的参数 `DestCidrIp` 不合法。|
|InvalidPolicy.Malformed|The specified parameter “Policy” is not valid.|400|指定的参数 `Policy`不合法。|
|InvalidNicType.ValueNotSupported|The specified NicType does not exist.|400|指定的参数 `NicType`不存在。|
|InvalidSourceGroupId.Mismatch|Specified security group and source group are not in the same VPC.|400|指定的安全组的网络类型是 VPC，源端安全组必须在同一个 VPC 里。|
|InvalidNicType.Mismatch|Specified nic type conflicts with the authorization record.|400|指定网卡类型 `NicType` 与安全组规则不符合。|
|InvalidSourceGroup.NotFound|The specified SourceGroupId does not exist.|400|指定的源端安全组 `SourceGroupId` 不存在。|
|InvalidPriority.ValueNotSupported|The specified Priority is invalid.|400|指定的参数 `Priority` 不合法。|
|InvalidSecurityGroupDiscription.Malformed|The specified security group rule description is not valid.|400|安全组规则的描述 `Description` 不合法。|
|OperationDenied|The specified IpProtocol does not exist or IpProtocol and PortRange do not match.|400|指定的参数 `IpProtocol` 不存在。或者指定的 IP 协议和端口范围不匹配。|
|AuthorizationLimitExceed|The maximum number of authorization rules in the security group is exceeded.|403|单个安全组的安全组规则最多为 100 条。|
|InvalidSourceGroupId.Mismatch|NicType is required or NicType expects intranet.|403|需要明确 `NicType` 参数。或者 `NicType` 必须为 `intranet`。|
|InvalidNetworkType.Mismatch|The specified SecurityGroup network type should be same with SourceGroup network type \(vpc or classic\).|403|安全组规则中的两个安全组网络类型必须相同，即必须同时为经典网络或者 VPC。|
|InvalidParamter.Conflict|The specified SecurityGroupId should be different from the SourceGroupId.|403|参数 `SecurityGroupId`和 `SourceGroupId`不能相同。|
|MissingParameter|The input parameter “SourceGroupId” or “SourceCidrIp” cannot be both blank.|403|需要指定参数 `SourceGroupId` 或者 `SourceCidrIp`。|
|InvalidSourceGroupId.NotFound|The SourceGroupId provided does not exist in our records.|404|指定的 `SourceGroup`不存在。|
|InvalidSecurityGroupId.NotFound|The specified SecurityGroupId does not exist.|404|指定的 `SecurityGroupId`不存在。|
|InvalidRegionId.NotFound|The specified RegionId does not exist.|404|指定的 `RegionId` 不存在。|

