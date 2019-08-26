# ModifyInstanceVncPasswd {#ModifyInstanceVncPasswd .reference}

修改一台 ECS 实例的 [Web 管理终端](../../../../intl.zh-CN/用户指南/连接实例/使用管理终端连接 ECS 实例.md) 密码。

## 描述 {#section_m4j_bst_xdb .section}

-   密码长度必须是 6 位字符，只支持大小写英文字母和阿拉伯数字。
-   修改密码后：
    -   I/O 优化的实例，立刻生效，无需重启实例。
    -   非I/O优化的实例，需要在控制台 [重启实例](../../../../intl.zh-CN/用户指南/实例/重启实例.md) 或者调用 API [RebootInstance](intl.zh-CN/API参考/实例/RebootInstance.md#) 才能生效。

## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：ModifyInstanceVncPasswd|
|RegionId|String|是|ECS 实例所在的地域。您可以调用 [DescribeRegions](intl.zh-CN/API参考/地域/DescribeRegions.md#) 查看最新的阿里云地域列表。|
|InstanceId|String|是|ECS 实例。|
|VncPassword|String|是|新的 ECS 实例管理终端连接密码。|

## 返回参数 {#section_u4j_bst_xdb .section}

全是公共返回参数。参阅 [公共参数](intl.zh-CN/API参考/调用方式/公共参数.md#commonResponseParameters)

## 示例 { .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=ModifyInstanceVncPasswd
&DescribeInstanceVncUrl
&InstanceId=AY121018033933eae8689
&VncPassword=123456
&<公共请求参数>
```

**返回示例** 

**XML 格式**

```
<ModifyInstanceVncPasswdResponse>
    <RequestId>FDB6C963-9CE8-4B7F-BCA3-845F6BD29AFC</RequestId>
</ModifyInstanceVncPasswdResponse>
```

 **JSON 格式** 

```
{
  "RequestId": "FDB6C963-9CE8-4B7F-BCA3-845F6BD29AFC", 
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问 [API 错误中心](https://error-center.alibabacloud.com/status/product/Ecs)。

|错误代码|错误信息|HTTP 状态码|说明|
|:---|:---|:-------|:-|
|IncorrectVncPassword.Malformed|The specified parameter VncPassword is not valid.|400|指定的参数 `VncPassword` 不合法，密码长度必须是 6 位字符，只支持大小写英文字母和阿拉伯数字。|
|IncorrectInstanceStatus|The current status of the resource does not support this operation.|403|指定实例的状态需要处于 **运行中**（`Running`）。|
|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|404|指定的 ECS 实例不存在。|
|InvalidRegionId.NotFound|The specified RegionId does not exist.|404|指定的 `RegionId` 不存在。|

