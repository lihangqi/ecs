# Attach a cloud disk {#concept_llz_b4c_ydb .concept}

You can create a cloud disk and attach it to an ECS instance to function as a data disk by going to the Instance Disks page or on the Disk List page.

## Note {#section_utx_d4c_ydb .section}

Before you attach a cloud disk to an ECS instance, consider the following:

-   If a cloud disk is created at the same time as an ECS instance, you do not have to attach the disk.
-   You can attach a cloud disk to work as a data disk only, but not as a system disk.
-   To attach a cloud disk to an ECS instance, the instance must meet the following requirements:
    -   The instance must be in the **Running** or **Stopped** status. It cannot be in **Locked** status.
    -   The instance must not have any overdue payments.
-   The disk to be attached must be in the **Available** status.
-   The cloud disk and the ECS instance must be in the same region and the same zone.
-   Up to 16 cloud disks can be attached to an ECS instance to work as data disks. However, a cloud disk cannot be attached to multiple instances simultaneously.
-   A cloud disk can be attached to an ECS instance, regardless of the billing method of the instance.

## Prerequisites {#section_xtx_d4c_ydb .section}

You must create an ECS instance and a cloud disk in the same region and zone. For more information, see [create a cloud disk](reseller.en-US/User Guide/Cloud disks/Create a cloud disk.md#) and [create an instance](../../../../reseller.en-US/Quick Start for Entry-Level Users/Step 2. Create an instance.md#) in *Quick Start*.

## Attach a cloud disk on the Instance Disks page {#section_ytx_d4c_ydb .section}

To attach one or multiple cloud disks to a specified ECS instance, follow these steps:

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, click **Instances**.
3.  Select the target region.
4.  Find the target ECS instance and click its ID to go to its Instance Details page.
5.  In the left-side navigation pane, click **Disks** and then, on the Disks page, click **Mount**.
6.  In the dialog box, complete the following configurations:
    -   **Target Disk**: Select a cloud disk in the **Unmounted** status in the same region and zone.
    -   **Release Disk with Instance**: If you select this option, the disk is released when you release its corresponding instance.
    -   **Delete Automatic Snapshots While Releasing Disk**: If you select this option, all the automatic snapshots of the target disk are deleted when you release it. However, all the manual snapshots are retained. To keep a complete data backup, we recommend that you do not select this option.

        Click **OK** and then click **Mount**.

7.  Refresh the Disk List.

    When the status of the cloud disk is **In Use**, the attachment is successful.

8.  According to the content of the cloud disk and the operating system of the ECS instance, perform follow-up operations as required to make the disk ready for use. The following table details the different follow-up operations available.

    |Disk content|Operating system of the ECS instance|Follow-up operations|
    |:-----------|:-----------------------------------|:-------------------|
    |A new empty cloud disk|Linux|[Format a data disk for Linux instance](../../../../reseller.en-US/Quick Start for Entry-Level Users/Step 4. Format a data disk/Format a data disk for Linux instance.md#). If the cloud disk is larger than 2 TiB, see [partition and format data disk more than 2 TiB](reseller.en-US/User Guide/Cloud disks/Partition and format data disk more than 2 TiB.md#).|
    |Windows|[Format a data disk for Windows instances](../../../../reseller.en-US/Quick Start for Entry-Level Users/Step 4. Format a data disk/Format a data disk for Windows instances.md#). If the cloud disk is larger than 2 TiB, see [partition and format data disk more than 2 TiB](reseller.en-US/User Guide/Cloud disks/Partition and format data disk more than 2 TiB.md#).|
    |A cloud disk from a snapshot|Linux|Connect to the Linux instance and run the `mount` command to mount the partitions to make the disk ready for use.|
    |Windows|No follow-up operations are required. The cloud disk is ready for use.|


## Attach a cloud disk on the Disk List page {#section_i5x_d4c_ydb .section}

To attach a cloud disks to an ECS instances, follow these steps:

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, select **Block Storage** \> **Disks**.
3.  Select the target region.
4.  Find a cloud disk in the **Unmounted** status and then, in the **Actions** column, select **More** \> **Mount**.
5.  In the dialog box, complete the following configurations:
    -   **Target Instance**: Select an ECS instance in the same zone.
    -   **Release Disk with Instance**: If you select this option, the disk is released when you release its instance.
    -   **Delete Automatic Snapshots While Releasing Disk**: If you select this option, all the automatic snapshots of the selected disk are deleted when you release the disk. However, all the manual snapshots are retained. To keep complete data backup, we recommend that you do not select this option.

        Click **Mount**.

6.  Refresh the disk list.

    When the status of the cloud disk is **In Use**, the attachment is successful.

7.  According to the content of the cloud disk and the operating system of the ECS instance, perform follow-up operations as required to make the disk ready for use. The following table details the different follow-up operations available.

    |Disk content|Operating system of the ECS instance|Follow-up operations|
    |:-----------|:-----------------------------------|:-------------------|
    |A new empty cloud disk|Linux|[Format a data disk for Linux instance](../../../../reseller.en-US/Quick Start for Entry-Level Users/Step 4. Format a data disk/Format a data disk for Linux instance.md#). If the cloud disk is larger than 2 TiB, see [partition and format data disk more than 2 TiB](reseller.en-US/User Guide/Cloud disks/Partition and format data disk more than 2 TiB.md#).|
    |Windows|[Format a data disk for Windows instances](../../../../reseller.en-US/Quick Start for Entry-Level Users/Step 4. Format a data disk/Format a data disk for Windows instances.md#). If the cloud disk is larger than 2 TiB, see [partition and format data disk more than 2 TiB](reseller.en-US/User Guide/Cloud disks/Partition and format data disk more than 2 TiB.md#).|
    |A cloud disk from a snapshot|Linux|Connect to the Linux instance and run the `mount` command to mount the partitions to make the disk ready for use.|
    |Windows|No follow-up operations are required. The cloud disk is ready for use.|


## Additional operations {#section_r5x_d4c_ydb .section}

After a cloud disk is attached to an ECS instance, you can perform any of the following operations according to your business needs:

-   You can [reinitialize a cloud disk](reseller.en-US/User Guide/Cloud disks/Reinitialize a cloud disk.md#) to restore it to the initial status after it is created.
-   You can increase the size of the cloud disk by resizing it. For more information, see [Linux \_ Resize a data disk](reseller.en-US/User Guide/Cloud disks/Resize cloud disks/Linux _ Resize a data disk.md#) or [Windows \_ Resize a data disk](reseller.en-US/User Guide/Cloud disks/Resize cloud disks/Windows _ Resize a data disk.md#).
-   You can [create snapshots](reseller.en-US/User Guide/Snapshots/Create a snapshot.md#) of the cloud disk to back up data. Alternatively, you can [apply automatic snapshot policies to disks](reseller.en-US/User Guide/Snapshots/Apply automatic snapshot policies to disks.md#).
-   You can use a snapshot to [roll back a cloud disk](reseller.en-US/User Guide/Cloud disks/Roll back a cloud disk.md#) to restore the cloud disk to a previous state.
-   You can [detach a cloud disk](reseller.en-US/User Guide/Cloud disks/Detach a cloud disk.md#) and [release a cloud disk](reseller.en-US/User Guide/Cloud disks/Release a cloud disk.md#) when you no longer require a cloud disk to reduce costs.

## Related API {#section_u5x_d4c_ydb .section}

[AttachDisk](../../../../reseller.en-US/API Reference/Disk/AttachDisk.md#)

