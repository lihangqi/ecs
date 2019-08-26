# DeleteDeploymentSet {#doc_api_Ecs_DeleteDeploymentSet .reference}

调用DeleteDeploymentSet删除一个部署集。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=DeleteDeploymentSet)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|DeploymentSetId|String|是|ds-deploymentsetid1|部署集ID。如果部署集中仍有实例存在，则无法删除。

 |
|RegionId|String|是|cn-hangzhou|部署集所属地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。

 |
|Action|String|否|DeleteDeploymentSet|系统规定参数，取值：DeleteDeploymentSet

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=DeleteDeploymentSet
&RegionId=cn-hangzhou
&DeploymentSetId=ds-bp1frxuzdg87zh4pz***
&<公共请求参数>
```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DeleteDeploymentSetResponse>
  <RequestId>04F0F334-1335-436C-A1D7-6C044FE73368</RequestId>
</DeleteDeploymentSetResponse>

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
|400|MissingParameter|The input parameter "DeploymentSetId" that is mandatory for processing this request is not supplied.|参数 DeploymentSetId 不得为空。|
|403|DependencyViolation.NotEmpty|There are still instance\(s\) in the specified DeploymentSetId.|指定的部署集 ID 内仍有实例。|
|403|DependencyViolation.ReferByHPC|The specified deployment set is still referred by an HPC cluster.|指定的部署集与其他HPC集群有关联。|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

