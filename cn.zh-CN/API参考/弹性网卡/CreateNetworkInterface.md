# CreateNetworkInterface {#doc_api_Ecs_CreateNetworkInterface .reference}

创建一个弹性网卡（ENI）。

## 接口说明 {#description .section}

-   新创建的弹性网卡处于可用（Available）状态。
-   弹性网卡只支持附加到同一可用区的VPC类型实例。
-   一个弹性网卡只能附加到一台实例，附加到新实例之前您需要将其与当前实例分离。
-   弹性网卡重新附加到另一台实例时，其属性不变，网络流量也会重定向到新的实例。
-   一个账号在一个阿里云地域内默认最多可创建100个弹性网卡。如果需要更多，请 [提交工单](https://selfservice.console.aliyun.com/ticket/createIndex.htm) 申请。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=CreateNetworkInterface)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|RegionId|String|是|cn-hangzhou|实例所在地域的ID。您可以调用 [DescribeRegions](~~25609~~) 查看最新的阿里云地域列表。

 |
|SecurityGroupId|String|是|sg-c0003exxxxx|所属的安全组ID必须是同一个VPC下的安全组。

 |
|VSwitchId|String|是|\[vswitchid\]|指定VPC的交换机ID。

 |
|Action|String|否|CreateNetworkInterface|系统规定参数。取值：CreateNetworkInterface

 |
|ClientToken|String|否|123e4567-e89b-12d3-a456-426655440000|保证请求幂等性。从您的客户端生成一个参数值，确保不同请求间该参数值唯一。只支持ASCII字符，且不能超过64个字符。更多详情，请参阅 [如何保证幂等性](~~25693~~)。

 |
|Description|String|否|test|弹性网卡的描述信息。长度为2~256个英文或中文字符，不能以 http:// 和 https:// 开头。

 默认值：空。

 |
|NetworkInterfaceName|String|否|eni-eniname1|弹性网卡名称。长度为2~128个英文或中文字符。必须以大小字母或中文开头，不能以 http:// 和 https:// 开头。可以包含数字、半角冒号（:）、下划线（\_）或者连字符（-）。

 默认值：空。

 |
|PrimaryIpAddress|String|否|172.17.XX.XXX|弹性网卡的主私有IP地址。指定IP必须是在所属交换机的地址段内的空闲地址，不指定则默认随机分配该交换机中的空闲地址。

 |
|ResourceGroupId|String|否|rg-resourcegroupid1|资源组ID。

 |
|Tag.N.Key|String|否|test|弹性网卡的标签键。n 的取值范围：1~20。一旦传入该值，则不允许为空字符串。最多支持 64 个字符，不能以 aliyun 和 acs: 开头，不能包含 http:// 或者 https:// 。

 |
|Tag.N.Value|String|否|api|弹性网卡的标签值。n的取值范围：1~20。一旦传入该值，可以为空字符串。最多支持 128 个字符，不能以 aliyun 和 acs: 开头，不能包含 http:// 或者 https:// 。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|NetworkInterfaceId|String|eni-eniIxxxxx|弹性网卡ID。

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=CreateNetworkInterface
&RegionId=cn-hangzhou
&SecurityGroupId=sg-c0003exxxxx
&VSwitchId=[vswitchid]
&Tag.1.Key=test
&Tag.1.Value=api
&ResourceGroupId=rg-resourcegroupid1
&PrimaryIpAddress=172.17.XX.XXX
&NetworkInterfaceName=eni-eniname1
&Description=test
&ClientToken=xxxxx
&<公共请求参数>
```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<CreateNetworkInterfaceResponse>
  <RequestId>04F0F334-1335-436C-A1D7-6C044FExxxxx</RequestId>
  <NetworkInterfaceId>eni-eniIxxxxx</NetworkInterfaceId>
</CreateNetworkInterfaceResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"04F0F334-1335-436C-A1D7-6C044FExxxxx",
	"NetworkInterfaceId":"eni-enixxxxx"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|403|InvalidUserType.NotSupported|%s|此操作暂不支持您的账号类型。|
|403|Abs.InvalidAccount.NotFound|%s|您的阿里云账号不存在，或者您的AccessKey已经过期。|
|400|MissingParameter|%s|缺失必需参数。|
|403|Forbidden.NotSupportRAM|%s|暂不支持 RAM 用户执行该操作。|
|400|UnsupportedParameter|%s|不支持参数。|
|403|Forbidden.SubUser|%s|子账号没有授权操作此资源。|
|400|InvalidParameter|%s|参数格式不正确。|
|400|InvalidInstanceID.Malformed|%s|实例 ID 格式不正确。|
|400|InvalidOperation.InvalidEcsState|%s|ECS 实例当前状态不支持释放私网 IP。|
|400|InvalidOperation.InvalidEniState|%s|弹性网卡当前状态不支持释放私网 IP。|
|400|InvalidOperation.DetachPrimaryEniNotAllowed|%s|不允许分离主网卡。|
|404|InvalidEcsId.NotFound|%s|指定的实例ID不存在。|
|404|InvalidEniId.NotFound|%s|指定的网卡ID不存在。|
|404|InvalidVSwitchId.NotFound|%s|指定的交换机ID。|
|404|InvalidSecurityGroupId.NotFound|%s|指定的安全组ID不存在。|
|403|EniPerInstanceLimitExceeded|%s|弹性网卡的数量超过了指定实例类型允许的最大值。|
|403|InvalidOperation.AvailabilityZoneMismatch|%s|指定的VPC交换机ID、弹性网卡和实例ID不在同一个可用区。|
|403|InvalidOperation.VpcMismatch|%s|指定的弹性网卡和安全组ID不在同一个 VPC。|
|403|SecurityGroupInstanceLimitExceed|%s|该安全组内已有的实例数量已超出最大限制。|
|403|InvalidSecurityGroupId.NotVpc|%s|指定的安全组 ID 不是 VPC 类型。|
|403|InvalidOperation.InvalidEniType|%s|当前弹性网卡类型不支持该操作。|
|403|InvalidVSwitchId.IpNotEnough|%s|指定的交换机内ip数量不足。|
|403|InvalidVSwitchId.IpInvalid|%s|指定的私网ip不合法。|
|400|Forbidden.RegionId|%s|前区域暂不支持此功能。|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Ecs)

