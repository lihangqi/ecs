# API behavior when an instance is locked for security reasons {#EcsApi .reference}

This topic provides the API request consequence when your resource is frozen due to security concerns.

## API request consequence {#section_flj_dpg_ydb .section}

When a security lock is indicated, the `OperationLocks` in the outgoing parameters returned by the `DescribeInstances` will include `LockReason:security`.

**Note:** Disk-related activities in the `In_use` status reference the instance `OperationLocks`. Otherwise, the instance `OperationLocks` may be ignored.

In the following table, "Normal Logic" indicates that the interface is executed and result returned based on the normal logic of the interface.

|Interface|Behavior|
|:--------|:-------|
|AllocatePublicIpAddress|Error|
|AttachDisk|Error|
|AuthorizeSecurityGroup|Normal logic|
|CreateDisk|Normal logic|
|CreateImage|Normal logic|
|CreateInstance|Normal logic|
|CreateSecurityGroup|Normal logic|
|CreateSnapshot|Error \(Only for disks attached on this instance in the In\_use status\)|
|DeleteDisk|Normal logic|
|DeleteImage|Normal logic|
|DeleteInstance|Normal logic|
|DeleteSecurityGroup|Normal logic|
|DeleteSnapshot|Normal logic|
|DescribeAutoSnapshotPolicy|Normal logic|
|DescribeDisks|Normal logic|
|DescribeImages|Normal logic|
|DescribeInstanceStatus|Normal logic|
|DescribeInstanceTypes|Normal logic|
|DescribeInstanceMonitorData|Normal logic|
|DescribeRegions|Normal logic|
|DescribeSecurityGroupAttribute|Normal logic|
|DescribeSecurityGroups|Normal logic|
|DescribeSnapshotAttribute|Normal logic|
|DescribeSnapshots|Normal logic|
|DescribeZones|Normal logic|
|DetachDisk|Error|
|JoinSecurityGroup|Error|
|LeaveSecurityGroup|Error|
|ModifyAutoSnapshotPolicy|Normal logic|
|ModifyDiskAttribute|Normal logic|
|ModifyInstanceAttribute|Error|
|RebootInstance|Error|
|ReInitDisk| -   When the disk is in the `In_use`:
-   When the disk is in the other status: Normal Logic

 |
|ReplaceSystemDisk|Normal logic|
|ResetDisk|Error|
|RevokeSecurityGroup|Normal logic|
|StartInstance|Error|
|StopInstance|Error|

