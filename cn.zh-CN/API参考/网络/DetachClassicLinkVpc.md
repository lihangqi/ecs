# DetachClassicLinkVpc {#DetachClassicLinkVpc .reference}

取消经典网络类型实例与专有网络 VPC 的连接（ClassicLink）。更多详情，请参阅 *VPC* 文档 [ClassicLink 迁移概述](../../../../../cn.zh-CN/用户指南/ClassicLink/ClassicLink概述.md#)。取消 ClassicLink 后，经典网络类型实例无法与 VPC 互通。

## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：DetachClassicLinkVpc|
|RegionId|String|是|实例所属的地域 ID。您可以调用 [DescribeRegions](cn.zh-CN/API参考/地域/DescribeRegions.md#) 查看最新的阿里云地域列表。|
|InstanceId|String|是|经典网络类型实例 ID。|
|VpcId|String|是|实例连接的 VPC ID。|

## 返回参数 {#section_f54_lk5_xdb .section}

全是公共返回参数。参阅 [公共参数](cn.zh-CN/API参考/HTTP调用方式/公共参数.md#commonResponseParameters)。

## 示例 { .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=DetachClassicLinkVpc
&RegionId=cn-hangzhou
&VpcId=vpc-test
&InstanceId=i-test
&<公共请求参数>
```

**返回示例** 

**XML 格式**

```
<DetachClassicLinkVpcResponse>
    <RequestId>C0003E8B-B930-4F59-ADC0-0E209A9012A8</RequestId>
</DetachClassicLinkVpcResponse>
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
|InvalidInstanceId.MalFormed|The specified instance is not a classic network type instance.|400|指定的实例不是经典网络类型。|
|InvalidRegionId.Malformed|The specified RegionId is invalid.|400|指定的 `RegionId` 不存在或者未授权。|
|InvalidVpcId.Malformed|The specified VpcId is invalid.|400|指定的 `VpcId` 不合法。|
|InvalidInstanceId.NotBelong|The user does not own the specified instance.|403|指定的实例不属于您。|
|InvalidStatus.InstanceLocked|The specified instance is in another process list.|403|指定的实例正在处理其他进程。|
|InvalidStatus.InstanceStatus|Only the Running or Stopped InstanceStatus is allowed.|403|仅 **运行中**（`Running`） 或 **已停止**（`Stopped`） 的实例支持该操作。|
|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|404|指定的 `InstanceId` 不存在。|

