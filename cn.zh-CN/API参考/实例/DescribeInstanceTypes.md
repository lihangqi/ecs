# DescribeInstanceTypes {#doc_api_Ecs_DescribeInstanceTypes .reference}

查询云服务器 ECS 提供的实例规格资源。

## 接口说明 {#description .section}

DescribeInstanceTypes仅查询所有[ECS实例规格](~~25378~~)的详情。如果您需要查询具体地域下可购买的实例规格，请使用 [DescribeAvailableResource](~~66186~~)。

如果您需要使用更多实例规格资源，可以 [提交工单](https://selfservice.console.aliyun.com/ticket/createIndex.htm) 联系我们。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=DescribeInstanceTypes)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|否|DescribeInstanceTypes|接口名称。取值：**DescribeInstanceTypes**

 |
|InstanceTypeFamily|String|否|ecs.t1|实例规格所属的规格族。更多详情，请参阅 [实例规格族](~~25378~~)。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|InstanceTypes| | |由实例规格项 **InstanceTypeItemType** 组成的集合。

 |
|└BaselineCredit|Integer|4|突发性能实例基准 vCPU 计算性能（多核和）。

 |
|└CpuCoreCount|Integer|8|vCPU 内核数目。

 |
|└EniPrivateIpAddressQuantity|Integer|2|实例绑定的弹性网卡中分配的私有IP地址数量。

 |
|└EniQuantity|Integer|2|实例规格支持网卡数量。

 |
|└GPUAmount|Integer|2|实例规格附带 GPU 数量。

 |
|└GPUSpec|String|NVIDIA V100|实例规格附带 GPU 类型。

 |
|└InitialCredit|Integer|120|突发性能实例的初始积分值。

 |
|└InstanceBandwidthRx|Integer|2000|内网入方向带宽限制，单位为 kbps。

 |
|└InstanceBandwidthTx|Integer|2000|内网出方向带宽限制，单位为 kbps。

 |
|└InstanceFamilyLevel|String|EnterpriseLevel|实例规格级别。可能值：

 -   EntryLevel：入门级
-   EnterpriseLevel：企业级
-   CreditEntryLevel：积分入门级，特指 [突发性能实例](~~59977~~)

 |
|└InstancePpsRx|Long|300|内网入方向PPS限制。

 |
|└InstancePpsTx|Long|300|内网出方向PPS限制。

 |
|└InstanceTypeFamily|String|ecs.g5|实例规格族。

 |
|└InstanceTypeId|String|ecs.g5.large|实例规格 ID。

 |
|└LocalStorageAmount|Integer|1|实例挂载的本地存储的数量。

 |
|└LocalStorageCapacity|Long|5000|实例挂载的本地存储的单盘容量。

 |
|└LocalStorageCategory|String|ephemeral\_ssd|实例挂载的本地存储的类型。

 |
|└MemorySize|Float|1024|内存大小，单位 GiB。

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

https://ecs.aliyuncs.com/?Action=DescribeInstanceTypes
&InstanceTypeFamily=ecs.t1
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeInstanceTypesResponse>
  <InstanceTypes>
    <InstanceType>
      <CpuCoreCount>1</CpuCoreCount>
      <InstanceTypeFamily>ecs.t1</InstanceTypeFamily>
      <EniQuantity>1</EniQuantity>
      <InstanceTypeId>ecs.t1.xsmall</InstanceTypeId>
      <InstanceFamilyLevel>EntryLevel</InstanceFamilyLevel>
      <GPUSpec/>
      <MemorySize>0.5</MemorySize>
      <GPUAmount>0</GPUAmount>
      <LocalStorageCategory/>
    </InstanceType>
    <InstanceType>
      <CpuCoreCount>1</CpuCoreCount>
      <InstanceTypeFamily>ecs.t1</InstanceTypeFamily>
      <EniQuantity>1</EniQuantity>
      <InstanceTypeId>ecs.t1.small</InstanceTypeId>
      <InstanceFamilyLevel>EntryLevel</InstanceFamilyLevel>
      <GPUSpec/>
      <MemorySize>1</MemorySize>
      <GPUAmount>0</GPUAmount>
      <LocalStorageCategory/>
    </InstanceType>
  </InstanceTypes>
  <RequestId>01D5A075-FB83-4DDC-9F00-24A17AB386F6</RequestId>
</DescribeInstanceTypesResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"InstanceTypes":{
		"InstanceType":[
			{
				"CpuCoreCount":1,
				"InstanceTypeFamily":"ecs.t1",
				"EniQuantity":1,
				"InstanceTypeId":"ecs.t1.xsmall",
				"GPUSpec":"",
				"InstanceFamilyLevel":"EntryLevel",
				"MemorySize":0.5,
				"GPUAmount":0,
				"LocalStorageCategory":""
			},
			{
				"CpuCoreCount":1,
				"InstanceTypeFamily":"ecs.t1",
				"EniQuantity":1,
				"InstanceTypeId":"ecs.t1.small",
				"GPUSpec":"",
				"InstanceFamilyLevel":"EntryLevel",
				"MemorySize":1,
				"GPUAmount":0,
				"LocalStorageCategory":""
			}
		]
	},
	"RequestId":"01D5A075-FB83-4DDC-9F00-24A17AB386F6"
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/Ecs)

