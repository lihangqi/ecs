# CreateDeploymentSet {#CreateDeploymentSet .reference}

在指定的地域内创建一个部署集。

## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：CreateDeploymentSet|
|RegionId|String|是|部署集所属地域ID。您可以调用[DescribeRegions](../cn.zh-CN/API 参考/地域/DescribeRegions.md#)查看最新的阿里云地域列表。|
|DeploymentStrategy|String|是|部署策略。可选值：`Availability``Availability`为高可用策略，部署集内所有ECS实例会在所在地域内严格分散在不同的物理服务器上。适用于需要将几台ECS实例相互隔离的应用架构，大幅降低服务不可用的几率。

|
|DeploymentSetName|String|否|部署集名称。长度为\[2, 128\]个英文或中文字符。必须以大小字母或中文开头，不能以http://和https://开头。可以包含数字、半角冒号（:）、下划线（\_）或者连字符（-）。|
|Description|String|否|部署集描述信息。长度为\[2, 256\]个英文或中文字符，不能以http://和https://开头。|
|OnUnableToRedeployFailedInstance|String|否|部署集内实例宕机迁移后，缺乏可供打散的实例库存的紧急处理方案。取值范围：-   CancelMembershipAndStart（默认）：将实例移出部署集，宕机迁移后即刻启动实例。
-   KeepStopped：保持异常状态等待补货充足后再启动实例。

|
|ClientToken|String|否|保证请求幂等性。从您的客户端生成一个参数值，确保不同请求间该参数值唯一。只支持ASCII字符，且不能超过64个字符。更多详情，请参阅[如何保证幂等性](../cn.zh-CN/API 参考/附录/如何保证幂等性.md#)。

|

## 返回参数 {#ResponseParameter .section}

|名称|类型|描述|
|:-|:-|:-|
|DeploymentSetId|String|部署集ID|

## 示例 { .section}

**请求示例**

```
https://ecs.aliyuncs.com/?Action=CreateDeploymentSet
&RegionId=cn-hangzhou
&DeploymentStrategy=Availability
&DeploymentSetName=AvailMySet
&<公共请求参数>
```

**返回示例**

**XML格式**

```
<CreateDeploymentSetResponse>
	<RequestId>04F0F334-1335-436C-A1D7-6C044FE73368</RequestId>
	<DeploymentSetId>ds-bp1frxuzdg87zh4pzqkcm</DeploymentSetId>
</CreateDeploymentSetResponse>
```

**JSON格式**

```
{
	"RequestId": "04F0F334-1335-436C-A1D7-6C044FE73368"
	"DeploymentSetId": "ds-bp1frxuzdg87zh4pzqkc"
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问[API错误中心](https://error-center.aliyun.com/status/product/Ecs)。

|错误代码|错误信息|HTTP状态码|说明|
|:---|:---|:------|:-|
|InvalidDescription.Malformed|The specified parameter “Description” is not valid.|400|指定的Description无效。|
|InvalidParameter.Strategy|The specified parameter Strategy is not valid|400|指定部署策略无效。|
|MissingParameter|The input parameter “RegionId” that is mandatory for processing this request is not supplied.|400|您需要指定RegionId参数。或者您暂时无法使用指定地域中的资源。|
|DEPLOYMENTSET.QUOTA\_FULL|The deploymentSet quota is full|403|您能创建的部署集数量已达上限。|
|InvalidRegionId.NotFound|The RegionId provided does not exist in our records.|404|指定的RegionId不存在。|

