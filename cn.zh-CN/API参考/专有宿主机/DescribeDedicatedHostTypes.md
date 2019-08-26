# DescribeDedicatedHostTypes {#DescribeDedicatedHostTypes .reference}

查询指定地域下支持的专有宿主机规格详细参数，或者查询专有宿主机支持的 ECS 实例规格族。

## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：DescribeDedicatedHostTypes|
|RegionId|String|是|地域 ID。您可以调用[DescribeRegions](../cn.zh-CN/API参考/地域/DescribeRegions.md#)查看最新的阿里云地域列表。|
|DedicatedHostType|String|否|专有宿主机规格。更多详情，请参阅 [宿主机规格](../../../../../../cn.zh-CN/产品简介/宿主机规格.md#)。|
|SupportedInstanceTypeFamily|String|否|专有宿主机规格支持的 ECS 实例规格族。|

## 返回参数 {#ResponseParameter .section}

|名称|类型|描述|
|:-|:-|:-|
|DedicatedHostTypes|Array of [DedicatedHostType](#)|返回专有宿主机规格的信息。|

**DedicatedHostType**

|名称|类型|描述|
|:-|:-|:-|
|DedicatedHostType|String|专有宿主机类型。如果您需要使用更多专有宿主机规格，可以 [提交工单](https://selfservice.console.aliyun.com/ticket/createIndex.htm) 联系阿里云。|
|SupportedInstanceTypeFamilies|Array of [SupportedInstanceTypeFamilySetType](#)|专有宿主机规格支持的 ECS 实例的规格族。|
|Sockets|Integer|物理处理器（CPU）的数量。|
|Cores|Integer|单个物理 CPU 的核数。|
|TotalVcpus|Integer|虚拟 CPU 总核数。|
|MemorySize|Float|内存容量，单位：GiB。|
|LocalStorageCapacity|Long|一块本地盘容量，单位：GiB。|
|LocalStorageAmount|Integer|专有宿主机上的本地盘块数。|
|LocalStorageCategory|String|本地盘类型。|

**SupportedInstanceTypeFamilySetType**

|名称|类型|描述|
|:-|:-|:-|
|SupportedInstanceTypeFamily|String|专有宿主机规格支持的 ECS 实例规格族。|

## 示例 {#Samples .section}

**请求示例**

```
https://ecs.aliyuncs.com/?Action=DescribeDedicatedHostTypes
&RegionId=cn-hangzhou
&<公共请求参数>
```

**返回示例**

**XML 格式**

```
<DescribeDedicatedHostTypesResponse>
  <DedicatedHostTypes>
    <DedicatedHostType>
      <LocalStorageAmount>0</LocalStorageAmount>
      <Sockets>2</Sockets>
      <DedicatedHostType>ddh.sn1ne</DedicatedHostType>
      <LocalStorageCapacity>0</LocalStorageCapacity>
      <SupportedInstanceTypeFamilies>
        <SupportedInstanceTypeFamily>ecs.sn1ne</SupportedInstanceTypeFamily>
      </SupportedInstanceTypeFamilies>
      <MemorySize>112.0</MemorySize>
      <Cores>32</Cores>
      <TotalVcpus>56</TotalVcpus>
      <LocalStorageCategory/>
    </DedicatedHostType>
    <DedicatedHostType>
      <LocalStorageAmount>0</LocalStorageAmount>
      <Sockets>2</Sockets>
      <DedicatedHostType>ddh.sn2ne</DedicatedHostType>
      <LocalStorageCapacity>0</LocalStorageCapacity>
      <SupportedInstanceTypeFamilies>
        <SupportedInstanceTypeFamily>ecs.sn2ne</SupportedInstanceTypeFamily>
      </SupportedInstanceTypeFamilies>
      <MemorySize>224.0</MemorySize>
      <Cores>32</Cores>
      <TotalVcpus>56</TotalVcpus>
      <LocalStorageCategory/>
    </DedicatedHostType>
  </DedicatedHostTypes>
  <RequestId>5FE5FF06-3A33-4658-8495-6445FC54E327</RequestId>
</DescribeDedicatedHostTypesResponse>
```

**JSON 格式**

```
{
    "DedicatedHostTypes":{
        "DedicatedHostType":[
            {
                "LocalStorageAmount":0,
                "Sockets":2,
                "DedicatedHostType":"ddh.sn1ne",
                "LocalStorageCapacity":0,
                "SupportedInstanceTypeFamilies":{
                    "SupportedInstanceTypeFamily":[
                        "ecs.sn1ne"
                    ]
                },
                "MemorySize":112,
                "Cores":32,
                "TotalVcpus":56,
                "LocalStorageCategory":""
            },
            {
                "LocalStorageAmount":0,
                "Sockets":2,
                "DedicatedHostType":"dh.c60m83.n1",
                "LocalStorageCapacity":0,
                "SupportedInstanceTypeFamilies":{
                    "SupportedInstanceTypeFamily":[
                        "ecs.n1"
                    ]
                },
                "MemorySize":84,
                "Cores":32,
                "TotalVcpus":40,
                "LocalStorageCategory":""
            }
        ]
    },
    "RequestId":"9A0FE8A2-720C-45AE-B2D9-813060FCBBF5"
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问[API错误中心](https://error-center.aliyun.com/status/product/Ecs)。

|错误代码|错误信息|HTTP 状态码|说明|
|:---|:---|:-------|:-|
|InternalError|The request processing has failed due to some unknown error,exception or failure.|500|内部错误。|

