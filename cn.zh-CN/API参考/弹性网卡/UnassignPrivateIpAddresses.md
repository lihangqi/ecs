# UnassignPrivateIpAddresses {#doc_api_Ecs_UnassignPrivateIpAddresses .reference}

从一块弹性网卡删除一个或多个辅助私有IP地址。

## 接口说明 {#description .section}

-   只支持可用（Available）或者已绑定（InUse）状态下的弹性网卡。
-   操作主网卡时，网卡附加的实例必须处于运行中（Running）或者已停止（Stopped）状态。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=UnassignPrivateIpAddresses)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|NetworkInterfaceId|String|是|eni-myeni|弹性网卡ID。

 |
|PrivateIpAddress.N|RepeatList|是|192.168.0.1|一个或多个需要删除的辅助私有IP地址。N 的取值范围：

 -   弹性网卡处于可用（Available）状态：1~10
-   弹性网卡处于已绑定（InUse）状态：受到实例规格限制

 |
|RegionId|String|是|cn-hangzhou|资源所属地域。您可以调用 [DescribeRegions](~~25609~~) 查看最新的阿里云地域列表。

 |
|Action|String|否|UnassignPrivateIpAddresses|系统规定参数。取值：UnassignPrivateIpAddresses

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=UnassignPrivateIpAddresses
&NetworkInterfaceId=eni-myeni
&PrivateIpAddress.1=192.168.0.1
&RegionId=cn-hangzhou
&<公共请求参数>
```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<UnassignPrivateIpAddressesResponse>
  <RequestId>04F0F334-1335-436C-A1D7-6C044FE70008</RequestId>
</UnassignPrivateIpAddressesResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"04F0F334-1335-436C-A1D7-6C044FE70008"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|403|InvalidUserType.NotSupported|%s|此操作暂不支持您的账号类型。|
|403|Abs.InvalidAccount.NotFound|%s|您的阿里云账号不存在，或者您的AccessKey已经过期。|
|403|MissingParameter|%s|缺失必需参数。|
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
|404|InvalidInstanceId.NotFound|%s|指定的实例不存在。|
|403|InvalidVSwitchId.IpInvalid|%s|指定的私网ip不合法。|
|403|InvalidIp.IpUnassigned|%s|指定的 IP 未被分配。|
|403|Operation.Conflict|%s|操作发生冲突，请重试。|
|400|Forbidden.RegionId|%s|前区域暂不支持此功能。|
|400|InvalidAction|%s|操作不合法。|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Ecs)

