# API behavior for accounts with overdue payment {#EcsApiOverduePayement .reference}

When payment is overdue, the `OperationLocks` in the outgoing parameters returned by the `DescribeInstances` or `DescribeDisks` will include `LockReason: financial`.

## API request consequence with overdue payment {#section_wdr_cng_ydb .section}

In the following tables, "Normal Logic" indicates that the interface is executed and result returned based on the normal logic of the interface.

|Actions| Disk Payment Overdue|Disk Normal|
|:------|:--------------------|:----------|
|AllocatePublicIpAddress|Error|Error|
|AttachDisk|Error|Normal logic|
|AuthorizeSecurityGroup|Normal logic|Normal logic|
|CreateDisk|Error|Normal logic|
|CreateImage|Normal logic|Normal logic|
|CreateInstance|Error|Error|
|CreateSecurityGroup|Normal logic|Normal logic|
|CreateSnapshot|Normal logic|Normal logic|
|DeleteDisk|Normal logic|Normal logic|
|DeleteImage|Normal logic|Normal logic|
|DeleteInstance|Normal logic|Normal logic|
|DeleteSecurityGroup|Normal logic|Normal logic|
|DeleteSnapshot|Normal logic|Normal logic|
|DescribeAutoSnapshotPolicy|Normal logic|Normal logic|
|DescribeDisks|Normal logic|Normal logic|
|DescribeImages|Normal logic|Normal logic|
|DescribeInstanceStatus|Normal logic|Normal logic|
|DescribeInstanceTypes|Normal logic|Normal logic|
|DescribeInstanceMonitorData|Normal logic|Normal logic|
|DescribeRegions|Normal logic|Normal logic|
|DescribeSecurityGroupAttribute|Normal logic|Normal logic|
|DescribeSecurityGroups|Normal logic|Normal logic|
|DescribeSnapshotAttribute|Normal logic|Normal logic|
|DescribeSnapshots|Normal logic|Normal logic|
|DescribeZones|Normal logic|Normal logic|
|DetachDisk|Normal logic|Normal logic|
|JoinSecurityGroup|Normal logic|Normal logic|
|LeaveSecurityGroup|Normal logic|Normal logic|
|ModifyAutoSnapshotPolicy|Normal logic|Normal logic|
|ModifyDiskAttribute|Normal logic|Normal logic|
|ModifyInstanceAttribute|Normal logic|Normal logic|
|RebootInstance|-|-|
|ReInitDisk|Error|Error|
|ReplaceSystemDisk|Error|Error|
|ResetDisk|Error|Error|
|RevokeSecurityGroup|Normal logic|Normal logic|
|StartInstance|Error|Error|
|StopInstance|-|-|

|Actions|Instance Payment Overdue|Instance Normal|
|:------|:-----------------------|:--------------|
|AllocatePublicIpAddress|Error|Normal logic|
|AttachDisk|Error|Error|
|AuthorizeSecurityGroup|Normal logic|Normal logic|
|CreateDisk|Error|Error|
|CreateImage|Normal logic|Normal logic|
|CreateInstance|Error|Normal logic|
|CreateSecurityGroup|Normal logic|Normal logic|
|CreateSnapshot|Normal logic|Normal logic|
|DeleteDisk|Normal logic|Normal logic|
|DeleteImage|Normal logic|Normal logic|
|DeleteInstance|Normal logic|Normal logic|
|DeleteSecurityGroup|Normal logic|Normal logic|
|DeleteSnapshot|Normal logic|Normal logic|
|DescribeAutoSnapshotPolicy|Normal logic|Normal logic|
|DescribeDisks|Normal logic|Normal logic|
|DescribeImages|Normal logic|Normal logic|
|DescribeInstanceStatus|Normal logic|Normal logic|
|DescribeInstanceMonitorData|Normal logic|Normal logic|
|DescribeRegions|Normal logic|Normal logic|
|DescribeSecurityGroupAttribute|Normal logic|Normal logic|
|DescribeSecurityGroups|Normal logic|Normal logic|
|DescribeSnapshotAttribute|Normal logic|Normal logic|
|DescribeSnapshots|Normal logic|Normal logic|
|DescribeZones|Normal logic|Normal logic|
|DetachDisk|Normal logic|Normal logic|
|JoinSecurityGroup|Normal logic|Normal logic|
|LeaveSecurityGroup|Normal logic|Normal logic|
|ModifyAutoSnapshotPolicy|Normal logic|Normal logic|
|ModifyDiskAttribute|Normal logic|Normal logic|
|ModifyInstanceAttribute|Error|Normal logic|
|ModifyInstanceSpec|Error|Normal logic|
|RebootInstance|-|-|
|ReInitDisk|Error|Normal logic|
|ReplaceSystemDisk|Error|Normal logic|
|ResetDisk|Error|Error|
|RevokeSecurityGroup|Normal logic|Normal logic|
|StartInstance|Error|Normal logic|
|StopInstance|-|-|

