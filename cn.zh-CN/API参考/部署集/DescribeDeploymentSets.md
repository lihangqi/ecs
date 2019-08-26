# DescribeDeploymentSets {#DescribeDeploymentSets .reference}

查询一个或多个部署集的属性列表。

## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：DescribeDeploymentSets|
|RegionId|String|是|部署集所属地域ID。您可以调用[DescribeRegions](../cn.zh-CN/API参考/地域/DescribeRegions.md#)查看最新的阿里云地域列表。|
|DeploymentSetIds|String|否|部署集ID列表。取值可以由多个部署集ID组成一个JSON数组，格式为\["ds-xxxxxxxxx", "ds-yyyyyyyyy", … "ds-zzzzzzzzz"\]，最多支持100个ID，ID之间用半角逗号（`,`）隔开。|
|DeploymentSetName|String|否|部署集名称。|
|Strategy|String|否|部署策略。取值：Availability默认值：空。

|
|PageNumber|Integer|否|部署集列表的页码。起始值：1默认值：1

|
|PageSize|Integer|否|分页查询时设置的每页行数，最大值：100默认值：10

|

## 返回参数 {#ResponseParameter .section}

|名称|类型|描述|
|:-|:-|:-|
|TotalCount|Integer|查询到的部署集总数。|
|PageNumber|Integer|部署集列表的页数。|
|PageSize|Integer|设置的每页行数。|
|DeploymentSetList|Array of [DeploymentSetType](#)|由DeploymentSet组成的数组格式，返回部署集详细信息。|

**数据类型DeploymentSetType** 

|名称|类型|描述|
|:-|:-|:-|
|DeploymentSetId|String|部署集ID。|
|DeploymentStrategy|String|部署策略。|
|DeploymentSetName|String|部署集名称。|
|Description|String|部署集描述。|
|InstanceIds|Array of InstanceId|部署集中所含的实例。|

## 示例 { .section}

**请求示例**

```
https://ecs.aliyuncs.com/?Action=DescribeDeploymentSets
&RegionId=cn-hangzhou
&DeploymentSetsIds=["ds-bp13v7bjnj9gisnlo1"]
&<公共请求参数>
```

**返回示例**

**XML格式**

```
<DescribeDeploymentSetsResponse>
	<PageSize>10</PageSize>
	<TotalCount>1</TotalCount>
	<PageNumber>1</PageNumber>
	<RequestId>1CB9A584-9E43-408D-B5A8-DB42CDECE03B</RequestId>
	<DeploymentSets>
		<DeploymentSet>
			<DeploymentSetDescription>default</DeploymentSetDescription>
			<DeploymentSetId>ds-bp13v7bjnj9gisnlo1ow</DeploymentSetId>
			<DeploymentStrategy>Availability</DeploymentStrategy>
			<DeploymentSetName>test default</DeploymentSetName>
			<InstanceIds>
				<InstanceId>i-sdfkjsdfk</InstanceId>
				<InstanceId>i-kiiwsch</InstanceId>
			</InstanceIds>
		</DeploymentSet>
	</DeploymentSets>
</DescribeDeploymentSetsResponse>
```

**JSON格式**

```
{
	"PageSize": 10,
	"TotalCount": 1,
	"PageNumber": 1,
	"RequestId": "1CB9A584-9E43-408D-B5A8-DB42CDECE03B",
	"DeploymentSets":
		{
			"DeploymentSet":
				[
					{
						"DeploymentSetDescription": "default",
						"DeploymentSetId": "ds-bp13v7bjnj9gisnlo1ow",
						"DeploymentStrategy": "Availability",
						"DeploymentSetName": "test default",
						"InstanceIds":
							{
								"InstanceId": ["i-sdfkjsdfk", "i-kiiwsch"]
							}
					}
				]
		}
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问[API错误中心](https://error-center.aliyun.com/status/product/Ecs)。

|错误代码|错误信息|HTTP状态码|说明|
|:---|:---|:------|:-|
|InvalidDescription.Malformed|The specified parameter “Description” is not valid.|400|指定的Description无效。|
|InvalidParameter.Strategy|The specified parameter Strategy is not valid|400|指定部署策略无效。|
|MissingParameter|The input parameter “RegionId” that is mandatory for processing this request is not supplied.|400|您需要指定RegionId参数。或者您暂时无法使用指定地域中的资源。|
|InvalidRegionId.NotFound|The RegionId provided does not exist in our records.|404|指定的RegionId不存在。|

