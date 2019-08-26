# UnassignIpv6Addresses {#doc_api_Ecs_UnassignIpv6Addresses .reference}

若弹性网卡已被分配了IPv6地址，调用UnassignIpv6Addresses可以回收一个或多个IPv6地址。

## 接口说明 {#description .section}

IPv6 地址目前处于公测阶段，您可以提交 [公测申请](https://page.aliyun.com/form/act608662110/index.htm)。

调用该接口时，您需要注意：

-   弹性网卡必须处于**可用**（Available）或**已挂载**（InUse）状态。
-   主网卡关联的 ECS 实例必须处于**运行中**（Running）或**已停止**（Stopped）状态。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=UnassignIpv6Addresses&type=RPC&version=2014-05-26)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Ipv6Address.N|RepeatList|是|2001:db8:1234:1a00::XXX|为弹性网卡指定一个或多个 IPv6 地址。目前，N 的取值范围仅支持 1。

 取值示例：Ipv6Address.1=2001:db8:1234:1a00::XXX

 **说明：** 您不能同时指定参数 Ipv6Addresses.N 和 Ipv6AddressCount。

 |
|NetworkInterfaceId|String|是|eni-test|弹性网卡 ID。

 |
|RegionId|String|是|cn-hangzhou|弹性网卡所在地域的 ID。您可以调用 [DescribeRegions](~~25609~~) 查看最新的阿里云地域列表。

 |
|Action|String|否|UnassignIpv6Addresses|系统规定参数。取值：UnassignIpv6Addresses。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=UnassignIpv6Addresses
&Ipv6Address.1=2001:db8:1234:1a00::***
&NetworkInterfaceId=eni-test
&RegionId=cn-hangzhou
&<公共请求参数>
```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<UnassignIpv6AddressesResponse>
      <RequestId>48285314-3192-47FE-B4C8-9D51E7Fxxxxx</RequestId>
</UnassignIpv6AddressesResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"48285314-3192-47FE-B4C8-9D51E7Fxxxxx"
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
|403|InvalidIp.IpUnassigned|%s|指定的 IP 未被分配。|
|403|InvalidIp.IpRepeated|%s|指定的 IP 重复。|
|403|InvalidIp.Address|%s|指定的 IPv6 地址不合法。|
|403|Forbidden.RegionId|%s|前区域暂不支持此功能。|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

