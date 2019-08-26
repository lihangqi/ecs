# DetachClassicLinkVpc {#doc_api_1000064 .reference}

取消经典网络类型实例与专有网络 VPC 的连接（ClassicLink）。更多详情，请参阅 VPC 文档 ClassicLink 迁移概述。取消 ClassicLink 后，经典网络类型实例无法与 VPC 互通。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=DetachClassicLinkVpc)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|InstanceId|String|是|i-test|经典网络类型实例 ID。

 |
|RegionId|String|是|cn-hangzhou|实例所属的地域 ID。您可以调用 [DescribeRegions](~~25609~~) 查看最新的阿里云地域列表。

 |
|VpcId|String|是|vpc-test|实例连接的 VPC ID。

 |
|Action|String|否|DetachClassicLinkVpc|系统规定参数。取值：DetachClassicLinkVpc

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。无论调用接口成功与否，我们都会返回请求 ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

https://ecs.aliyuncs.com/?Action=DetachClassicLinkVpc
&RegionId=cn-hangzhou
&VpcId=vpc-test
&InstanceId=i-test
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DetachClassicLinkVpcResponse>
  <RequestId>C0003E8B-B930-4F59-ADC0-0E209A9012A8</RequestId>
</DetachClassicLinkVpcResponse>

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
|403|OperationDenied|The instances are not allowed to detach from the linked vpc.|不允许将此实例与已连接的 VPC 分离。|
|403|InvalidStatus.InstanceStatus|The specified instance status is not support this operation ,expect status is running or shutted.|指定的实例状态不支持此操作，期望的操作状态是running或者shutted状态。|
|403|Forbidden.SubUser|User not authorized to operate on the specified resource.|子账号没有授权操作此资源。|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Ecs)

