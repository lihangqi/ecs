# ModifyNetworkInterfaceAttribute {#ModifyNetworkInterfaceAttribute .reference}

修改一个弹性网卡（ENI）属性。

## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：ModifyNetworkInterfaceAttribute|
|RegionId|String|是|实例所在地域 ID。您可以调用 [DescribeRegions](intl.zh-CN/API参考/地域/DescribeRegions.md#) 查看最新的阿里云地域列表。|
|NetworkInterfaceId|String|是|弹性网卡 ID。|
|SecurityGroupId.N|String|否|安全组 ID，新的安全组将会覆盖旧的安全组，安全组必须跟弹性网卡在同一个 VPC 内。|
|NetworkInterfaceName|String|否|弹性网卡的名称。-   字符长度为 \[2, 128\] 个英文或中文字符，必须以大小字母或中文开头，可包含数字、下划线（\_） 或连字符（-）。
-   弹性网卡名称会展示在控制台。
-   不能以 http:// 和 https:// 开头。
-   不填则为空，默认值为空。

|
|Description|String|否|弹性网卡的描述信息。-   字符长度为 \[2, 256\] 个英文或中文字符。
-   不能以 http:// 和 https:// 开头。
-   不填则为空，默认值为空。

|

## 返回参数 {#section_f54_lk5_xdb .section}

全是公共返回参数。参阅 [公共参数](intl.zh-CN/API参考/调用方式/公共参数.md#commonResponseParameters)。

## 示例 { .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=ModifyNetworkInterfaceAttribute
&RegionId=cn-hangzhou
&NetworkInterfaceId=[networkInterfaceId]
&<公共请求参数>
```

**返回示例** 

**XML 格式**

```
<DetachNetworkInterfaceResponse>
    <RequestId>04F0F334-1335-436C-A1D7-6C044FExxxxx</RequestId>
</DetachNetworkInterfaceResponse>
```

 **JSON 格式** 

```
{
    "RequestId": "04F0F334-1335-436C-A1D7-6C044FExxxxx",
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问 [API 错误中心](https://error-center.alibabacloud.com/status/product/Ecs)。

|错误代码|错误信息|HTTP 状态码|说明|
|:---|:---|:-------|:-|
|UnsupportedParameter|The parameters is unsupported.|400|该参数不存在，或者不支持该参数。|
|MissingParameter|The input parameter that is mandatory for processing this request is not supplied.|400|缺少必需参数。|
|Abs.InvalidAccount.NotFound|The Account is not found or ak is expired.|403|您的阿里云账号不存在，或者您的 AccessKey 已经过期。|
|Forbidden.NotSupportRAM|This action does not support accessed by RAM mode.|403|不允许 RAM 用户执行该操作。|
|Forbidden.SubUser|The specified action is not available for you.|403|不允许 RAM 用户执行该操作。|
|InvalidOperation.AvailabilityZoneMismatch|The VPC VSwitch of the specified ENI and ECS instance are not in the same availability zone.|403|指定的 VPC 交换机 ID、弹性网卡和实例 ID 不在同一个可用区。|
|InvalidOperation.VpcMismatch|The VPC of the specified ENI and security group are not in the same VPC.|403|指定的弹性网卡和安全组 ID 不在同一个 VPC。|
|SecurityGroupInstanceLimitExceed|The maximum number of instances in a security group is exceeded.|403|该安全组内已有的实例数量已超出最大限制。|
|InvalidSecurityGroupId.NotVpc|The specified SecurityGroupId not in VPC.|403|指定的安全组 ID 不是 VPC 类型。|
|InvalidOperation.InvalidEniType|The operation is not allowed in the current ENI type.|403|当前弹性网卡类型不支持该操作。|
|InvalidVSwitchId.NotFound|The specified VSwitchId is not found.|404|指定的交换机 ID 不存在。|
|InvalidSecurityGroupId.NotFound|The specified SecurityGroupId is not found.|404|指定的安全组 ID 不存在。|

