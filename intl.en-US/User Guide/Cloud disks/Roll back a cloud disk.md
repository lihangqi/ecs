# Roll back a cloud disk {#concept_pkk_wf3_ydb .concept}

If you have [created snapshots](reseller.en-US/User Guide/Snapshots/Create a snapshot.md#) for a cloud disk, you can use the **Disk Rollback** feature to restore a cloud disk to a specific snapshot status at a given time point.

## Note {#section_i4y_dg3_ydb .section}

Before you roll back a cloud disk, note the following:

-   Rolling back a cloud disk is an irreversible action. Once rollback is complete, data cannot be restored. Exercise caution when performing this action.

-   After the disk is rolled back, data from the creation date of the snapshot to the rollback date is lost.

-   After a system disk is restored, the logon password or the SSH key pair of the ECS instance is retained.


## Prerequisites {#section_k4y_dg3_ydb .section}

Before rolling back a cloud disk, check that:

-   You have [created a snapshot](reseller.en-US/User Guide/Snapshots/Create a snapshot.md#) for the cloud disk, and no snapshot creation is in progress.

-   You have not released the cloud disk.

-   The cloud disk has been [attached to an ECS instance](reseller.en-US/User Guide/Cloud disks/Attach a cloud disk.md#) and the instance is in the [Stopped](reseller.en-US/User Guide/Instances/Start or stop an instance.md#) status.

    **Note:** For a Pay-As-You-Go VPC-Connected ECS instance, if the [No fees for stopped instances \(VPC-Connected\)](../../../../reseller.en-US/Pricing/No fees for stopped VPC instances.md#) feature is enabled, to stop an instance, in the Notice dialog box, click **OK**. Then in the Stop dialog box, select **Keep Instance with Fees**, and click **OK**. If you use the **No fees for stopped instances \(VPC-Connected\)** feature, you may not be able to start the instance successfully after changing the system disk.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9676/15432253115328_en-US.png)


## Procedure {#section_o4y_dg3_ydb .section}

To roll back a cloud disk , follow these steps:

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, click **Instances**.
3.  Select the target region.
4.  Find the target instance and click its ID to go to its Instance Details page.
5.  In the left-side navigation pane, click **Instance Snapshots**.
6.  Find the target snapshot and then in the **Actions** column, click **Disk Rollback**.
7.  In the dialog box, click **OK**.

    **Note:** If you select **Start Instance after Rollback**, the instance starts automatically after the disk is restored.


## Related API {#section_r4y_dg3_ydb .section}

[ResetDisk](../../../../reseller.en-US/API Reference/Disk/ResetDisk.md#)

## Additional operations {#section_s4y_dg3_ydb .section}

If you resize a cloud disk after creating a snapshot, you can connect to the instance to resize its file system. For more information, see:

-   [Linux \_ Resize a data disk](reseller.en-US/User Guide/Cloud disks/Resize cloud disks/Linux _ Resize a data disk.md#)
-   [Windows \_ Resize a data disk](reseller.en-US/User Guide/Cloud disks/Resize cloud disks/Windows _ Resize a data disk.md#)

