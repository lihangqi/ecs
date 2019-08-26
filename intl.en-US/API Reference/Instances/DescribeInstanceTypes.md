# DescribeInstanceTypes {#doc_api_1161571 .reference}

Queries the instance type list provided by ECS.

## Description {#description .section}

**DescribeInstanceTypes** returns the same instance type list as the list of Pay-As-You-Go instances after an instance is created. For more information, see[Pay-As-You-Go](~~40653~~) and [Limits](~~25412~~).

For more information, see [Instance type families](~~25378~~).

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=DescribeInstanceTypes) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|Action|String|No|DescribeInstanceTypes| The operation that you want to perform. Set the value to **DescribeInstanceTypes**.

 |
|InstanceTypeFamily|String|No|ecs.t1| The instance type family. For more information, see [Instance type families](~~25378~~).

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|InstanceTypes| | | The returned instance type information. It is an array that consists of **InstanceTypeItemType** data.

 |
|└BaselineCredit|Integer|4| The \(combined\) benchmark vCPU computing performance of the burstable performance instance \(t5\).

 |
|└CpuCoreCount|Integer|8| The number of vCPUs.

 |
|└EniPrivateIpAddressQuantity|Integer|2| The number of private IP addresses allocated to the ENIs bound to the instance.

 |
|└EniQuantity|Integer|2| The maximum number of ENIs attached to the instance type.

 |
|└GPUAmount|Integer|2| The number of GPUs for the instance type.

 |
|└GPUSpec|String|NVIDIA V100| The category of GPUs for the instance type.

 |
|└InitialCredit|Integer|120| The initial credit value of the burstable performance instance \(t5\).

 |
|└InstanceBandwidthRx|Integer|2,000| The inbound bandwidth limit for the instance. Unit: Kbit/s.

 |
|└InstanceBandwidthTx|Integer|2,000| The outbound bandwidth limit for the instance. Unit: Kbit/s.

 |
|└InstanceFamilyLevel|String|EnterpriseLevel| The level of the instance type. Valid values:

 -   EntryLevel.
-   EnterpriseLevel.
-   CreditEntryLevel: This value is only valid for [burstable performance instances \(t5\)](~~59977~~).

 |
|└InstancePpsRx|Long|300| The inbound PPS limit for the instance.

 |
|└InstancePpsTx|Long|300| The outbound PPS limit for the instance.

 |
|└InstanceTypeFamily|String|ecs.g5| The instance type family.

 |
|└InstanceTypeId|String|ecs.g5.large| The ID of the instance type.

 |
|└LocalStorageAmount|Integer|1| The number of local disks attached to the instance.

 |
|└LocalStorageCapacity|Long|5000| The capacity of a local disk.

 |
|└LocalStorageCategory|String|ephemeral\_ssd| The category of the local disk attached to the instance.

 |
|└MemorySize|Float|1024| The capacity of the memory. Unit: GiB.

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The request ID.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=DescribeInstanceTypes
&InstanceTypeFamily=ecs.t1
&<Common request parameters>
```

Successful response examples

`XML` format

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

`JSON` format

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

## Error codes { .section}

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

