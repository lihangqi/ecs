# AllocatePublicIpAddress {#doc_api_999740 .reference}

为一台实例分配一个公网 IP 地址。

## 描述 {#description .section}

调用该接口时，您需要注意：

-   分配公网 IP 地址之前，实例必须处于运行中（Running）或者已停止（Stopped）状态。
-   当VPC类型实例已经绑定了 EIP，则无法再分配公网 IP。
-   一台实例只能分配一个公网 IP 地址。如果实例已经拥有一个公网 IP 地址，将报错 AllocatedAlready。
-   重启实例（[RebootInstance](~~25502~~)）或者启动实例（[StartInstance](~~25500~~)）后，新的公网 IP 地址生效。
-   被 [安全控制](~~25695~~) 的实例的 OperationLocks 中标记了 "LockReason" : "security" 时，不能分配公网 IP 地址。

除分配公网 IP 之外，您还可以给实例绑定弹性公网 IP（EIP）。更多详情，请参阅 [AssociateEipAddress](~~36017~~)。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=AllocatePublicIpAddress)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|InstanceId|String|是|i-instance1|需要分配 IP 地址的实例 ID。

 |
|Action|String|否|AllocatePublicIpAddress|系统规定参数。取值：AllocatePublicIpAddress

 |
|IpAddress|String|否|10.1.149.159|实例的公网 IP 地址。

 |
|OwnerAccount|String|否|ECSforCloud@Alibaba.com|RAM 用户的账号登录名称。

 |
|VlanId|String|否|100|VLAN ID。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|IpAddress|String|10.1.149.159|实例的公网 IP 地址

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。无论调用接口成功与否，我们都会返回请求 ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

https://ecs.aliyuncs.com/?Action=AllocatePublicIpAddress
&InstanceId=i-instance1
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<AllocatePublicIpAddressResponse>
  <RequestId>F2EF6A3B-E345-46B9-931E-0EA094818567</RequestId>
  <IpAddress>10.1.149.159</IpAddress>
</AllocatePublicIpAddressResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"F2EF6A3B-E345-46B9-931E-0EA094818567",
	"IpAddress":"10.1.149.159"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|404|InvalidVlanId.NotFound|The VlanId provided does not exist in our records.|指定的虚拟局域网ID不存在。|
|403|InstanceExpiredOrInArrears|The specified operation is denied as your prepay instance is expired \(prepay mode\) or in arrears \(afterpay mode\).|包年包月实例已过期，请您续费后再进行操作。|
|404|InvalidIpAddress.NotFound|The specified IP is not in the specified vlan.|指定的 IP 不在指定的虚拟局域网内。|
|403|AllocatedAlready|There is an IpAddress allocated already for the specified instance.|（用户使用指定IP进行绑定时，）该实例已经被分配了别的IP地址。|
|400|OperationDenied|Specified operation is denied as your instance is in VPC.|由于实例存在于 VPC 中，指定的操作不合法。|
|400|AllocateIpInvalidInstanceBandwidth|OperationDenied The InternetMaxBandwidthOut of the specified instance cannot be less than 0.|请确保公网带宽至少大于0 才可分配 IP 地址。|
|400|OperationDenied|The specified parameter "VlanId" is not valid or vlan has not enough IP address.|指定的 VlanId 不合法，或已超出最大 IP 地址数限制。|
|403|NAT\_PUBLIC\_IP\_BINDING\_FAILED|Binding nat public ip failed|绑定公网 IP（NatPublicIp）失败。|
|403|NAT\_PUBLIC\_IP\_ALLOCATE\_FAILED|Nat public ip binding failed.|分配公网 IP（NatPublicIp）失败。|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Ecs)

