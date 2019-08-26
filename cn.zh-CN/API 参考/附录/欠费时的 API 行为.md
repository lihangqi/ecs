# 欠费时的 API 行为 {#EcsApiOverduePayement .reference}

下列表中，“-” 表示无关，“正常逻辑逻辑”表示按照接口的正常逻辑逻辑执行并返回结果。

欠费指的是在`DescribeInstanceAttribute`或者`DescribeDisks`返回的传出参数中的`OperationLocks`包含了`LockReason: financial`。

## 实例欠费时 {#section_wdr_cng_ydb .section}

|接口|磁盘欠费|磁盘正常|
|:-|:---|:---|
|AllocatePublicIpAddress|报错|报错|
|AttachDisk|报错|正常逻辑|
|AuthorizeSecurityGroup|正常逻辑|正常逻辑|
|CreateDisk|报错|正常逻辑|
|CreateImage|正常逻辑|正常逻辑|
|CreateInstance|报错|报错|
|CreateSecurityGroup|正常逻辑|正常逻辑|
|CreateSnapshot|正常逻辑|正常逻辑|
|DeleteDisk|正常逻辑|正常逻辑|
|DeleteImage|正常逻辑|正常逻辑|
|DeleteInstance|正常逻辑|正常逻辑|
|DeleteSecurityGroup|正常逻辑|正常逻辑|
|DeleteSnapshot|正常逻辑|正常逻辑|
|DescribeAutoSnapshotPolicy|正常逻辑|正常逻辑|
|DescribeDisks|正常逻辑|正常逻辑|
|DescribeImages|正常逻辑|正常逻辑|
|DescribeInstanceAttribute|正常逻辑|正常逻辑|
|DescribeInstanceStatus|正常逻辑|正常逻辑|
|DescribeInstanceTypes|正常逻辑|正常逻辑|
|DescribeInstanceMonitorData|正常逻辑|正常逻辑|
|DescribeRegions|正常逻辑|正常逻辑|
|DescribeSecurityGroupAttribute|正常逻辑|正常逻辑|
|DescribeSecurityGroups|正常逻辑|正常逻辑|
|DescribeSnapshotAttribute|正常逻辑|正常逻辑|
|DescribeSnapshots|正常逻辑|正常逻辑|
|DescribeZones|正常逻辑|正常逻辑|
|DetachDisk|正常逻辑|正常逻辑|
|JoinSecurityGroup|正常逻辑|正常逻辑|
|LeaveSecurityGroup|正常逻辑|正常逻辑|
|ModifyAutoSnapshotPolicy|正常逻辑|正常逻辑|
|ModifyDiskAttribute|正常逻辑|正常逻辑|
|ModifyInstanceAttribute|正常逻辑|正常逻辑|
|RebootInstance|-|-|
|ReInitDisk|报错|报错|
|ReplaceSystemDisk|报错|报错|
|ResetDisk|报错|报错|
|RevokeSecurityGroup|正常逻辑|正常逻辑|
|StartInstance|报错|报错|
|StopInstance|-|-|

## 磁盘欠费时 {#section_jvm_vmg_ydb .section}

|接口|实例欠费|实例正常|
|:-|:---|:---|
|AllocatePublicIpAddress|报错|正常逻辑|
|AttachDisk|报错|报错|
|AuthorizeSecurityGroup|正常逻辑|正常逻辑|
|CreateDisk|报错|报错|
|CreateImage|正常逻辑|正常逻辑|
|CreateInstance|报错|正常逻辑|
|CreateSecurityGroup|正常逻辑|正常逻辑|
|CreateSnapshot|正常逻辑|正常逻辑|
|DeleteDisk|正常逻辑|正常逻辑|
|DeleteImage|正常逻辑|正常逻辑|
|DeleteInstance|正常逻辑|正常逻辑|
|DeleteSecurityGroup|正常逻辑|正常逻辑|
|DeleteSnapshot|正常逻辑|正常逻辑|
|DescribeAutoSnapshotPolicy|正常逻辑|正常逻辑|
|DescribeDisks|正常逻辑|正常逻辑|
|DescribeImages|正常逻辑|正常逻辑|
|DescribeInstanceAttribute|正常逻辑|正常逻辑|
|DescribeInstanceStatus|正常逻辑|正常逻辑|
|DescribeInstanceMonitorData|正常逻辑|正常逻辑|
|DescribeRegions|正常逻辑|正常逻辑|
|DescribeSecurityGroupAttribute|正常逻辑|正常逻辑|
|DescribeSecurityGroups|正常逻辑|正常逻辑|
|DescribeSnapshotAttribute|正常逻辑|正常逻辑|
|DescribeSnapshots|正常逻辑|正常逻辑|
|DescribeZones|正常逻辑|正常逻辑|
|DetachDisk|正常逻辑|正常逻辑|
|JoinSecurityGroup|正常逻辑|正常逻辑|
|LeaveSecurityGroup|正常逻辑|正常逻辑|
|ModifyAutoSnapshotPolicy|正常逻辑|正常逻辑|
|ModifyDiskAttribute|正常逻辑|正常逻辑|
|ModifyInstanceAttribute|报错|正常逻辑|
|ModifyInstanceSpec|报错|正常逻辑|
|RebootInstance|-|-|
|ReInitDisk|报错|正常逻辑|
|ReplaceSystemDisk|报错|正常逻辑|
|ResetDisk|报错|报错|
|RevokeSecurityGroup|正常逻辑|正常逻辑|
|StartInstance|报错|正常逻辑|
|StopInstance|-|-|

