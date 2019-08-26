# DetachDisk {#doc_api_999557 .reference}

从一台实例上卸载一块按量付费磁盘。磁盘类型包括普通云盘、高效云盘和SSD云盘。

## 描述 {#description .section}

当您使用该接口时，请注意：

-   云盘的 Portable 属性必须为 True。
-   云盘必须已经挂载到实例上，状态为 使用中（In\_Use\)。
-   云盘所挂载的实例的状态必须为 运行中（Running）或者 已停止（Stopped）。
-   云盘所挂载的实例被 [安全控制](~~25695~~) 后，OperationLocks 中不能标记为 "LockReason" : "security" 的锁定状态。
-   卸载磁盘后，其属性 DeleteWithInstance 会被置为 False，表示释放该实例时，会保留该云盘，不随实例一起释放。
-   该接口是异步操作，调用接口成功后您需要等待片刻才能完成卸载，预计在 1 分钟左右。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=DetachDisk)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|DiskId|String|是|d-diskid1|待卸载的云盘 ID。

 |
|InstanceId|String|是|i-instanceid1|待卸载的 ECS 实例 ID。

 |
|Action|String|否|DetachDisk|系统规定参数。取值：DetachDisk

 |
|OwnerAccount|String|否|ECSforCloud@Alibaba.com|RAM 用户的账号登录名称。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。无论调用接口成功与否，我们都会返回请求 ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

https://ecs.aliyuncs.com/?Action=DetachDisk
&DiskId=d-diskid1
&InstanceId=i-instanceid1
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DetachDiskResponse>
  <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</DetachDiskResponse>

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
|403|InstanceLockedForSecurity|The instance is locked due to security.|您的资源被安全锁定，拒绝操作。|
|400|InvalidOperation.InstanceTypeNotSupport|The instance type of the specified instance does not support hot detach disk.|磁盘挂载的实例不支持磁盘热插拔操作。|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Ecs)

