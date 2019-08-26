# ModifyHpcClusterAttribute {#doc_api_1022305 .reference}

修改一个 HPC 集群的描述信息。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=ModifyHpcClusterAttribute)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|HpcClusterId|String|是|hpc-hpcclusterid1|HPC 集群 ID。

 |
|RegionId|String|是|cn-hangzhou|地域 ID。您可以调用 [DescribeRegions](~~25609~~) 查看最新的阿里云地域列表。

 |
|Action|String|否|ModifyHpcClusterAttribute|系统规定参数。取值：ModifyHpcClusterAttribute

 |
|ClientToken|String|否|123e4567-e89b-12d3-a456-426655440000|保证请求幂等性。从您的客户端生成一个参数值，确保不同请求间该参数值唯一。**ClientToken** 只支持 ASCII 字符，且不能超过 64 个字符。更多详情，请参阅 [如何保证幂等性](~~25693~~)。

 |
|Description|String|否|FinanceDept|HPC 集群描述。长度为 2~256 个英文或中文字符，不能以 http:// 和 https:// 开头。默认值：空。

 |
|Name|String|否|FinanceJoshua|HPC 集群名称。长度为 2~128 个英文或中文字符。必须以大小字母或中文开头，不能以 http:// 和 https:// 开头。可以包含数字、半角冒号（:）、下划线（\_）或者连字符（-）。默认值：空。

 |
|OwnerAccount|String|否|EcsforCloud@Alibaba.com|RAM用户的账号登录名称。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

https://ecs.aliyuncs.com/?Action=ModifyHpcClusterAttribute
&HpcClusterId=hpc-hpcclusterid1
&RegionId=cn-hangzhou
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ModifyHpcClusterAttributeResponse>
  <RequestId>04F0F334-1335-436C-A1D7-6C044FE73368</RequestId>
</ModifyHpcClusterAttributeResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"04F0F334-1335-436C-A1D7-6C044FE73368"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|MissingParameter|The input parameter RegionId that is mandatory for processing this request is not supplied.|参数 RegionID 不得为空。|
|400|InvalidHpcClusterName.Malformed|Specified hpc cluster name is not valid.|指定的hpc集群名称不合法。|
|400|InvalidHpcClusterDescription.Malformed|The specified parameter Description is not valid.|指定的hpc集群描述不合法。|
|400|InvalidRegionId.NotFound|The specified parameter "RegionId" is not valid.|指定的 RegionId 不存在，请您检查此产品在该地域是否可用。|
|400|InvalidModifyInfo|Modify info is invalid, name/description must not null at the same time|参数不合法，hpc集群名称或者描述至少一个非空。|
|400|HPC\_CLUSTER\_MODIFY\_FAILED|Modify failed, possibly this hpc cluster does not exist|修改hpc集群失败，hpc集群不存在。|
|400|Invalid.Parameter|Invalid parameters|参数不合法。|
|400|HpcClusterNotExists|The specified hpc cluster does not exist|指定的hpc集群不存在。|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Ecs)

