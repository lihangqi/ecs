# AttachClassicLinkVpc {#AttachClassicLinkVpc .reference}

将一台经典网络类型实例连接到 [专有网络 VPC](../../../../cn.zh-CN/产品简介/什么是专有网络.md#) 中，使经典网络类型实例可以和 VPC 中的云资源私网互通。更多详情，请参阅 *VPC* 文档 [ClassicLink 迁移概述](../../../../cn.zh-CN/用户指南/ClassicLink/ClassicLink概述.md#)。

## 描述 {#section_brt_tjn_ydb .section}

调用该接口时，您需要注意：

-   连接经典网络类型实例前，实例必须处于 **运行中**（`Running`）或者 **已停止**（`Stopped`）状态。

-   目标 VPC 必须已 [开启 ClassicLink 功能](../../../../cn.zh-CN/用户指南/ClassicLink/建立ClassicLink连接.md#)。

-   经典网络类型实例和 VPC 必须在同一个阿里云地域。


## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：AttachClassicLinkVpc|
|RegionId|String|是|实例所属的地域 ID。您可以调用 [DescribeRegions](cn.zh-CN/API 参考/地域/DescribeRegions.md#) 查看最新的阿里云地域列表。|
|InstanceId|String|是|经典网络类型实例 ID。您可以调用 [DescribeInstances](cn.zh-CN/API 参考/实例/DescribeInstances.md#) 查看您可用的实例。|
|VpcId|String|是|开启 ClassicLink 的 VPC ID。您可以调用 [DescribeVpcs](../../../../cn.zh-CN/API 参考/专有网络（VPC）/DescribeVpcs.md#) 查看您可用的 VPC。|

## 返回参数 {#section_f54_lk5_xdb .section}

全是公共返回参数。参阅 [公共参数](cn.zh-CN/API 参考/快速入门/公共参数.md#commonResponseParameters)。

## 示例 { .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=AttachClassicLinkVpc
&RegionId=cn-hangzhou
&InstanceId=i-test
&VpcId=vpc-test
&<公共请求参数>
```

**返回示例** 

**XML 格式**

```
<AttachClassicLinkVpcResponse>
    <RequestId>C0003E8B-B930-4F59-ADC0-0E209A9012A8</RequestId>
</AttachClassicLinkVpcResponse>
```

 **JSON 格式** 

```
{
    "RequestId": "C0003E8B-B930-4F59-ADC0-0E209A9012A8"
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问 [API 错误中心](https://error-center.aliyun.com/status/product/Ecs)。

|错误代码|错误信息|HTTP 状态码|说明|
|:---|:---|:-------|:-|
|Abs.InvalidInstanceId.MalFormed|The specified instance has already been linked to another VPC.|400|指定的实例已经被连接到其他 VPC 中。|
|InvalidInstanceId.MalFormed|The specified instance is not a classic network type instance.|400|指定的实例不是经典网络类型。|
|InvalidRegionId.Malformed|The specified RegionId is invalid.|400|指定的 `RegionId` 不存在或者未授权。|
|InvalidVpcId.Malformed|The specified VpcId is invalid.|400|指定的 `VpcId` 不合法。|
|InvalidInstanceId.NotBelong|The user does not own the specified instance.|403|指定的实例不属于该用户。|
|InvalidStatus.InstanceLocked|The specified instance is in another processing list.|403|指定的实例正在处理其他进程。|
|InvalidStatus.InstanceStatus|Only the Running or Stopped InstanceStatus is allowed.|403|连接经典网络类型实例前，实例必须处于 **运行中**（`Running`）或者 **已停止**（`Stopped`）状态。|
|OperationDenied|The specified VPC are unable to attach ClassicLink.|403|指定的 VPC 不能开启 ClassicLink 功能。|
|QuotaExceeded|The maximum number of links in the specified VPC exceeds.|403|当前 VPC 的可用链接数已经达到上限，最多允许 1000 台经典网络类型实例连接到同一个 VPC。|
|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|404|指定的 `InstanceId`不存在。|

