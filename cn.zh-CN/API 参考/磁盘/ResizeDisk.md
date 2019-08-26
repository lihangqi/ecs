# ResizeDisk {#ResizeDisk .reference}

扩容一块数据盘。

## 描述 {#section_szg_25y_xdb .section}

调用该接口时，您需要注意：

-   该接口暂时仅支持扩容数据盘，不支持扩容系统盘。

-   仅支持扩容磁盘类型为普通云盘（`Cloud`）、高效云盘（`Cloud_efficiency`）和 SSD 云盘（`Cloud_ssd`）的数据盘。

-   当磁盘正在创建快照时，不允许扩容。

-   对于已挂载的数据盘：

    -   磁盘挂载的实例的状态必须为 **运行中**（`Running`）或者 **已停止**（`Stopped`）。

    -   扩容后，您需要在控制台 [重启实例](../cn.zh-CN/用户指南/实例/重启实例.md#) 或者调用 API [RebootInstance](cn.zh-CN/API参考/实例/RebootInstance.md#) 使操作生效。

-   扩容时，不会修改磁盘分区和文件系统，您需要在扩容后自行分配存储空间。


## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：ResizeDisk|
|DiskId|String|是|磁盘 ID。|
|NewSize|Integer|是|希望扩容到的磁盘容量大小。单位为 GB。取值范围：-   普通云盘（`Cloud`）：\[5, 2000\]
-   高效云盘（`Cloud_efficiency`）:\[5, 2000\]
-   SSD 云盘（`Cloud_ssd`）：\[5, 2000\]

指定的新磁盘容量必须比原磁盘容量大。且 2 TB 以下的磁盘不能扩容到 2 TB 以上。|
|ClientToken|String|否|用于保证请求的幂等性。由客户端生成该参数值，要保证在不同请求间唯一。只支持 ASCII 字符，且不能超过 64 个字符。更多详情，请参阅 [如何保证幂等性](cn.zh-CN/API参考/附录/如何保证幂等性.md#)。|

## 返回参数 {#section_c1h_25y_xdb .section}

全是公共返回参数。参阅 [公共参数](cn.zh-CN/API参考/调用方式/公共参数.md#commonResponseParameters)

## 示例 { .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=ResizeDisk
&DiskId=xxx
&NewSize=1024
&<公共请求参数>
```

**返回示例** 

**XML 格式**

```
<ResizeDiskResponse>
    <RequestId>F3CD6886-D8D0-4FEE-B93E-1B73239673DE</RequestId>
</ResizeDiskResponse>
```

 **JSON 格式** 

```
{
    "RequestId": "F3CD6886-D8D0-4FEE-B93E-1B73239673DE"
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问 [API 错误中心](https://error-center.aliyun.com/status/product/Ecs)。

|错误代码|错误信息|HTTP 状态码|说明|
|:---|:---|:-------|:-|
|DiskCreatingSnapshot|The operation is denied due to a snapshot of the specified disk is not completed yet.|403|指定的磁盘正在创建快照，请稍后再试。|
|DiskError|IncorrectDiskStatus|403|磁盘状态异常。|
|DiskInArrears|The specified operation is denied as your disk owing fee.|403|指定磁盘已经欠费。|
|IncorrectInstanceStatus|The current status of the resource does not support this operation.|403|磁盘挂载的实例的状态必须为 **运行中**（`Running`）或者 **已停止**（`Stopped`）。|
|InstanceExpiredOrInArrears|The specified operation is denied as your prepay instance is expired \(prepay mode\) or in arrears \(afterpay mode\).|403|指定磁盘挂载的实例已过期。|
|InvalidDiskSize.TooLarge|Specified new disk size is beyond the permitted range.|403|指定的新磁盘大小超出取值范围。|
|InvalidDiskSize.TooSmall|Specified new disk size is less than the original disk size.|403|指定的新磁盘容量必须比原磁盘容量大。|
|OperationDenied|The status of the disk or the instance that the disk is attaching with does not support the operation.|403|仅支持扩容数据盘。或者磁盘挂载的实例的状态必须为 **运行中**（`Running`）或者 **已停止**（`Stopped`）。|
|OperationDenied|The type of the disk does not support the operation.|403|仅支持扩容普通云盘、高效云盘和 SSD 云盘。|
|InvalidDiskId.NotFound|The specified disk does not exist.|404|指定的磁盘不存在。|
|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|404|指定的 ECS 实例不存在。|

