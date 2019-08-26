# JoinResourceGroup {#JoinResourceGroup .reference}

将一个ECS资源或者服务加入另一个资源组。资源是您在阿里云创建的云服务实体，例如，一台ECS实例、一个ECS弹性网卡或者一份ECS镜像等都可以是资源。资源组是项目、环境或者栈的基础设施集合，在资源组里管理资源能集中监控和执行任务，免去了在多种阿里云服务间反复查看的负担。

## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：JoinResourceGroup|
|RegionId|String|是|资源所在的地域ID。您可以调用[DescribeRegions](../cn.zh-CN/API 参考/地域/DescribeRegions.md#)查看最新的阿里云地域列表。|
|ResourceType|String|是|ECS资源的类型。取值范围： instance（实例） | disk（磁盘） | snapshot（快照） | image（镜像） | securitygroup（安全组） | ddh（专有宿主机） | eni（弹性网卡） | keypair（密钥对） | launchtemplate（启动模板）以上参数取值均大小写敏感。

|
|ResourceId|String|是|资源类型的ID标识符。例如，当`ResourceType=instance`时，则ResourceId可以理解为`InstanceId`。|
|ResourceGroupId|String|是|目标资源组ID。|

## 返回参数 {#ResponseParameter .section}

全是公共返回参数。参阅[公共返回参数](../cn.zh-CN/API 参考/快速入门/公共参数.md#commonResponseParameters)。

## 示例 { .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=JoinResourceGroup
&RegionId=cn-hangzhou
&RsourceType=securitygroup
&ResourceId=sg-securitygroupid
&ResourceGroupId=rg-resourcegrouid
&<公共请求参数>
```

**返回示例**

**XML格式**

```
<JoinResourceGroupResponse>
    <RequestId>C0003E8B-B930-4F59-ADC0-0E20xxxxxxxx</RequestId>
</JoinResourceGroupResponse>
```

**JSON格式**

```
{
    "RequestId": "C0003E8B-B930-4F59-ADC0-0E20xxxxxxxx"
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问[API错误中心](https://error-center.aliyun.com/status/product/Ecs)。

|错误代码|错误信息|HTTP状态码|说明|
|:---|:---|:------|:-|
|MissingParameter|The input parameter that is mandatory for processing this request is not supplied.|403|请求中不能缺乏必需参数。|
|InvalidResourceGroup.NotFound|The ResourceGroup provided does not exist in our records.|404|指定的资源组不存在。|
|InvalidResourceId.NotFound|The ResourceId provided does not exist in our records.|404|指定的资源ID不存在。|
|InvalidResourceType.NotFound|The ResourceType provided does not exist in our records.|404|不支持指定的资源类型。|

