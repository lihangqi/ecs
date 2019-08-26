# AssignIpv6Addresses {#doc_api_Ecs_AssignIpv6Addresses .reference}

使用 AssignIpv6Addresses 为弹性网卡分配一个或多个 IPv6 地址。

## 描述 {#description .section}

IPv6 地址目前处于公测阶段，您可以提交 [公测申请](https://page.aliyun.com/form/act608662110/index.htm)。

您可以指定弹性网卡所属交换机下 CIDR 的 IPv6 地址，也可以指定IPv6地址数量自动创建 IPv6 地址。

-   弹性网卡必须处于**可用**（Available）或**已挂载**（InUse）状态。
-   主网卡关联的 ECS 实例必须处于**运行中**（Running）或**已停止**（Stopped）状态。
-   单个网卡能够分配的 IPv6 地址数量和网卡附加的实例规格有关。
    -   如果弹性网卡处于**可用**（Available）状态，最多可以分配 10 个 IPv6 地址。
    -   如果弹性网卡挂载到实例上，能够分配的 IPv6 地址数将受到实例规格限制。更多详情，请参阅 [实例规格族](~~25378~~)。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=AssignIpv6Addresses)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|NetworkInterfaceId|String|是|eni-test|弹性网卡 ID。

 |
|RegionId|String|是|cn-hangzhou|弹性网卡所在地域的 ID。您可以调用 [DescribeRegions](~~25609~~) 查看最新的阿里云地域列表。

 |
|Action|String|否|AssignIpv6Addresses|系统规定参数。取值：AssignIpv6Addresses

 |
|Ipv6Address.N|RepeatList|否|2001:db8:1234:1a00::XXX|为弹性网卡指定一个或多个 IPv6 地址。目前，N 的取值范围仅支持 1。

 取值示例：Ipv6Address.1=2001:db8:1234:1a00::XXX

 **说明：** 您不能同时指定参数 Ipv6Addresses.N 和 Ipv6AddressCount。

 |
|Ipv6AddressCount|Integer|否|1|为弹性网卡指定随机生成的 IPv6 地址数量。

 **说明：** 您不能同时指定参数 Ipv6Addresses.N 和 Ipv6AddressCount。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=AssignIpv6Addresses
&NetworkInterfaceId=eni-test
&RegionId=cn-hangzhou
&Ipv6Address.1=2001:db8:1234:1a00::XXX
&Ipv6AddressCount=1
&<公共请求参数>
```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<AssignIpv6AddressesResponse>
  <RequestId>A94E0C9F-B39E-4A87-BFFC-6DC7840xxxxx</RequestId>
</AssignIpv6AddressesResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"A94E0C9F-B39E-4A87-BFFC-6DC7840xxxxx"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|403|InvalidUserType.NotSupported|%s|此操作暂不支持您的账号类型。|
|403|Abs.InvalidAccount.NotFound|%s|您的阿里云账号不存在，或者您的AccessKey已经过期。|
|403|MissingParameter|%s|缺失必需参数。|
|403|Forbedden.NotSupportRAM|%s|暂不支持 RAM 用户执行该操作。|
|400|UnsupportedParameter|%s|不支持参数。|
|403|Forbbiden.SubUser|%s|暂不支持 RAM 用户执行该操作。|
|400|InvalidParameter|%s|参数格式不正确。|
|400|InvalidInstanceID.Malformed|%s|实例 ID 格式不正确。|
|400|InvalidOperation.InvalidEcsState|%s|ECS 实例当前状态不支持释放私网 IP。|
|400|InvalidOperation.InvalidEniState|%s|弹性网卡当前状态不支持释放私网 IP。|
|404|InvalidEniId.NotFound|%s|指定的网卡ID不存在。|
|403|InvalidOperation.InvalidEniType|%s|当前弹性网卡类型不支持该操作。|
|403|MaxEniIpv6IpsCountExceeded|%s|弹性网卡挂载 IPv6 个数达到上限。|
|403|InvalidIp.IpUnassigned|%s|指定的 IP 未被分配。|
|403|InvalidIp.IpRepeated|%s|指定的 IP 重复。|
|403|InvalidIp.IpAssigned|%s|指定的 IP 已被分配。|
|403|InvalidIp.Address|%s|指定的 IPv6 地址不合法。|
|403|InvalidOperation.Ipv4CountExceeded|%s|IPv4 个数达到上限。|
|403|InvalidOperation.Ipv6CountExceeded|%s|IPv6 个数达到上限。|
|403|InvalidOperation.Ipv6NotSupport|%s|实例规格不支持 IPv6。|
|403|InvalidVSwitch.Ipv6NotTurnOn|%s|交换机未开启 IPv6 功能。|
|403|InvalidVSwitchId.IpInvalid|%s|指定的私网ip不合法。|
|403|Forbidden.RegionId|%s|前区域暂不支持此功能。|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Ecs)

