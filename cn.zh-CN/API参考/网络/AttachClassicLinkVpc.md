# AttachClassicLinkVpc {#doc_api_Ecs_AttachClassicLinkVpc .reference}

调用AttachClassicLinkVpc将一台经典网络类型实例连接到专有网络VPC中，使经典网络类型实例可以和VPC中的云资源私网互通。

## 接口说明 {#description .section}

调用该接口时，您需要注意：

-   连接经典网络类型实例前，实例必须处于**运行中**（Running）或者**已停止**（Stopped）状态。
-   目标VPC必须已[开启ClassicLink功能](~~65413~~)。
-   经典网络类型实例和VPC必须在同一个阿里云地域。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=AttachClassicLinkVpc&type=RPC&version=2014-05-26)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|InstanceId|String|是|i-test|经典网络类型实例ID。您可以调用[DescribeInstances](~~25506~~)查看您可用的实例。

 |
|RegionId|String|是|cn-hangzhou|实例所属的地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。

 |
|VpcId|String|是|vpc-test|开启ClassicLink的VPC ID。您可以调用[DescribeVpcs](~~35739~~)查看您可用的VPC。

 |
|Action|String|否|AttachClassicLinkVpc|系统规定参数。取值：AttachClassicLinkVpc

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。

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
|403|InvalidInstanceId.NotFound|The InstanceId provided does not exist in our records.|指定的实例不存在，请您检查实例ID是否正确。|
|403|InvalidRegionId.Malformed|The specified parameter ?RegionId? is not valid.|指定的 RegionId 不合法。|
|403|InvalidVpcId.Malformed|The specified parameter ?VpcId? is not valid.|指定的 VpcId 不合法。|
|403|InvalidInstanceId.MalFormed|The specified instance is not a classic network instance.|指定的实例不是经典网络实例。|
|403|OperationDenied|The instance does not allow link to vpc.|不允许将此实例与 VPC 连接。|
|403|InvalidParameter.InvalidInstanceIdAndVpcId|The parameter InstanceId and VpcId are not allowed to be empty at the same time.|至少指定一个 InstanceId 或 VpcId。|
|403|OperationDenied|The specified vpc is disabled attach classic link.|指定的VPC网络禁止创建classicLink链接。|
|403|InvalidInstanceId.NotFound|The specified instance does not exist.|指定的实例不存在，请您检查实例ID是否正确。|
|403|InvalidStatus.InstanceStatus|The specified instance status is not support this operation ,expect status is running or shutted.|指定的实例状态不支持此操作，期望的操作状态是running或者shutted状态。|
|403|InvalidStatus.InstanceStatus|The specified instance status is not support this operation, expect status is running or shutted.|指定的实例状态不支持此操作，期望的操作状态是running或者shutted状态 。|
|403|InvalidInstanceId.NotBelong|The specified instance is not belong to you.|指定的实例不在您账号下。|
|403|QuotaExceeded|The link quota exceeded in this vpc.|已达到指定的VPC网络创建链接的配额。|
|403|InvalidStatus.InstanceLocked|The specified instance is locked,please wait more.|指定的实例被锁定，请等待解锁后再操作。|
|403|InvalidInstanceId.LimitedRegion|The specified instance does not support this operation due to the limitation of its region.|指定的实例在受限区域，不支持创建classicLink链接 。|
|403|Forbidden.SubUser|User not authorized to operate on the specified resource.|子账号没有授权操作此资源。|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

