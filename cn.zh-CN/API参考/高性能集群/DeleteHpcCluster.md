# DeleteHpcCluster {#doc_api_Ecs_DeleteHpcCluster .reference}

调用DeleteHpcCluster删除一个HPC集群。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=DeleteHpcCluster&type=RPC&version=2014-05-26)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|HpcClusterId|String|是|hpc-cluster1|HPC集群ID。

 |
|RegionId|String|是|cn-hangzhou|HPC集群所属的地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。

 |
|Action|String|否|DeleteHpcCluster|系统规定参数。取值：DeleteHpcCluster

 |
|ClientToken|String|否|123e4567-e89b-12d3-a456-426655440000|保证请求幂等性。从您的客户端生成一个参数值，确保不同请求间该参数值唯一。**ClientToken**只支持ASCII字符，且不能超过64个字符。更多详情，请参见[如何保证幂等性](~~25693~~)。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=DeleteHpcCluster
&RegionId=cn-hangzhou
&HpcClusterId=hpc-cluster1
&<公共请求参数>
```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DeleteHpcClusterResponse>
      <RequestId>04F0F334-1335-436C-A1D7-6C044FE73368</RequestId>
</DeleteHpcClusterResponse>
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
|400|MissingParameter.RegionId|The input parameter RegionId that is mandatory for processing this request is not supplied.|缺少必填参数RegionId。|
|404|InvalidRegionId.NotFound|The specified parameter "RegionId" is not valid.|指定的 RegionId 不存在，请您检查此产品在该地域是否可用。|
|400|MissingParameter.HpcClusterId|The input parameter HpcClusterId that is mandatory for processing this request is not supplied.|缺少必填参数hpcClusterId。|
|400|Invalid.Parameter|Invalid parameters.|参数不合法。|
|400|NotExists.HpcCluster|The specified hpc cluster does not exist.|hpc集群不存在。|
|400|NotEmpty.HpcCluster|The specified hpc cluster is not empty, still contains instances.|hpc集群非空，包含实例，无法删除。|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

