# ModifyDiskSpec {#doc_api_Ecs_ModifyDiskSpec .reference}

调用ModifyDiskSpec升级一块ESSD云盘的性能等级。

## 接口说明 {#description .section}

升级ESSD云盘性能级别时，您需要注意以下内容。

-   ESSD云盘的状态必须是**使用中**（In\_Use）状态或者**待挂载**（Available）状态。
-   若ESSD云盘已挂载到ECS实例上，实例必须处于**运行中**（Running）状态或者**已停止**（Stopped）状态，ECS实例不能处于过期或者账号欠费状态。
-   调用接口后，ESSD云盘性能等级变更立即生效。同时，系统按照新性能级别单价计算消费账单。
-   由于ESSD云盘性能等级受容量限制，如果您无法升级性能等级，可以扩容（[ResizeDisk](~~25522~~)）后重新操作。更多详情，请参见[ESSD云盘](~~122389~~)。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=ModifyDiskSpec)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|DiskId|String|是|d-bp131n0q38u3a4zi\*\*\*\*\*|ESSD云盘的ID。

 |
|PerformanceLevel|String|是|PL2|修改ESSD云盘的性能等级。取值范围：

 -   PL1（默认）：单盘最高随机读写IOPS 5万。
-   PL2：单盘最高随机读写IOPS 10万。
-   PL3：单盘最高随机读写IOPS 100万。

 **说明：** 修改后的性能等级不能低于修改前的性能等级。

 |
|Action|String|否|ModifyDiskSpec|系统规定参数。对于您自行拼凑HTTP/HTTPS URL发起的API请求，`Action`为必选参数。取值：ModifyDiskSpec

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=ModifyDiskSpec
&PerformanceLevel=PL2
&<公共请求参数>
```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ModifyDiskSpecResponse>
  <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</ModifyDiskSpecResponse>

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
|404|InvalidDiskId.NotFound|The specified disk does not exist.|指定的磁盘不存在。请您检查磁盘 ID 是否正确。|
|403|DiskInArrears|The specified operation is denied as your disk owing fee.|指定的磁盘已欠费。|
|404|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|指定的实例不存在，请您检查实例ID是否正确。|
|403|InstanceExpiredOrInArrears|The specified operation is denied as your prepay instance is expired \(prepay mode\) or in arrears \(afterpay mode\).|包年包月实例已过期，请您续费后再进行操作。|
|403|IncorrectDiskStatus|The current disk status does not support this operation.|当前的磁盘不支持此操作，请您确认磁盘处于正常使用状态，是否欠费。|
|403|DiskCreatingSnapshot|The operation is denied due to a snapshot of the specified disk is not completed yet.|指定的磁盘正在创建快照。|
|403|OperationDenied|The type of the disk does not support the operation.|此磁盘种类不支持指定的操作。|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Ecs)

