# DeleteSnapshot {#DeleteSnapshot .reference}

删除指定的快照。如果需要取消正在创建的快照，也可以调用该接口删除快照，即取消创建快照任务。

## 描述 {#section_j3f_mxz_xdb .section}

调用该接口时，您需要注意：

-   如果指定的快照 ID 不存在，请求将被忽略。

-   如果快照已经被用于创建自定义镜像，则快照不能被删除。您需要先删除已创建的自定义镜像（[DeleteImage](intl.zh-CN/API参考/镜像/DeleteImage.md#)），才能继续删除快照。


## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：DeleteSnapshot|
|SnapshotId|String|是|快照 ID。|

## 返回参数 {#section_o3f_mxz_xdb .section}

全是公共返回参数。参阅 [公共参数](intl.zh-CN/API参考/调用方式/公共参数.md#commonResponseParameters)。

## 示例 { .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=DeleteSnapshot
&SnapshotId=s-923FE2BF0
&<公共请求参数>
```

**返回示例** 

**XML 格式**

```
<DeleteSnapshotResponse>
     <RequestId>CEF72CEB-54B6-4AE8-B225-F876FF7BA984</RequestId>
</DeleteSnapshotResponse>
```

 **JSON 格式** 

```
{
    "RequestId": "CEF72CEB-54B6-4AE8-B225-F876FF7BA984"
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问 [API 错误中心](https://error-center.alibabacloud.com/status/product/Ecs)。

|错误代码|错误信息|HTTP 状态码|说明|
|:---|:---|:-------|:-|
|MissingParameter|The input parameter SnapshotId that is mandatory for processing this request is not supplied.|400|您必须指定参数 `SnapshotId`。|
|SnapshotCreatedDisk|The snapshot has been used to create disk\(s\).|403|指定快照已经创建了磁盘。|
|SnapshotCreatedImage|The snapshot has been used to create user defined image\(s\).|403|指定快照已经被用于创建自定义镜像。您需要先删除已创建的自定义镜像。|

