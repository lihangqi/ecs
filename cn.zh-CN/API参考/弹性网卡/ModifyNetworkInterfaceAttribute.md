# ModifyNetworkInterfaceAttribute {#doc_api_Ecs_ModifyNetworkInterfaceAttribute .reference}

调用ModifyNetworkInterfaceAttribute修改一个弹性网卡（ENI）的属性。例如，弹性网卡名称、描述以及所属安全组等。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=ModifyNetworkInterfaceAttribute&type=RPC&version=2014-05-26)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|NetworkInterfaceId|String|是|eni-myeni|弹性网卡 ID。

 |
|RegionId|String|是|cn-hangzhou|弹性网卡所在地域 ID。您可以调用 [DescribeRegions](~~25609~~) 查看最新的阿里云地域列表。

 |
|Action|String|否|ModifyNetworkInterfaceAttribute|系统规定参数。取值：ModifyNetworkInterfaceAttribute

 |
|Description|String|否|test|弹性网卡的描述信息。

 -   字符长度为2~256个英文或中文字符。
-   不能以 http:// 和 https:// 开头。
-   不填则为空，默认值为空。

 |
|NetworkInterfaceName|String|否|my-eni-name|弹性网卡的名称。

 -   字符长度为2~128个英文或中文字符，必须以大小字母或中文开头，可包含数字、下划线（\_） 或连字符（-）。
-   弹性网卡名称会展示在控制台。
-   不能以 http:// 和 https:// 开头。
-   不填则为空，默认值为空。

 |
|SecurityGroupId.N|RepeatList|否|sg-securitygroupid|SecurityGroupId 列表，弹性网卡最终加入的安全组，并会移出已有的安全组。N的取值范围为1-5。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=ModifyNetworkInterfaceAttribute
&NetworkInterfaceId=eni-myeni
&RegionId=cn-hangzhou
&SecurityGroupId.1=sg-1133**
&NetworkInterfaceName=my-eni-name
&Description=test
&<公共请求参数>
```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DetachNetworkInterfaceResponse>
      <RequestId>04F0F334-1335-436C-A1D7-6C044FExxxxx</RequestId>
</DetachNetworkInterfaceResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"04F0F334-1335-436C-A1D7-6C044FExxxxx"
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
|400|InvalidParams.EniId|%s|指定的网卡ID格式不合法。|
|404|InvalidEcsId.NotFound|%s|指定的实例ID不存在。|
|404|InvalidEniId.NotFound|%s|指定的网卡ID不存在。|
|404|InvalidVSwitchId.NotFound|%s|指定的交换机ID不存在。|
|404|InvalidSecurityGroupId.NotFound|%s|指定的安全组ID不存在。|
|403|EniPerInstanceLimitExceeded|%s|弹性网卡的数量超过了指定实例类型允许的最大值。|
|403|InvalidOperation.AvailabilityZoneMismatch|%s|指定的VPC交换机ID、弹性网卡和实例ID不在同一个可用区。|
|403|InvalidOperation.VpcMismatch|%s|指定的弹性网卡和安全组ID不在同一个 VPC。|
|403|SecurityGroupInstanceLimitExceed|%s|该安全组内已有的实例数量已超出最大限制。|
|403|InvalidSecurityGroupId.NotVpc|%s|指定的安全组 ID 不是 VPC 类型。|
|403|InvalidOperation.InvalidEniType|%s|当前弹性网卡类型不支持该操作。|
|400|Forbidden.RegionId|%s|当前区域暂不支持此功能。|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

