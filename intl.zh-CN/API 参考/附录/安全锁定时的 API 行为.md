# 安全锁定时的 API 行为 {#EcsApi .reference}

注意，和磁盘有关的行为在`In_use`的状态下依赖实例的`OperationLocks`，否则可以忽略实例的`OperationLocks`。

被安全锁定指的是在`DescribeInstanceAttribute`返回的传出参数中的`OperationLocks`包含了`LockReason: security`。

|接口|行为|
|:-|:-|
|AllocatePublicIpAddress|报错|
|AttachDisk|报错|
|AuthorizeSecurityGroup|正常逻辑|
|CreateDisk|正常逻辑|
|CreateImage|正常逻辑|
|CreateInstance|-|
|CreateSecurityGroup|正常逻辑|
|CreateSnapshot|报错（只针对挂载在该实例上的磁盘，In\_use状态）|
|DeleteDisk|正常逻辑|
|DeleteImage|正常逻辑|
|DeleteInstance|正常逻辑|
|DeleteSecurityGroup|正常逻辑|
|DeleteSnapshot|正常逻辑|
|DescribeAutoSnapshotPolicy|正常逻辑|
|DescribeDisks|正常逻辑|
|DescribeImages|正常逻辑|
|DescribeInstanceAttribute|正常逻辑|
|DescribeInstanceStatus|正常逻辑|
|DescribeInstanceTypes|正常逻辑|
|DescribeInstanceMonitorData|正常逻辑|
|DescribeRegions|正常逻辑|
|DescribeSecurityGroupAttribute|正常逻辑|
|DescribeSecurityGroups|正常逻辑|
|DescribeSnapshotAttribute|正常逻辑|
|DescribeSnapshots|正常逻辑|
|DescribeZones|正常逻辑|
|DetachDisk|报错|
|JoinSecurityGroup|报错|
|LeaveSecurityGroup|报错|
|ModifyAutoSnapshotPolicy|正常逻辑|
|ModifyDiskAttribute|正常逻辑|
|ModifyInstanceAttribute|报错|
|RebootInstance|报错|
|ReInitDisk|报错\(In\_use\)，正常逻辑（其他状态）|
|ReplaceSystemDisk|正常逻辑|
|ResetDisk|报错|
|RevokeSecurityGroup|正常逻辑|
|StartInstance|报错|
|StopInstance|报错|

