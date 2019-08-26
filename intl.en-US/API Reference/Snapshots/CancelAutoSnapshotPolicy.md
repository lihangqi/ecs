# CancelAutoSnapshotPolicy {#CancelAutoSnapshotPolicy .reference}

Cancels the automatic snapshot policy for one or more disks.

## Request parameters {#RequestParameter .section}

|Name|Type|Required|Description|
|:---|:---|:-------|:----------|
|Action|String|Yes|The name of this interface. Value: CancelAutoSnapshotPolicy.|
|RegionId|String|Yes|The region ID of the automatic snapshot policy and the disks. For more information, call [DescribeRegions](intl.en-US/API Reference/Regions/DescribeRegions.md#) to obtain the latest region list.|
|DiskIds|String| Yes|The disk ID. When you want to cancel the automatic snapshot policy for multiple disks, you can set the DiskIds to a JSON array in the format of \["d-xxxxxxxxx", "d-yyyyyyyyy", … "d-zzzzzzzzz"\], and the IDs are separated by half-width commas \(`,`\).|

## Response parameters {#section_a3j_1yz_xdb .section}

All are common response parameters. For more information, see [Common parameters](intl.en-US/API Reference/Call methods/Common parameters.md#commonResponseParameters).

## Examples { .section}

**Request example** 

```
https://ecs.aliyuncs.com/?Action=CancelAutoSnapshotPolicy
&RegionId=cn-hangzhou
&DiskIds=["d-233e6ylv0", "d-23vbpbi03", "d-23vasz3ds"]
&<Common Request Parameters>
```

**Response example** 

**XML format**

```
<CancelAutoSnapshotPolicyResponse>
    <RequestId>F3CD6886-D8D0-4FEE-B93E-1B73239673DE</RequestId>
</CancelAutoSnapshotPolicyResponse>
```

 **JSON format** 

```
{
    "RequestId":"F3CD6886-D8D0-4FEE-B93E-1B73239673DE"
}
```

## Error codes {#ErrorCode .section}

Error codes specific to this interface are as follows. For more error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

|Error code|Error message|HTTP status code|Description|
|:---------|:------------|:---------------|:----------|
|ParameterInvalid|The specified DiskIds are invalid.|404|The specified `DiskIds` are invalid.|
|ParameterInvalid|The specified RegionId parameter is invalid.|404|The specified `RegionId` is invalid.|

