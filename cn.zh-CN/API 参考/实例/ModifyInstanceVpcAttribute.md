# ModifyInstanceVpcAttribute {#ModifyInstanceVpcAttribute .reference}

修改一台 ECS 实例的专有网络 VPC 属性。

## 描述 {#section_pgl_44t_xdb .section}

-   仅支持修改 **已停止**（`Stopped`）状态下 ECS 实例的 VPC 属性。
-   新建的 ECS 实例必须要经过一轮启动和停止才能调用该接口。
-   已成功修改 VPC 属性的 ECS 实例必须要经过一轮启动和停止才能调用该接口。
-   指定 `VSwitchId` 修改 VPC 属性时，指定的 `VSwitchId`，必须属于当前的专有网络。
-   指定 `VSwitchId` 不指定 `PrivateIpAddress` 时，系统自动为 ECS 实例分配一个私网 IP。
-   指定实例的当前交换机和新的交换机（`VSwitchId`）必须要属于同一个地域下的可用区。
-   指定实例的当前交换机和新的交换机（`VSwitchId`）必须要属于同一个 VPC 。
-   同时指定 `VSwitchId` 和 `PrivateIpAddress` 时，私网 IP 要属于指定交换机的 [网段](../../../../../cn.zh-CN/产品简介/什么是专有网络.md#section_w1b_tvz_ndb)。`PrivateIpAddress` 依赖于 `VSwitchId`，不能单独指定 `PrivateIpAddress`。
-   更多 VPC 相关接口，请参见 [专有网络（VPC）的 API 参考](../../../../../cn.zh-CN/API 参考/API概览.md#)。

## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：ModifyInstanceVpcAttribute|
|InstanceId|String|是|实例 ID。|
|VSwitchId|String|是|新的交换机 ID。指定实例的当前交换机和新的交换机（`VSwitchId`）必须要属于同一个地域下的可用区。|
|PrivateIpAddress|String|否|新的私网 IP 地址。`PrivateIpAddress` 依赖于 `VSwitchId`，不能单独指定 `PrivateIpAddress`。|

## 返回参数 {#section_zgl_44t_xdb .section}

全是公共返回参数。参阅 [公共参数](cn.zh-CN/API 参考/快速入门/公共参数.md#commonResponseParameters)

## 示例 { .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=ModifyInstanceVpcAttribute
&InstanceId=35F20777-0DFF-C152-41FA-BCE0EA0B2FD7
&VSwitchId=[vswitchid]
&<公共请求参数>
```

**返回示例** 

**XML 格式**

```
<ModifyInstanceAttributeResponse>
    <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</ModifyInstanceAttributeResponse>
```

**JSON 格式** 

```
{
    "RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E"
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问 [API 错误中心](https://error-center.aliyun.com/status/product/Ecs)。

|错误代码|错误信息|HTTP 状态码|说明|
|:---|:---|:-------|:-|
|IncorrectInstanceStatus|The current status of instance does not support this operation.|400|仅支持修改 **已停止**（`Stopped`）状态下 ECS 实例的 VPC 属性。|
|InvalidPrivateIp.Changing|Previous action is not finished yet.|400|实例修改私网 IP 暂未完成，无法重复操作。|
|InvalidPrivateIp.Changing|Specified private IP address is not in the CIDR block of virtual switch.|400|已成功修改 VPC 属性的 ECS 实例必须要经过一轮启动和停止才能调用该接口。|
|InvalidPrivateIpAddress.Duplicated|Specified private IP address is duplicated.|400|指定的私网 IP 已经被占用。|
|InvalidPrivateIpAddress.Malformed|Specified private IP address is malformed.|400|指定的私网 IP 不合法。|
|InvalidPrivateIpAddress.Mismatch|Specified private IP address is not in the CIDR block of virtual switch.|400|指定的私网 IP 不在指定交换机的网段中。|
|InvalidVSwitchId.Mismatch|Specified instance and virtual switch are not in the same zone.|400|指定的实例和指定的交换机（`VSwitchId`）必须属于同一个地域下的同一可用区。|
|OperationDenied|Specified operation is denied as your instance is not in VPC.|400|指定的实例的网络类型必须是专有网络（VPC）。|
|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|404|指定的 ECS 实例不存在。|
|InvalidVSwitchId.NotFound|Specified virtual switch does not exist.|404|指定的 VSwicthId 不存在。|
|InvalidVSwitchId.NotFound|Specified virtual switch is not found in current VPC.|404|指定实例的当前交换机和新的交换机必须要属于同一个 VPC 。|

