# ModifyInstanceVpcAttribute {#doc_api_1025864 .reference}

修改一台 ECS 实例的专有网络 VPC 属性。

## 描述 {#description .section}

当您使用该接口时，请注意：

-   仅支持修改 **已停止**（`Stopped`）状态下 ECS 实例的 VPC 属性。
-   新建的 ECS 实例必须要经过一轮启动和停止才能调用该接口。
-   已成功修改 VPC 属性的 ECS 实例必须要经过一轮启动和停止才能调用该接口。
-   指定 `VSwitchId` 修改 VPC 属性时，指定的 `VSwitchId`，必须属于当前的专有网络。
-   指定 `VSwitchId` 不指定 `PrivateIpAddress` 时，系统自动为 ECS 实例分配一个私网 IP。
-   指定实例的当前交换机和新的交换机（`VSwitchId`）必须要属于同一个地域下的可用区。
-   指定实例的当前交换机和新的交换机（`VSwitchId`）必须要属于同一个 VPC 。
-   同时指定 `VSwitchId` 和 `PrivateIpAddress` 时，私网 IP 要属于指定交换机的 [网段](~~34217~~)。`PrivateIpAddress` 依赖于 `VSwitchId`，不能单独指定 `PrivateIpAddress`。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=ModifyInstanceVpcAttribute)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|InstanceId|String|是|i-bp1iudwa5b1tqaxxxxxx|实例 ID。

 |
|VSwitchId|String|是|\[vswitchid\]|新的交换机 ID。指定实例的当前交换机和新的交换机（**VSwitchId**）必须要属于同一个地域下的可用区。

 |
|Action|String|否|ModifyInstanceVpcAttribute|接口名称。取值：**ModifyInstanceVpcAttribute**

 |
|OwnerAccount|String|否|ECSforCloud@Alibaba.com|RAM用户的账号登录名称。

 |
|PrivateIpAddress|String|否|172.17.XX.XXX|新的私网 IP 地址。**PrivateIpAddress** 依赖于 **VSwitchId**，不能单独指定 **PrivateIpAddress**。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。无论调用接口成功与否，我们都会返回请求 ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

https://ecs.aliyuncs.com/?Action=ModifyInstanceVpcAttribute
&InstanceId=i-bp1iudwa5b1tqaxxxxxx
&VSwitchId=[vswitchid]
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ModifyInstanceAttributeResponse>
  <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</ModifyInstanceAttributeResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|IncorrectVSwitchStatus|The current status of virtual switch does not support this operation.|指定的虚拟交换机处于pending状态，无法删除。|
|400|IncorrectInstanceStatus|The current status of instance does not support this operation.|目前实例状态不支持此类操作。|
|400|OperationDenied|Specified operation is denied as your instance is not in VPC.|实例不存在于 VPC 中，指定的操作被拒绝。|
|400|InvalidVSwitchId.Mismatch|Specified instance and virtual switch are not in the same zone.|指定的实例和指定的虚拟交换机不属于同一个可用区。|
|400|InvalidPrivateIpAddress.Mismatch|Specified private IP address is not in the CIDR block of virtual switch.|指定的私网IP不在指定虚拟交换机的网段中。|
|404|InvalidVSwitchId.NotFound|Specified virtual switch is not found in current VPC.|当前 VPC 中不存在指定的虚拟交换机。|
|404|NoSuchResource|The specified resource is not found.|指定的资源不存在|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Ecs)

