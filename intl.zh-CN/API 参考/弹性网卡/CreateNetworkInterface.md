# CreateNetworkInterface {#CreateNetworkInterface .reference}

创建一个弹性网卡（ENI）。

## 描述 {#section_apy_dwn_ydb .section}

-   新创建的弹性网卡**可用**（`Available`）状态。

-   弹性网卡只支持附加到同一可用区的VPC类型实例。

-   一个弹性网卡只能附加到一台实例，附加到新实例之前您需要将其与当前实例分离。

-   弹性网卡重新附加到另一台实例时，其属性跟随该弹性网卡，网络流量也会重定向到新的实例。

-   一个账号在一个阿里云地域内默认最多可创建100个弹性网卡。如果需要更多，请[提交工单](https://workorder-intl.console.aliyun.com/#/ticket/createIndex)申请。


## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：CreateNetworkInterface|
|RegionId|String|是|实例所在地域的ID。您可以调用[DescribeRegions](../intl.zh-CN/API 参考/地域/DescribeRegions.md#)查看最新的阿里云地域列表。|
|VSwitchId|String|是|指定VPC的交换机ID。|
|SecurityGroupId|String|是|所属的安全组ID必须是同一个VPC下的安全组。|
|PrimaryIpAddress|String|否|弹性网卡的主私有IP地址。指定IP必须是在所属交换机的地址段内的空闲地址，不指定则默认随机分配该交换机中的空闲地址。|
|NetworkInterfaceName|String|否|弹性网卡名称。长度为\[2, 128\]个英文或中文字符。必须以大小字母或中文开头，不能以http://和https://开头。可以包含数字、半角冒号（:）、下划线（\_）或者连字符（-）。默认值：空。

|
|Description|String|否|弹性网卡的描述信息。长度为\[2, 256\]个英文或中文字符，不能以http://和https://开头。默认值：空。

|
|Tag.n.Key|String|否|弹性网卡的标签键。n的取值范围：\[1, 20\]。一旦传入该值，则不允许为空字符串。最多支持64个字符，不能以aliyun、acs:、http://或者https://开头。|
|Tag.n.Value|String|否|弹性网卡的标签值。n的取值范围：\[1, 20\]。一旦传入该值，可以为空字符串。最多支持128个字符，不能以aliyun、acs:、http://或者https://开头。|
|ClientToken|String|否|保证请求幂等性。从您的客户端生成一个参数值，确保不同请求间该参数值唯一。只支持ASCII字符，且不能超过64个字符。更多详情，请参阅[如何保证幂等性](../intl.zh-CN/API 参考/附录/如何保证幂等性.md#)。

|

## 返回参数 {#ResponseParameter .section}

|名称|类型|描述|
|:-|:-|:-|
|NetworkInterfaceId|String|弹性网卡ID|

## 示例 { .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=CreateNetworkInterface
&RegionId=cn-hangzhou
&VSwitchId=[vswitchid]
&SecurityGroupId=sg-c0003exxxxx
&<公共请求参数>
```

**返回示例**

**XML格式**

```
<CreateNetworkInterfaceResponse>
    <RequestId>04F0F334-1335-436C-A1D7-6C044FExxxxx</RequestId>
    <NetworkInterfaceId>eni-eniIxxxxx</NetworkInterfaceId>
</CreateNetworkInterfaceResponse>
```

**JSON格式**

```
{
    "RequestId": "04F0F334-1335-436C-A1D7-6C044FExxxxx",
    "NetworkInterfaceId": "eni-enixxxxx"
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问[API错误中心](https://error-center.alibabacloud.com/status/product/Ecs)。

|错误代码|错误信息|HTTP状态码|说明|
|:---|:---|:------|:-|
|MissingParameter|The input parameter that is mandatory for processing this request is not supplied.|400|缺少必需参数。|
|UnsupportedParameter|The parameters is unsupported.|400|该参数不存在，或者不支持该参数。|
|Abs.InvalidAccount.NotFound|The Account is not found or ak is expired.|403|您的阿里云账号不存在，或者您的AccessKey已经过期。|
|Forbidden.NotSupportRAM|This action does not support accessed by RAM mode.|403|不允许RAM用户执行该操作。|
|Forbidden.SubUser|The specified action is not available for you.|403|您无法执行该操作。|
|InvalidOperation.AvailabilityZoneMismatch|The VPC VSwitch of the specified ENI and ECS instance are not in the same availability zone.|403|指定的VPC交换机ID、弹性网卡和实例ID不在同一个可用区。|
|InvalidOperation.VpcMismatch|The VPC of the specified ENI and security group are not in the same VPC.|403|指定的弹性网卡和安全组ID不在同一个 VPC。|
|InvalidSecurityGroupId.NotVpc|The specified SecurityGroupId not in VPC.|403|指定的安全组不是VPC类型。|
|MaxEniCountExceeded|The number of ENI exceeds the limit per region.|403|该地域已有的弹性网卡数量超过了最大限制。|
|SecurityGroupInstanceLimitExceed|The maximum number of instances in a security group is exceeded.|403|该安全组内已有的实例数量已超出最大限制。|
|InvalidEcsId.NotFound|The specified EcsId is not found.|404|指定的实例ID不存在。|
|InvalidSecurityGroupId.NotFound|The specified SecurityGroupId is not found.|404|指定的安全组ID不存在。|
|InvalidVSwitchId.NotFound|The specified VSwitchId is not found.|404|指定的交换机ID不存在。|

