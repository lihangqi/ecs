# ConvertNatPublicIpToEip {#ConvertNatPublicIpToEip .reference}

将一台网络类型为专有网络VPC的ECS实例的公网 IP（NatPublicIp）转化为弹性公网IP（EIP）。

## 描述 {#section_o52_y3n_ydb .section}

调用该接口时，您需要注意：

-   仅支持VPC网络类型的ECS实例。
-   仅支持状态为 **已停止**（`Stopped`）或者 **运行中**（`Running`）的ECS实例。
-   不支持公网带宽为0 Mbps的实例，此时该ECS实例没有分配公网IP（`NatPublicIp`）。
-   不支持已经绑定了EIP的ECS实例。
-   不支持有未生效的变更配置任务ECS实例。
-   不支持即将在24小时内到期的ECS实例。
-   公网IP（`NatPublicIp`）转换为EIP后，EIP将单独计费。EIP的计费方式参阅 [EIP计费说明](../../../../../cn.zh-CN/产品定价/预付费.md#)。
-   不支持 [公网带宽](../cn.zh-CN/产品定价/公网带宽计费.md#) 为 按固定带宽计费 的 [预付费（包年包月）](../cn.zh-CN/产品定价/预付费（包年包月）.md#)ECS实例。

## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：ConvertNatPublicIpToEip|
|RegionId|String|是|实例所属的地域ID。您可以调用 [DescribeRegions](cn.zh-CN/API 参考/地域/DescribeRegions.md#) 查看最新的阿里云地域列表。|
|InstanceId|String|是|需要转化公网IP的实例ID。|

## 返回参数 {#ResponseParameter .section}

全是公共返回参数。参阅 [公共返回参数](cn.zh-CN/API 参考/快速入门/公共参数.md#commonResponseParameters)。

## 示例 { .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=ConvertNatPublicIpToEip
&RegionId=cn-hangzhou
&InstanceId=i-test
&<公共请求参数>
```

**返回示例** 

**XML 格式**

```
<ConvertNatPublicIpToEipResponse>
    <RequestId>B154D309-F3E1-4AB7-BA94-FEFCA8B89001</RequestId>
</ConvertNatPublicIpToEipResponse>
```

**JSON 格式** 

```
{
   "RequestId":"B154D309-F3E1-4AB7-BA94-FEFCA8B89001"
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问 [API 错误中心](https://error-center.aliyun.com/status/product/Ecs)。

|错误代码|错误信息|HTTP 状态码|说明|
|:---|:---|:-------|:-|
|InvalidRegionId.Malformed|The specified RegionId is invalid.|400|指定的 `RegionId` 不存在或者未授权。|
|InvalidEndTime.Malformed|The specified instance is about to expire within 24 hours.|403|实例即将在24小时内到期，不能变更公网IP。|
|InvalidInstanceId.PlanedChange|The instance has uncompleted changes.|403|实例有未生效的变更配置任务。|
|InvalidInstanceStatus.Released|The specified instance has been released.|403|指定的实例已经被释放。|
|IncorrectInstanceStatus|The instance status does not support this operation. The instance may be expired, upgrading, starting, or locked.|404|仅支持 **已停止**（`Stopped`）和 **运行中**（`Running`）的ECS实例。|
|InstanceTypeNotSupported|The specified instance is a subscription instance with a specified bandwidth.|404|指定的实例是包年包月固定带宽类型的实例。|
|InvalidInstance.ZeroBandwidth|The public network bandwidth for the specified instance is zero. That is, this instance does not have a public IP.|404|实例公网带宽为0 Mbps，此时该实例无公网IP。|
|InvalidInstanceId.NotFound|The specified instance does not exist, or does not belong to you.|404|指定的实例不存在或者归属不正确。|
|OperationDenied|The network type of the specified instance is not VPC.|404|指定的实例的网络类型不是VPC。|

