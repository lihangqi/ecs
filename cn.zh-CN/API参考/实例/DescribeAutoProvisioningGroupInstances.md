# DescribeAutoProvisioningGroupInstances {#doc_api_Ecs_DescribeAutoProvisioningGroupInstances .reference}

调用DescribeAutoProvisioningGroupInstances查询指定弹性供应组下的实例。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=DescribeAutoProvisioningGroupInstances)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
| AutoProvisioningGroupId |String|是|apg-uf6jel2bbl62wh13\*\*\*\*| 弹性供应组的ID。

 |
| RegionId |String|是|cn-hangzhou| 弹性供应组所在地域的ID。

 |
| Action |String|否|DescribeAutoProvisioningGroupInstances| 系统规定参数，取值： **DescribeAutoProvisioningGroupInstances** 。

 |
| PageNumber |Integer|否|1| 实例状态列表的页码。起始值： **1** ，默认值： **1** 。

 |
| PageSize |Integer|否|10| 分页查询时设置的每页行数。最大值： **100** ，默认值： **10** 。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|Instances| | | 弹性供应组下所有实例的信息。

 |
|└CPU|Integer|2| 实例的vCPU核数。

 |
|└CreationTime|String|2017-12-10T04:04Z| 实例创建时间。

 |
|└InstanceId|String|i-instanc\*\*\*\*| 实例ID。

 |
|└InstanceType|String|ecs.g5.large| 实例规格。

 |
|└IoOptimized|Boolean|true| 是否为I/O优化型实例。

 |
|└IsSpot|Boolean|true| 是否为抢占式实例。

 |
|└Memory|Integer|1024| 内存大小，单位MiB。

 |
|└NetworkType|String|vpc| 实例的网络类型，取值范围：

 -    **vpc** ：专有网络。
-    **classic** ：经典网络。

 |
|└OsType|String|linux| 实例的操作系统类型，取值范围：

 -    **windows** ：操作系统类型为Windows。
-    **linux** ：操作系统类型为Linux。

 |
|└RegionId|String|cn-hangzhou| 实例所属地域的ID。

 |
|└Status|String|Running| 实例状态。

 |
|└ZoneId|String|cn-hangzhou-g| 实例所属可用区。

 |
|PageNumber|Integer|1| 实例状态列表的页码。

 |
|PageSize|Integer|10| 分页查询时设置的每页行数。

 |
|RequestId|String|B48A12CD-1295-4A38-A8F0-0E92C937\*\*\*\*| 请求ID。

 |
|TotalCount|Integer|10| 查询到的弹性供应组内实例的个数。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://ecs.aliyuncs.com/?Action=DescribeAutoProvisioningGroupInstances
$AutoProvisioningGroupId=apg-uf6jel2bbl62wh13****
&<公共请求参数>

```

正常返回示例

 `XML` 格式

``` {#xml_return_success_demo}
<DescribeAutoProvisioningGroupInstancesResponse>
  <PageNumber>1</PageNumber>
  <TotalCount>100</TotalCount>
  <PageSize>2</PageSize>
  <RequestId>A43735F7-30BD-4D89-AB8A-030EB24B****</RequestId>
  <Instances>
    <Instance>
      <CreationTime>2019-06-17T15:25Z</CreationTime>
      <IoOptimized>true</IoOptimized>
      <OsType>linux</OsType>
      <NetworkType>vpc</NetworkType>
      <Status>Running</Status>
      <Memory>8192</Memory>
      <RegionId>cn-shanghai</RegionId>
      <InstanceId>i-uf64neea72piruk0****</InstanceId>
      <CPU>2</CPU>
      <ZoneId>cn-shanghai-a</ZoneId>
      <InstanceType>ecs.g5.large</InstanceType>
    </Instance>
    <Instance>
      <CreationTime>2019-06-17T15:25Z</CreationTime>
      <IoOptimized>true</IoOptimized>
      <OsType>linux</OsType>
      <NetworkType>vpc</NetworkType>
      <Status>Running</Status>
      <Memory>8192</Memory>
      <RegionId>cn-shanghai</RegionId>
      <InstanceId>i-uf64neea72piruk0****</InstanceId>
      <CPU>2</CPU>
      <ZoneId>cn-shanghai-a</ZoneId>
      <InstanceType>ecs.g5.large</InstanceType>
    </Instance>
  </Instances>
</DescribeAutoProvisioningGroupInstancesResponse>

```

 `JSON` 格式

``` {#json_return_success_demo}
{
	"PageNumber":1,
	"TotalCount":100,
	"PageSize":2,
	"RequestId":"A43735F7-30BD-4D89-AB8A-030EB24B****",
	"Instances":{
		"Instance":[
			{
				"IoOptimized":true,
				"CreationTime":"2019-06-17T15:25Z",
				"Status":"Running",
				"NetworkType":"vpc",
				"OsType":"linux",
				"Memory":8192,
				"InstanceId":"i-uf64neea72piruk0****",
				"RegionId":"cn-shanghai",
				"CPU":2,
				"ZoneId":"cn-shanghai-a",
				"InstanceType":"ecs.g5.large"
			},
			{
				"IoOptimized":true,
				"CreationTime":"2019-06-17T15:25Z",
				"Status":"Running",
				"NetworkType":"vpc",
				"OsType":"linux",
				"Memory":8192,
				"InstanceId":"i-uf64neea72piruk0****",
				"RegionId":"cn-shanghai",
				"CPU":2,
				"ZoneId":"cn-shanghai-a",
				"InstanceType":"ecs.g5.large"
			}
		]
	}
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|403|Forbidden.RAM|User not authorized to operate on the specified resource, or this API doesn't support RAM.|子账号鉴权不通过。|
|400|MissingParamter.RegionId|The regionId should not be null.|参数 RegionId 不得为空。|

 [查看本产品错误码](https://error-center.aliyun.com/status/product/Ecs) 

