# RevokeSecurityGroup {#RevokeSecurityGroup .reference}

删除一条安全组入方向规则,撤销安全组出方向的权限设置。

## 描述 {#section_xwx_cp1_ydb .section}

我们定义出方向流量的发起端为源端（Source），数据传输的接收端为目的端（Destination）。更多详情，请参阅 [AuthorizeSecurityGroupEgress](intl.zh-CN/API参考/安全组/AuthorizeSecurityGroupEgress.md#)。

以下任意一组参数可以确定一条安全组入方向规则，只指定一个参数无法确定一条安全组规则。

-   撤销指定 IP 地址段的权限设置：`IpProtocol`、`PortRange`、（可选）`SourcePortRange`、`NicType`、`Policy`、`DestCiderIp` 和 （可选）`SourceCidrIp`

-   撤销其他安全组的权限设置：`IpProtocol`、`PortRange`、（可选）`SourcePortRange`、`NicType`、`Policy`、（可选）`DestCiderIp`、`DestGroupOwnerAccount` 和 `DestGroupId`


## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：RevokeSecurityGroup|
|RegionId|String|是|目的端安全组所属地域 ID。您可以调用 [DescribeRegions](intl.zh-CN/API参考/地域/DescribeRegions.md#) 查看最新的阿里云地域列表。|
|SecurityGroupId|String|是|目的端安全组 ID。|
|IpProtocol|String|是|传输层协议。参数值大小写敏感。取值范围：-   icmp
-   gre
-   tcp
-   udp
-   all：支持所有协议

|
|PortRange|String|是|目的端安全组开放的传输层协议相关的端口范围。取值范围：-   TCP/UDP 协议：取值范围为 \[1, 65535\] 。使用斜线（/）隔开起始端口和终止端口。正确示范：`1/200`；错误示范：`200/1`。
-   ICMP 协议：-1/-1。
-   GRE 协议：-1/-1。
-   all：-1/-1。

|
|SourcePortRange|String|否|源端安全组开放的传输层协议相关的端口范围。取值范围：-   TCP/UDP 协议：取值范围为 \[1, 65535\] 。使用斜线（/）隔开起始端口和终止端口。正确示范：`1/200`；错误示范：`200/1`。
-   ICMP 协议：-1/-1。
-   GRE 协议：-1/-1。
-   all：-1/-1。

|
|NicType|String|否|网卡类型。取值范围：-   internet：公网网卡。
-   intranet：内网网卡。

当撤销安全组之间互相访问时，即指定了 `SourceGroupId` 且没有指定 `SourceCidrIp` 时，参数 `NicType` 取值只能为 `intranet`。 默认值：internet|
|Policy|String|否|访问权限。取值范围：-   accept：接受访问。
-   drop：拒绝访问，不发回拒绝信息。

默认值：accept|
|DestCidrIp|String|否|目的端 IP 地址范围。支持 CIDR 格式和 IPv4 格式的 IP 地址范围。默认值：0.0.0.0/0|
|SourceCidrIp|String|否|源端 IP 地址范围。支持 CIDR 格式和 IPv4 格式的 IP 地址范围。默认值：0.0.0.0/0|
|SourceGroupId|String|否|需要撤销访问权限的源端安全组 ID。必须设置 `SourceGroupId` 或者 `SourceCidrIp` 参数。如果指定了 `SourceGroupId` 没有指定参数 `SourceCidrIp`，则参数 `NicType` 取值只能为 `intranet`。如果同时指定了 `SourceGroupId` 和 `SourceCidrIp`，则默认以 `SourceCidrIp` 为准。|
|SourceGroupOwnerAccount|String|否|跨账户删除安全组规则时，源端安全组所属的阿里云账户。-   如果 `SourceGroupOwnerAccount` 及 `SourceGroupOwnerId` 均未设置，则认为是撤销您其他安全组的访问权限。
-   如果已经设置参数 `SourceCidrIp`，则参数 `SourceGroupOwnerAccount` 无效。

|
|SourceGroupOwnerId|String|否|跨账户删除安全组规则时，源端安全组所属的阿里云账户 ID。-   如果 `SourceGroupOwnerId` 及 `SourceGroupOwnerAccount` 均未设置，则认为是撤销您其他安全组的访问权限。
-   如果您已经设置参数 `SourceCidrIp`，则参数 `SourceGroupOwnerId` 无效。

|
|Priority|String|否|安全组规则优先级。取值范围：\[1, 100\] 默认值：1

|

## 返回参数 {#section_vxx_cp1_ydb .section}

全是公共返回参数。参阅 [公共参数](intl.zh-CN/API参考/调用方式/公共参数.md#commonResponseParameters)。

## 示例 { .section}

**请求示例**

```
https://ecs.aliyuncs.com/?Action=RevokeSecurityGroup
&SecurityGroupId=C0003E8B-B930-4F59-ADC0-0E209A9012B0
&SourceGroupId=sg-F876FF7BA
&SourceGroupOwnerAccount=test@aliyun.com
&IpProtocol=tcp
&PortRange=1/65535
&Priority=1
&<公共请求参数>
```

**返回示例** 

**XML 格式**

```
<RevokeSecurityGroupResponse>
     <RequestId>CEF72CEB-54B6-4AE8-B225-F876FF7BA984</RequestId>
</RevokeSecurityGroupResponse>
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
|InvalidIpPortRange.Malformed|The specified parameter “PortRange” is not valid.|400|指定的 `PortRange` 不合法。|
|InvalidIpProtocol.ValueNotSupported|The specified IpProtocol does not exist.|400|指定的 `IpProtocol`不存在。|
|InvalidNicType.ValueNotSupported|The specified NicType does not exist.|400|指定的 `NicType` 不存在。|
|InvalidPolicy.Malformed|The specified parameter “Policy” is not valid.|400|指定的 `Policy` 不合法。|
|InvalidSourceCidrIp.Malformed|The specified parameter “SourceCidrIp” is not valid.|400|指定的 `SourceCidrIp`不合法。|
|InvalidSourceGroupId.Mismatch|Specified security group and source group are not in the same VPC.|400|指定安全组的网络类型是 VPC，目的端安全组必须在同一个 VPC 里。|
|MissingParameter|The input parameter “SourceGroupId” or “SourceCidrIp” cannot be both blank.|400|必须指定参数 `SourceGroupId` 或者 `SourceCidrIp`。|
|InvalidGroupAuthItem.NotFound|Specified group authorized item does not exist in our records.|403|指定的安全组规则不存在。|
|InvalidNicType.Mismatch|Specified nic type conflicts with the authorization record.|403|指定的 `NicType` 与安全组规则不符合。|
|InvalidRegionId.NotFound|The specified RegionId does not exist.|404|指定的 `RegionId` 不存在。|
|InvalidSecurityGroupId.NotFound|The specified SecurityGroupId does not exist.|404|指定的 `SecurityGroupId` 不存在。|
|InvalidSourceGroupId.NotFound|The SourceGroupId provided does not exist in our records.|404|指定的 `SourceGroupId` 不存在。|

