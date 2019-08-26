# Resize a cloud disk offline {#concept_kj1_mqg_ydb .concept}

This topic describes how to resize a cloud disk offline. If you resize a cloud disk offline, you need to restart the instance through the ECS console, or by calling the API RebootInstance for the operation to take effect.

## Limits {#section_bff_fwh_ydb .section}

**System limits** 

-   For detailed information about the limits of system disk resizing and data disk resizing, see [Disk resizing overview](intl.en-US/ECS/ECS conref warehouse/Disk resizing overview.md#).
-   Resizing a cloud disk does not extend the file system; it only extends the storage capacity. Therefore, you need to allocate storage space after you resize a cloud disk. For more information, see [What to do next](#).

**Supported cloud disk types** 

-   Cloud disks that are in use and are attached to **Running** or **Stopped** instances
-   Basic cloud disks, ultra disks, SSD cloud disks, and ESSD cloud disks
-   NTFS file system \(for Windows instances\)

**Unsupported cloud disk types** 

-   Cloud disks whose snapshot is being created
-   Cloud disks of Subscription instances that are included in the remaining billing cycle after such instances are [renewed for configuration downgrade](../../../../intl.en-US/Pricing/Renew instances/Renew for configuration downgrade.md#)
-   System disks of Windows Server 2003 instances

## Preparations {#section_tcx_kn5_qgb .section}

[Create a snapshot](intl.en-US/Snapshots/Use snapshots/Create a snapshot.md#) to back up your data.

## Procedure {#section_hff_fwh_ydb .section}

To resize a cloud disk in the ECS console, follow these steps:

1.  Log on to the [ECS console](https://ecs.console.aliyun.com/).
2.  In the left-side navigation pane, choose **Block Storage** \> **Disks**.
3.  Select the target region.
4.  Locate the target cloud disk, and then choose **More** \> **Resize Disk** in the **Actions** column.
5.  Set the **Capacity after resizing**.

    **Note:** The capacity after resizing cannot be less than the current capacity.

6.  Confirm the price, read and confirm you agree to the **ECS Service Terms** by selecting the check box, and then click **Confirm to resize**.
7.  Complete the payment.
8.  Use the ECS console or call the API \([RebootInstance](../../../../intl.en-US/API Reference/Instances/RebootInstance.md#)\) to restart the instance for the settings to take effect.

Related API: You can also call the API [ResizeDisk](../../../../intl.en-US/API Reference/Disk/ResizeDisk.md#) to resize the cloud disk.

## What to do next {#section_ivf_3by_khb .section}

After you resize a cloud disk, you can perform the following operations as needed.

|**Cloud disk type**|Cloud disk that is not attached or partitioned|Cloud disk that is attached but not partitioned|Cloud disk that is attached and partitioned|
|**Procedure**| If your cloud disk is in the **Available** state, the resizing settings take effect immediately after you complete the payment. You can:

 1.  Use the ECS console or call the API \(AttachDisk\) to [attach the cloud disk](../../../../intl.en-US/Block storage/Block storage/Attach a cloud disk.md#).
2.  Partition and format the cloud disk:
    -   [Partition and format a Linux data disk less than 2 TiB](../../../../intl.en-US/Quick Start for Entry-Level Users/Step 4. Format a data disk/Format a data disk of a Linux instance.md#).
    -   [Partition and format a Windows data disk less than 2 TiB](../../../../intl.en-US/Quick Start for Entry-Level Users/Step 4. Format a data disk/Format a data disk for Windows instances.md#).
    -   [Partition and format a cloud disk greater than 2 TiB](../../../../intl.en-US/Block storage/Block storage/Format a data disk/Partition and format data disk more than 2 TiB.md#).

 |You can perform the following operations as needed: 1.  Partition and format the cloud disk:
    -   [Partition and format a Linux data disk less than 2 TiB](../../../../intl.en-US/Quick Start for Entry-Level Users/Step 4. Format a data disk/Format a data disk of a Linux instance.md#).
    -   [Partition and format a Windows data disk less than 2 TiB](../../../../intl.en-US/Quick Start for Entry-Level Users/Step 4. Format a data disk/Format a data disk for Windows instances.md#).
    -   [Partition and format a cloud disk greater than 2 TiB](../../../../intl.en-US/Block storage/Block storage/Format a data disk/Partition and format data disk more than 2 TiB.md#).
2.  Extend the file system:
    -   [Extend the file system of a Linux system disk](intl.en-US/ECS/ECS conref warehouse/Extend the file system of the Linux system disk.md#) or [Extend the file system of a Linux data disk](intl.en-US/ECS/ECS conref warehouse/Extend the file system of a Linux data disk.md#).
    -   [Extend a Windows file system](intl.en-US/ECS/ECS conref warehouse/Extend a Windows partition and file system.md#).

 | Partition and format the cloud disk and extend the file system:

 -   [Extend the file system of a Linux system disk](intl.en-US/ECS/ECS conref warehouse/Extend the file system of the Linux system disk.md#) or [Extend the file system of a Linux data disk](intl.en-US/ECS/ECS conref warehouse/Extend the file system of a Linux data disk.md#).
-   [Extend a Windows file system](intl.en-US/ECS/ECS conref warehouse/Extend a Windows partition and file system.md#).

 |

