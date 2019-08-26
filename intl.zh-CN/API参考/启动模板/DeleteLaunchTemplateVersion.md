# DeleteLaunchTemplateVersion {#doc_api_999544 .reference}

删除指定实例启动模板的一个版本。不支持删除默认版本，您需要通过 DeleteLaunchTemplate 删除整个实例启动模板才能删除默认版本。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=DeleteLaunchTemplateVersion)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|DeleteVersion.N|RepeatList|是|2|模板版本号，n 的取值范围 1~29。您可以调用 [DescribeLaunchTemplateVersions](~~73761~~) 查询启动模板版本号列表。

 |
|RegionId|String|是|cn-hangzhou|模板所属的地域 ID。您可以调用 [DescribeRegions](~~25609~~) 查看最新的阿里云地域列表。

 |
|Action|String|否|DeleteLaunchTemplateVersion|系统规定参数。取值：DeleteLaunchTemplateVersion

 |
|LaunchTemplateId|String|否|lt-bp1apo0bbbkuy0rj3b9X|需要删除的启动模板 ID。更多详情，请调用 [DescribeLaunchTemplates](~~73759~~)。

 |
|LaunchTemplateName|String|否|JoshuaWinPostPaid|启动模板名称。

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

https://ecs.aliyuncs.com/?Action=DeleteLaunchTemplateVersion
&DeleteVersion.1=2
&RegionId=cn-hangzhou
&LaunchTemplateId=lt-bp1apo0bbbkuy0rj3b9X
&LaunchTemplateName=JoshuaWinPostPaid
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DeleteLaunchTemplateVersionResponse>
  <RequestId>04F0F334-1335-436C-A1D7-6C044FExxxxx</RequestId>
</DeleteLaunchTemplateVersionResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"04F0F334-1335-436C-A1D7-6C044FExxxxx"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InvalidRegion.NotExist|%s|指定的Region不存在。|
|400|MissingParameter|%s|缺失必需参数。|
|400|InvalidParameter|%s|参数格式不正确。|
|403|InnerServiceFailed|%s|内部服务调用失败。|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Ecs)

