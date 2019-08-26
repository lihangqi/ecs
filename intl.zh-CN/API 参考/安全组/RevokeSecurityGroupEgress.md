# RevokeSecurityGroupEgress {#RevokeSecurityGroupEgress .reference}

删除一条安全组出方向规则，撤销安全组出方向的访问权限。

## 描述 {#section_nc5_pq1_ydb .section}

我们定义出方向流量的发起端为源端（Source），数据传输的接收端为目的端（Destination）。更多详情，请参阅 [AuthorizeSecurityGroupEgress](intl.zh-CN/API参考/安全组/AuthorizeSecurityGroupEgress.md#)。

以下任意一组参数可以确定一条安全组出方向规则，只指定一个参数无法确定一条安全组规则。

-   撤销对指定 IP 地址段的访问权限，如 [请求示例一](#Sample1) ：`IpProtocol`、`PortRange`、（可选）`SourcePortRange`、`NicType`、`Policy`、`DestCiderIp` 和 （可选）`SourceCidrIp`

-   撤销对其他安全组的访问权限，如 [请求示例二](#Sample2)：`IpProtocol`、`PortRange`、（可选）`SourcePortRange`、`NicType`、`Policy`、（可选）`DestCiderIp`、`DestGroupOwnerAccount` 和 `DestGroupId`


## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：RevokeSecurityGroupEgress|
|RegionId|String|是|源端安全组所属地域 ID。您可以调用 [DescribeRegions](intl.zh-CN/API参考/地域/DescribeRegions.md#) 查看最新的阿里云地域列表。|
|SecurityGroupId|String|是|源端安全组 ID。|
|IpProtocol|String|是|传输层协议。不区分大小写。取值范围：-   icmp
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

当撤销安全组之间互相访问时，即指定了 `DestGroupId` 且没有指定 `DestCidrIp` 时，参数 `NicType` 取值只能为 `intranet`。 默认值：internet|
|Policy|String|否|访问权限。取值范围：-   accept：接受访问。
-   drop：拒绝访问，不发回拒绝信息。

默认值：accept|
|DestCidrIp|String|否|目的端 IP 地址范围。支持 CIDR 格式和 IPv4 格式的 IP 地址范围。默认值：0.0.0.0/0|
|SourceCidrIp|String|否|源端 IP 地址范围。支持 CIDR 格式和 IPv4 格式的 IP 地址范围。默认值：0.0.0.0/0|
|DestGroupId|String|否|需要撤销访问权限的目的端安全组 ID。必须设置 `DestGroupId` 或者 `DestCidrIp` 参数。如果指定了 `DestGroupId` 没有指定参数 `DestCidrIp`，则参数 `NicType` 取值只能为 `intranet`。如果同时指定了 `DestGroupId` 和 `DestCidrIp`，则默认以 `DestCidrIp` 为准。|
|DestGroupOwnerAccount|String|否|跨账户删除安全组规则时，目的端安全组所属的阿里云账户。-   如果 `DestGroupOwnerAccount` 及 `DestGroupOwnerId` 均未设置，则认为是撤销您其他安全组的访问权限。
-   如果已经设置参数 `DestCidrIp`，则参数 `DestGroupOwnerAccount` 无效。

|
|DestGroupOwnerId|String|否|跨账户删除安全组规则时，目的端安全组所属的阿里云账户 ID。-   如果 `DestGroupOwnerId` 及 `DestGroupOwnerAccount` 均未设置，则认为是撤销您其他安全组的访问权限。
-   如果您已经设置参数 `DestCidrIp`，则参数 `DestGroupOwnerId` 无效。

|
|Priority|String|否|安全组规则优先级。取值范围：\[1, 100\] 默认值：1

|

## 返回参数 {#section_f54_lk5_xdb .section}

全是公共返回参数。参阅 [公共参数](intl.zh-CN/API参考/调用方式/公共参数.md#commonResponseParameters)。

## 示例 { .section}

**请求示例一** 

撤销对指定 IP 地址段的访问权限。

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

**请求示例二**

撤销对其他安全组的访问权限。

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

**返回示例** 

**XML 格式**

```
<RevokeSecurityGroupEgressResponse>
     <RequestId>CEF72CEB-54B6-4AE8-B225-F876FF7BA984</RequestId>
</RevokeSecurityGroupEgressResponse>
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
|InvalidDestCidrIp.Malformed|The specified parameter “DestCidrIp” is not valid.|400|指定的 `DestCidrIp`不合法。|
|InvalidDestCidrIp.sMalformed|The specified parameter “DestCidrIp” is not valid.|400|指定的 `DestCidrIp`不合法。|
|InvalidDestGroupId.Mismatch|Specified security group and destination group are not in the same VPC.|400|指定安全组的网络类型是 VPC，目的端安全组必须在同一个 VPC 里。|
|InvalidIpPortRange.Malformed|The specified parameter “PortRange” is not valid.|400|指定的 `PortRange` 不合法。|
|InvalidIpProtocol.ValueNotSupported|The specified IpProtocol does not exist.|400|指定的 `IpProtocol`不存在。|
|InvalidNicType.ValueNotSupported|The specified NicType does not exist.|400|指定的 `NicType` 不存在。|
|InvalidPolicy.Malformed|The specified parameter “Policy” is not valid.|400|指定的 `Policy` 不合法。|
|MissingParameter|The input parameter “DestGroupId” or “DestCidrIp” cannot be both blank.|400|必须指定参数 `DestGroupId` 或者 `DestCidrIp`。|
|InvalidGroupAuthItem.NotFound|Specified group authorized item does not exist in our records.|403|指定的安全组规则不存在。|
|InvalidNicType.Mismatch|Specified nic type conflicts with the authorization record.|403|两方安全组的网络类型必须相同，即必须同时为经典网络或者 VPC。|
|InvalidSecurityGroup.IsSame|The authorized SecurityGroupId should be different from the DestGroupId.|403|参数 `SecurityGroupId` 和 `DestGroupId` 不能相同。|
|InvalidDestGroupId.NotFound|The DestGroupId provided does not exist in our records.|404|指定的 `DestGroupId`不存在。|
|InvalidRegionId.NotFound|The specified RegionId does not exist.|404|指定的 `RegionId` 不存在。|
|InvalidSecurityGroupId.NotFound|The specified SecurityGroupId does not exist.|404|指定的 `SecurityGroupId` 不存在。|

