# ModifyInstanceVncPasswd {#doc_api_1161588 .reference}

修改一台 ECS 实例的 Web 管理终端 密码。

## 描述 {#description .section}

-   密码长度必须是 6 位字符，只支持大小写英文字母和阿拉伯数字。
-   修改密码后：
    -   I/O 优化的实例，立刻生效，无需重启实例。
    -   非 I/O 优化的实例，需要在控制台 [重启实例](~~25440~~) 或者调用 API [RebootInstance](~~25502~~) 才能生效。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=ModifyInstanceVncPasswd)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|InstanceId|String|是|i-AY121018033933eae8689| ECS 实例。

 |
|RegionId|String|是|cn-hangzhou| ECS 实例所在的地域。您可以调用 [DescribeRegions](~~25609~~) 查看最新的阿里云地域列表。

 |
|VncPassword|String|是|123456| 新的 ECS 实例管理终端连接密码。

 |
|Action|String|否|ModifyInstanceVncPasswd| 接口名称。取值：**ModifyInstanceVncPasswd**

 |
|OwnerAccount|String|否|ECSforCloud@Alibaba.com| RAM用户的账号登录名称。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| 请求 ID。无论调用接口成功与否，我们都会返回请求 ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

https://ecs.aliyuncs.com/?Action=ModifyInstanceVncPasswd
&RegionId=cn-hangzhou
&InstanceId=i-AY121018033933eae8689
&VncPassword=123456
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ModifyInstanceVncPasswdResponse>
  <RequestId>FDB6C963-9CE8-4B7F-BCA3-845F6BD29AFC</RequestId>
</ModifyInstanceVncPasswdResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"FDB6C963-9CE8-4B7F-BCA3-845F6BD29AFC"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|403|IncorrectInstanceStatus|The current status of the resource does not support this operation.|该资源目前的状态不支持此操作。|
|400|IncorrectVncPassword.Malformed|The specified parameter VncPassword is not valid.|指定的 VNC 密码不合法。|
|404|NoSuchResource|The specified resource is not found.|指定的资源不存在|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Ecs)

