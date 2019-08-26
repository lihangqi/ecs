# Roll back a disk by using a snapshot {#concept_smh_y2l_xdb .concept}

This topic describes how to roll back a disk by using a snapshot. You can perform a disk rollback when your OS is unresponsive, when an incorrect operation was performed, or when rolling back an application version is required. After you roll back the system disk, the current key pair or password of the corresponding instance is attached automatically.

**Warning:** Before you roll back a disk, [create a snapshot](reseller.en-US/Snapshots/Use snapshots/Create a snapshot.md#) of the disk to ensure that you can perform data recovery if needed. Disk rollback is irreversible. Exercise caution when performing this action.

## Prerequisites {#section_k4y_dg3_ydb .section}

-   A snapshot of the disk to be rolled back is created, and no new snapshot is being created for the disk. For more information, see [created a snapshot](reseller.en-US/Snapshots/Use snapshots/Create a snapshot.md#).
-   The disk has not been released.
-   The disk to be rolled back is attached to an ECS instance, and the corresponding instance is stopped. For more information, see [Attach to an ECS instance](reseller.en-US/Block storage/Block storage/Attach a cloud disk.md#) and [Stop an instance](reseller.en-US/Instances/ECS instance life cycle/Start or stop an instance.md#).

    **Note:** 

    -   After you [replace the system disk](../../../../../reseller.en-US/Block storage/Block storage/Change the operating system/Replace the system disk (public image).md#), old system disk snapshots cannot be used to roll back the new system disk.
    -   Pay-As-You-Go VPC instances may not be restarted in [No fees for stopped VPC instances](../../../../../reseller.en-US/Pricing/No fees for stopped VPC instances.md#) mode after you roll back the disk. We recommend that you disable **No fees for stopped VPC instances** before you stop the instance.

## Procedure {#section_o4y_dg3_ydb .section}

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, click **Instances**.
3.  Select the target region.
4.  Locate the instance whose disk you want to roll back, and then click **Manage**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9688/155255168739440_en-US.png)

5.  In the left-side navigation pane, click **Instance snapshots**.
6.  Select the target snapshot, and then click **Roll Back Disk** in the **Actions** column.

    **Note:** Only one disk can be rolled back at a time. When you roll back a disk, other disks attached to the instance are not affected. After the rollback, the entire disk \(rather than a partition or a directory\) recovers to its status at a specified point in time.

7.  In the displayed dialog box, click **OK**.

    **Note:** If you select **Start Instance After Disk Rollback**, the instance is restarted after you roll back the disk.


## Related APIs {#section_r4y_dg3_ydb .section}

[ResetDisk](../../../../../reseller.en-US/API Reference/Disk/ResetDisk.md#)

## What to do next {#section_s4y_dg3_ydb .section}

If you create a snapshot of a disk and then you scale out the disk, you need to log on to the instance to expand the capacity of the file system after disk rollback. For more information, see:

-   [Linux - Resize a data disk](reseller.en-US/Block storage/Block storage/Resize cloud disks/Linux - Resize a data disk.md#).
-   [Windows - Resize a data disk](reseller.en-US/Block storage/Block storage/Resize cloud disks/Windows - Resize a data disk.md#).

