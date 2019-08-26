# Attach a cloud disk {#concept_llz_b4c_ydb .concept}

This topic describes how to attach a cloud disk. You can create a cloud disk and attach it to an ECS instance as a data disk.

## Limits {#section_utx_d4c_ydb .section}

Before you attach a cloud disk to an ECS instance, consider the following:

-   You can attach a cloud disk as a data disk only. You cannot attach a cloud disk as a system disk.
-   To attach a cloud disk to an ECS instance, the instance must meet the following requirements:
    -   The instance must be in the **Running** or **Stopped** status, but not in the **Locked** status.
    -   The instance must not have any overdue payments.
-   The disk to be attached must be in the **Unmounted** status.
-   The cloud disk and the ECS instance must be in the same region and the same zone.
-   Up to 16 cloud disks can be attached to an ECS instance to work as data disks. One cloud disk cannot be attached to multiple instances simultaneously.
-   If a cloud disk is created independently on the **Disks** page in the [ECS console](https://partners-intl.console.aliyun.com/#/ecs), it can be attached to any ECS instance in the same region and the same zone, regardless of the billing method of the instance.

## Prerequisites {#section_xtx_d4c_ydb .section}

You have created an ECS instance and a cloud disk in the same region and zone. For more information, see [Create an instance by using the wizard](../../../../../reseller.en-US/Instances/Create an instance/Create an instance by using the wizard.md#) and [Create a cloud disk](reseller.en-US/Block storage/Block storage/Create a cloud disk/Create a cloud disk.md#).

## Attach a cloud disk on the Instances page {#section_ytx_d4c_ydb .section}

If you want to attach multiple cloud disks to one ECS instance, we recommend that you do so on the Instances page. To attach cloud disks to a specified ECS instance, follow these steps:

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, click **Instances**.
3.  Select the target region.
4.  Find the target ECS instance and click its ID to go to its Instance Details page.
5.  In the left-side navigation pane, click **Disks**. Then on the Disks page, click **Mount** in the upper right corner.
6.  In the dialog box, complete the following configurations:
    -   **Target Disk**: Select a cloud disk in the **Unmounted** status in the same zone.
    -   **Release Disk with Instance**: If you select this option, the disk is released when you release the corresponding instance.
    -   **Delete Automatic Snapshots While Releasing Disk**: If you select this option, all the automatic snapshots of the selected disk are deleted when you release the disk. However, all the manual snapshots are retained. To keep a complete data backup history, we recommend that you do not select this option.

        Click **OK**, and then **Mount**.

7.  Refresh the Disks page.

    When the status of the cloud disk is **In Use**, the attachment is successful.

8.  According to the content of the cloud disk and the operating system of the ECS instance, perform appropriate operations to make the disk ready for use. The following table details the different follow-up operations.

    |Disk content|Operating system of the ECS instance|Follow-up operations|
    |:-----------|:-----------------------------------|:-------------------|
    |A new empty cloud disk|Linux|[Format a data disk of a Linux instance](../../../../../reseller.en-US/Quick Start for Entry-Level Users/Step 4. Format a data disk/Format a data disk of a Linux instance.md#). If the cloud disk is larger than 2 TiB, see [Partition and format data disk more than 2 TiB](reseller.en-US/Block storage/Block storage/Format a data disk/Partition and format data disk more than 2 TiB.md#).|
    |Windows|[Format a data disk for Windows instances](../../../../../reseller.en-US/Quick Start for Entry-Level Users/Step 4. Format a data disk/Format a data disk for Windows instances.md#). If the cloud disk is larger than 2 TiB, see [Partition and format data disk more than 2 TiB](reseller.en-US/Block storage/Block storage/Format a data disk/Partition and format data disk more than 2 TiB.md#).|
    |A cloud disk created from a snapshot|Linux|Connect to the Linux instance and run the `mount <partition> <mount point>` command to mount the partitions to the target mount points make the disk ready for use.|
    |Windows|No follow-up operations are required. The cloud disk is ready for use.|


## Attach a cloud disk on the Disks page {#section_i5x_d4c_ydb .section}

If you want to attach multiple cloud disks to different ECS instances, we recommend that you do so on the Disks page. To attach a cloud disk to an ECS instance, follow these steps:

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, select **Block Storage** \> **Disks**.
3.  Select the target region.
4.  Find a cloud disk in the **Unmounted** status. Then in the **Actions** column, select **More** \> **Mount**.
5.  In the dialog box, complete the following configurations:
    -   **Target Instance**: Select an ECS instance in the same zone.
    -   **Release Disk with Instance**: If you select this option, the disk is released when you release the corresponding instance.
    -   **Delete Automatic Snapshots While Releasing Disk**: If you select this option, all the automatic snapshots of the selected disk are deleted when you release the disk. However, all the manual snapshots are retained. To keep a complete data backup history, we recommend that you do not select this option.

        Click **Mount**.

6.  Refresh the Disks page.

    When the status of the cloud disk is **In Use**, the attachment is successful.

7.  According to the content of the cloud disk and the operating system of the ECS instance, perform appropriate operations to make the disk ready for use. The following table details different follow-up operations.

    |Disk content|Operating system of the ECS instance|Follow-up operations|
    |:-----------|:-----------------------------------|:-------------------|
    |A new empty cloud disk|Linux|[Format a data disk of a Linux instance](../../../../../reseller.en-US/Quick Start for Entry-Level Users/Step 4. Format a data disk/Format a data disk of a Linux instance.md#). If the cloud disk is larger than 2 TiB, see [Partition and format data disk more than 2 TiB](reseller.en-US/Block storage/Block storage/Format a data disk/Partition and format data disk more than 2 TiB.md#).|
    |Windows|[Format a data disk for Windows instances](../../../../../reseller.en-US/Quick Start for Entry-Level Users/Step 4. Format a data disk/Format a data disk for Windows instances.md#). If the cloud disk is larger than 2 TiB, see [Partition and format data disk more than 2 TiB](reseller.en-US/Block storage/Block storage/Format a data disk/Partition and format data disk more than 2 TiB.md#).|
    |A cloud disk created from a snapshot|Linux|Connect to the Linux instance and run the `mount` command to mount the partitions to make the disk ready for use.|
    |Windows|No follow-up operations are required. The cloud disk is ready for use.|


## What to do next {#section_r5x_d4c_ydb .section}

After a cloud disk is attached to an ECS instance, you can perform any of the following operations as needed:

-   You can [reinitialize a cloud disk](reseller.en-US/Block storage/Block storage/Reinitialize a cloud disk.md#) to restore its initial status.
-   You can increase the size of a cloud disk. For more information, see [Extend the file system of a Linux data disk](reseller.en-US/Block storage/Block storage/Resize cloud disks/Linux - Resize a data disk.md#) or [Extend a Windows file system](reseller.en-US/Block storage/Block storage/Resize cloud disks/Windows - Resize a data disk.md#).
-   You can [create a snapshot](reseller.en-US/Snapshots/Use snapshots/Create a snapshot.md#) of a cloud disk to back up its data. Alternatively, you can [use automatic snapshot policies](reseller.en-US/Snapshots/Use snapshots/Apply automatic snapshot policies to disks.md#) to create automatic snapshots.
-   You can use a snapshot to [roll back a cloud disk](reseller.en-US/Block storage/Block storage/Roll back a cloud disk.md#) to restore the cloud disk to a previous state.
-   You can [detach a cloud disk](reseller.en-US/Block storage/Block storage/Detach a cloud disk.md#) and [release a cloud disk](reseller.en-US/Block storage/Block storage/Release a cloud disk.md#) when you no longer require the cloud disk, thus reducing the costs.

## Related APIs {#section_u5x_d4c_ydb .section}

[AttachDisk](../../../../../reseller.en-US/API Reference/Disk/AttachDisk.md#)

