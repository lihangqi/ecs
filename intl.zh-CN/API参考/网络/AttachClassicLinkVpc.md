# AttachClassicLinkVpc {#doc_api_1000063 .reference}

将一台经典网络类型实例连接到专有网络 VPC 中，使经典网络类型实例可以和 VPC 中的云资源私网互通。更多详情，请参阅 VPC 文档 ClassicLink 迁移概述。

## 描述 {#description .section}

调用该接口时，您需要注意：

-   连接经典网络类型实例前，实例必须处于运行中（Running）或者已停止（Stopped）状态。
-   目标 VPC 必须已 [开启 ClassicLink 功能](~~65413~~)。
-   经典网络类型实例和 VPC 必须在同一个阿里云地域。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=AttachClassicLinkVpc)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|InstanceId|String|是|i-test|经典网络类型实例 ID。您可以调用 [DescribeInstances](~~25506~~) 查看您可用的实例。

 |
|RegionId|String|是|cn-hangzhou|实例所属的地域 ID。您可以调用 [DescribeRegions](~~25609~~) 查看最新的阿里云地域列表。

 |
|VpcId|String|是|vpc-test|开启 ClassicLink 的 VPC ID。您可以调用 [DescribeVpcs](~~35739~~) 查看您可用的 VPC。

 |
|Action|String|否|AttachClassicLinkVpc|系统规定参数。取值：AttachClassicLinkVpc

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。无论调用接口成功与否，我们都会返回请求 ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

https://ecs.aliyuncs.com/?Action=AttachClassicLinkVpc
&RegionId=cn-hangzhou
&InstanceId=i-test
&VpcId=vpc-test
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<AttachClassicLinkVpcResponse>
  <RequestId>C0003E8B-B930-4F59-ADC0-0E209A9012A8</RequestId>
</AttachClassicLinkVpcResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"C0003E8B-B930-4F59-ADC0-0E209A9012A8"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|403|InvalidRegionId.Malformed|The specified parameter ?RegionId? is not valid.|指定的 RegionId 不合法。|
|403|OperationDenied|The instance does not allow link to vpc.|不允许将此实例与 VPC 连接。|
|403|Abs.InvalidInstanceId.MalFormed|The instance has been linked to other vpc|指定的实例已经被链接到了其他VPC网络。|
|403|OperationDenied|The specified vpc is disabled attach classic link.|指定的VPC网络禁止创建classicLink链接。|
|403|InvalidStatus.InstanceStatus|The specified instance status is not support this operation ,expect status is running or shutted.|指定的实例状态不支持此操作，期望的操作状态是running或者shutted状态。|
|403|InvalidStatus.InstanceStatus|The specified instance status is not support this operation, expect status is running or shutted.|指定的实例状态不支持此操作，期望的操作状态是running或者shutted状态 。|
|403|QuotaExceeded|The link quota exceeded in this vpc.|已达到指定的VPC网络创建链接的配额。|
|403|InvalidStatus.InstanceLocked|The specified instance is locked,please wait more.|指定的实例被锁定，请等待解锁后再操作。|
|403|InvalidInstanceId.LimitedRegion|The specified instance does not support this operation due to the limitation of its region.|指定的实例在受限区域，不支持创建classicLink链接 。|
|403|Forbidden.SubUser|User not authorized to operate on the specified resource.|子账号没有授权操作此资源。|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Ecs)

