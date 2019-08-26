# ApplyAutoSnapshotPolicy {#ApplyAutoSnapshotPolicy .reference}

Applies automatic snapshot policies to one or more disks. If an automatic snapshot policy has been applied to a disk, ApplyAutoSnapshotPolicy can change the automatic snapshot policy for the specified disks.

## Description  {#section_idr_vwz_xdb .section}

When you call this interface, consider the following: 

-   One disk can be applied to only one automatic snapshot policy.

-   You can apply an automatic snapshot policy to multiple disks.

-   A short queuing waiting time exists if many automatic snapshot tasks at a certain time point exist. Consequently, the automatic snapshot tasks scheduled at the same time cannot be carried out simultaneously.


## Request parameters  {#RequestParameter .section}

|Name |Type |Required |Description |
|:----|:----|:--------|:-----------|
|Action |String |Yes |The name of this interface. Value: ApplyAutoSnapshotPolicy.|
|RegionId |String |Yes|The region ID of the automatic snapshot policy and the disks. For more information, call [DescribeRegions](reseller.en-US/API Reference/Regions/DescribeRegions.md#) to obtain the latest region list.|
|Autosnapshotpolicyid|String |Yes|The ID of the automatic snapshot policy. You can call DescribeAutoSnapshotPolicyEx to obtain all of your automatic snapshot policy IDs.|
|DiskIds|String |Yes|The disk ID. When you want to apply the automatic snapshot policy to multiple disks, you can set the DiskIds to an array.  The format is a JSON array of \["d-xxxxxxxxx", "d-yyyyyyyyy", … "d-zzzzzzzzz"\]  and the IDs are separated by commas \(,\).|

## Response parameters  {#section_odr_vwz_xdb .section}

All are common response parameters. For more information, see [Common parameters](reseller.en-US/API Reference/Getting started/Common parameters.md#commonResponseParameters).

## Examples  { .section}

**Request example ** 

```
https://ecs.aliyuncs.com/?Action=ApplyAutoSnapshotPolicy
&RegionId=cn-hangzhou
&AutoSnapshotPolicyId=p-233e6ylv0
&DiskIds=["d-233e6ylv0", "d-23vbpbi03", "d-23vasz3ds"]
&<Common Request Parameters>
```

**Response example ** 

**XML format **

```
<ApplyAutoSnapshotPolicyResponse>
    <RequestId>F3CD6886-D8D0-4FEE-B93E-1B73239673DE</RequestId>
</ApplyAutoSnapshotPolicyResponse>
```

 **JSON format ** 

```
{
    "RequestId":"F3CD6886-D8D0-4FEE-B93E-1B73239673DE"
}
```

## Error codes {#ErrorCode .section}

|Error code|Error message|HTTP status code|Description|
|:---------|:------------|:---------------|:----------|
|DiskCategory.OperationNotSupported |The type of the specified disk does not support creating a snapshot.|400 |You cannot apply automatic policy to a local disk. For more information, see [Local disks](../../../../reseller.en-US/Product Introduction/Block storage/Local disks.md#).|
|DiskCategory.OperationNotSupported|The types of some disks in the disk list do not support creating snapshots.|400|IDs of local disks exist in the `DiskIds`.|
|ParameterInvalid|The specified automatic snapshot policy does not exist.|404 |The specified `AutoSnapshotPolicyId` does not exist.|
|ParameterInvalid|The specified automatic snapshot policy does not exist in the region.|404 |The specified `AutoSnapshotPolicyId` does not exist in the specified region.|
|ParameterInvalid|The specified AutoSnapshotPolicyId parameter is invalid.|404 |The specified `AutoSnapshotPolicyId` is invalid.|
|ParameterInvalid|The specified DiskIds are invalid.|404 |The specified `DiskIds` are invalid.|
|ParameterInvalid|The specified RegionId parameter is invalid.|404 |The specified `RegionId` is invalid.|

