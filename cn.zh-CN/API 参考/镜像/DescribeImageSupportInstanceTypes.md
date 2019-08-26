# DescribeImageSupportInstanceTypes {#DescribeImageSupportInstanceTypes .reference}

查询指定镜像支持的实例规格。

## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：DescribeImageSupportInstanceTypes|
|RegionId|String|是|实例所属的地域 ID。您可以调用[DescribeRegions](../cn.zh-CN/API 参考/地域/DescribeRegions.md#)查看最新的阿里云地域列表。|
|ImageId|String|否|镜像 ID。|

## 返回参数 {#ResponseParameter .section}

|名称|类型|描述|
|:-|:-|:-|
|RegionId|String|镜像所属地域 ID。|
|ImageId|String|查询的镜像 ID。|
|InstanceTypes|[InstanceTypeItemType](cn.zh-CN/API 参考/数据类型/InstanceTypeItemType.md#)|由 `InstanceTypeItemType` 组成的实例规格集合，返回以下信息：-   InstanceTypeId：镜像支持的实例规格 ID。

-   CpuCoreCount：实例规格的 vCPU 内核数目。

-   MemorySize：实例规格的内存大小，单位 GiB。

-   InstanceTypeFamily：实例规格族。


|

## 示例 {#Samples .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=DescribeImageSupportInstanceTypes
&RegionId=cn-hangzhou
&ImageId=ubuntu_16_0402_64_20G_alibase_20180409.vhd
&<公共请求参数>
```

**返回示例**

**XML 格式**

```
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

**JSON 格式**

```
{
    "RequestId": "CF661E2D-4AFE-4BCD-959A-A65E14416B44",
    "RegionId": "cn-hangzhou",
    "ImageId": "ubuntu_16_0402_64_20G_alibase_20180409.vhd",
    "InstanceTypes": {
        "InstanceType": [{
            "InstanceTypeId": "ecs.t1.xsmall",
            "CpuCoreCount": 1,
            "MemorySize": 0.5,
            "InstanceTypeFamily": "ecs.t1"
        },
        {
            "InstanceTypeId": "ecs.t1.small",
            "CpuCoreCount": 1,
            "MemorySize": 1,
            "InstanceTypeFamily": "ecs.t1"
        }]
    }
}
```

## 错误码 {#ErrorCode .section}

全是公共错误码。更多错误码，请访问[API错误中心](https://error-center.aliyun.com/status/product/Ecs)。

