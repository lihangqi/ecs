# DescribeImageSupportInstanceTypes {#doc_api_Ecs_DescribeImageSupportInstanceTypes .reference}

查询指定镜像支持的实例规格。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=DescribeImageSupportInstanceTypes)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|RegionId|String|是|cn-hangzhou|实例所属的地域 ID。您可以调用 [DescribeRegions](~~25609~~) 查看最新的阿里云地域列表。

 |
|Action|String|否|DescribeImageSupportInstanceTypes|系统规定参数。取值：DescribeImageSupportInstanceTypes

 |
|ActionType|String|否|\*|实例规格需要使用到的场景。取值范围：

 -   CreateEcs（默认）：创建实例
-   Upgrade：升级实例规格
-   Downgrade：降级实例规格
-   RenewDowngrade：续费降配

 |
|Filter.N.Key|String|否|CreationStartTime|指定过滤条件 Key。

 |
|Filter.N.Value|String|否|2017-12-05T22:40:00Z|指定过滤条件 Value。

 |
|ImageId|String|否|m-imageid1|镜像 ID。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|ImageId|String|m-imageid2|查询的镜像 ID。

 |
|InstanceTypes| | |由 InstanceTypeItemType 组成的实例规格集合。

 |
|└CpuCoreCount|Integer|1|实例规格的 vCPU 内核数目。

 |
|└InstanceTypeFamily|String|ecs.t1|实例规格族。

 |
|└InstanceTypeId|String|ecs.t1.xsmall|镜像支持的实例规格 ID。

 |
|└MemorySize|Float|1024|实例规格的内存大小，单位 GiB。

 |
|RegionId|String|cn-hangzhou|镜像所属地域 ID。

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

https://ecs.aliyuncs.com/?Action=DescribeImageSupportInstanceTypes
&RegionId=cn-hangzhou
&ImageId=m-imageid1
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeImageSupportInstanceTypesResponse>
  <RequestId>CF661E2D-4AFE-4BCD-959A-A65E14416B44</RequestId>
  <RegionId>cn-hangzhou</RegionId>
  <ImageId>ubuntu_16_0402_64_20G_alibase_20180409.vhd</ImageId>
  <InstanceTypes>
    <InstanceType>
      <InstanceTypeId>ecs.t1.xsmall</InstanceTypeId>
      <CpuCoreCount>1</CpuCoreCount>
      <MemorySize>0.5</MemorySize>
      <InstanceTypeFamily>ecs.t1</InstanceTypeFamily>
    </InstanceType>
    <InstanceType>
      <InstanceTypeId>ecs.t1.small</InstanceTypeId>
      <CpuCoreCount>1</CpuCoreCount>
      <MemorySize>1</MemorySize>
      <InstanceTypeFamily>ecs.t1</InstanceTypeFamily>
    </InstanceType>
  </InstanceTypes>
</DescribeImageSupportInstanceTypesResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"ImageId":"ubuntu_16_0402_64_20G_alibase_20180409.vhd",
	"InstanceTypes":{
		"InstanceType":[
			{
				"CpuCoreCount":1,
				"InstanceTypeFamily":"ecs.t1",
				"InstanceTypeId":"ecs.t1.xsmall",
				"MemorySize":0.5
			},
			{
				"CpuCoreCount":1,
				"InstanceTypeFamily":"ecs.t1",
				"InstanceTypeId":"ecs.t1.small",
				"MemorySize":1
			}
		]
	},
	"RegionId":"cn-hangzhou",
	"RequestId":"CF661E2D-4AFE-4BCD-959A-A65E14416B44"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InvalidParamter|Invalid Parameter|指定的参数不合法。|
|404|InvalidUsage|The specifed Usage is not valid|指定有引用关系的资源类型（image、disk、image\_disk、none）不合法。|
|400|InvalidInstanceType.ValueNotSupported|The specified InstanceType does not exist or beyond the permitted range.|指定的实例规格不支持。|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Ecs)

