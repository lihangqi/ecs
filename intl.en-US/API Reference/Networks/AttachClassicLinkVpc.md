# AttachClassicLinkVpc {#AttachClassicLinkVpc .reference}

Links a classic network instance to the [Virtual Private Cloud \(VPC\)](../../../../reseller.en-US/Product Introduction/What is VPC?.md#), which allows the classic network instance communicating with the resources that are in the intranet of a VPC.  For more information, see *VPC*topic [ClassicLink overview](../../../../reseller.en-US/User Guide/ClassicLink/ClassicLink overview.md#). 

## Description {#section_brt_tjn_ydb .section}

When you call this interface, consider the following:

-   The instance must be in the **Running** \(`Running`\) or **Stopped** \(`Stopped`\) status.

-   The ClassiscLink service must be enabled for the specified VPC. For more information, see VPC topic [Build ClassicLink connection](../../../../reseller.en-US/User Guide/ClassicLink/Build a ClassicLink connection.md#).

-   The classic network instance and the VPC must be in the same Alibaba Cloud region.


## Request parameters {#RequestParameter .section}

|Name|Type|Required|Description|
|:---|:---|:-------|:----------|
|Action|String|Yes|The name of this interface.  Value: AttachClassicLinkVpc.|
|RegionId|String|Yes.| Region ID of the instance.  For more information, see [DescribeRegions](reseller.en-US/API Reference/Regions/DescribeRegions.md#)  to obtain the latest region list.|
|InstanceId|String|Yes.| ID of the classic network instance.  You can call [DescribeInstances](reseller.en-US/API Reference/Instances/DescribeInstances.md#) to obtain all of your instance IDs.|
|VpcId|String|Yes.| ID of the ClassicLink enabled VPC.  You can call DescribeVpcs to obtain all of your VPC IDs.|

## Response parameters {#section_f54_lk5_xdb .section}

All are common response parameters.  For more information, see[Common parameter](reseller.en-US/API Reference/Getting started/Common parameters.md#commonResponseParameters).

## Examples { .section}

**Request example** 

```
https://ecs.aliyuncs.com/?Action=AttachClassicLinkVpc
&RegionId=cn-hangzhou
&InstanceId=i-test
&VpcId=vpc-test
&<Common Request Parameters>
```

**Response example** 

**XML format**

```
<AttachClassicLinkVpcResponse>
    <RequestId>C0003E8B-B930-4F59-ADC0-0E209A9012A8</RequestId>
</AttachClassicLinkVpcResponse>
```

 **JSON format** 

```

    "RequestId": "C0003E8B-B930-4F59-ADC0-0E209A9012A8"

```

## Error codes {#ErrorCode .section}

|Error code|Error information|HTTP status code|Description|
|:---------|:----------------|:---------------|:----------|
|Abs.InvalidInstanceId.MalFormed|The specified instance has already been linked to another VPC.|400|The specified instance is already linked to another VPC.|
|InvalidInstanceId.MalFormed|The specified instance is not a classic network type instance.|400|The network type of the specified instance is not a classic network.|
|InvalidRegionId.Malformed|The specified RegionId is invalid.|400|The specified `RegionId` does not exist or you are not authorized to access the specified region.|
|InvalidVpcId.Malformed|The specified VpcId is invalid.|400|The specified `VpcId` is invalid.|
|InvalidInstanceId.NotBelong|The user does not own the specified instance.|403|The specified instance does not belong to you.|
|InvalidStatus.InstanceLocked|The specified instance is in another processing list.|403|The specified instance is processing another task.|
|InvalidStatus.InstanceStatus|Only the Running or Stopped InstanceStatus is allowed.|403|The specified instance must be in the **Running** \(`Running`\) or **Stopped** \(`Stopped`\) status.|
|OperationDenied|The specified VPC are unable to attach ClassicLink.|403|The specified VPC cannot enable ClassicLink.|
|QuotaExceeded|The maximum number of links in the specified VPC exceeds.|403|The number of available links for the current VPC has reached the upper limit, up to 1000 classic network type instances are allowed to connect to the same VPC.|
|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|404|The specified `InstanceId` does not exist.|

