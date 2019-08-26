# Resize cloud disks online {#concept_syg_jxz_2hb .concept}

You can resize Alibaba Cloud disks online. In this mode, you do not need to restart instances. You can resize both system disks and data disks online as described in this topic. The size of the disks is expected to increase as your business and application data grows.

## What is online resizing? {#section_ppz_wm1_fhb .section}

In the online mode, you can see that cloud disks are extended without restarting instances by using the console or API \([RebootInstance](../reseller.en-US/API Reference/Instances/RebootInstance.md#)\). The difference between the online and offline modes:

-   Online mode: You do not need to restart instances and instances must be in the **running** \(Running\) state.
-   [Offline mode](reseller.en-US/Block Storage/Block storage/Resize cloud disks/Resize cloud disks offline.md#): You must restart instances and instances can be in the **running** \(Running\) or **stopped** \(Stopped\) state.

## Notes {#section_m1k_pbb_fhb .section}

**System limits** 

-   For more information about thresholds of extended system disks and data disks, see [Overview](reseller.en-US/Block Storage/Block storage/Resize cloud disks/Overview.md#).
-   The operating system must meet the following conditions when you resize system disks. Otherwise, you must select the [offline mode](reseller.en-US/Block Storage/Block storage/Resize cloud disks/Resize cloud disks offline.md#).
    -   Windows operating system: cannot be Windows Server 2003.
    -   Linux operating system: The kernel version must be later than 3.6 when you run the `uname -a` command.
-   When you resize cloud disks, only storage capacity is extended, but not file systems. You can allocate your own storage space after resizing. For more information, see [Next operations](#).

**What is not supported** 

-   You cannot resize a cloud disk for which a snapshot is being created.
-   After you click [Renew for Configuration Downgrade](../reseller.en-US/Pricing/Renew instances/Renew for configuration downgrade.md#) for the subscription instance, you cannot resize subscription cloud disks of the instance during the remaining period of the current billing cycle.
-   If a data disk adopts the MBR partition format, you cannot resize the data disk to more than 2 TiB. If you want to resize a data disk to 2 TiB while the MBR partition format is used, we recommend that you create and attach another data disk. Format a GPT partition and copy the data in the MBR partition to the GPT partition.

**What is supported** 

-   You can resize cloud disks that are in the in use state. This occurs when instances to which the disks are attached are in the **Running**\(Running\) state.
-   You can resize cloud disks of I/O-optimized instances.
-   You can resize ultra disks and SSD disks.
-   For Windows instances, you can only resize the NTFS file system.

## Preparations {#section_tcx_kn5_qgb .section}

1.  [Create a snapshot](reseller.en-US/Snapshots/Use snapshots/Create a snapshot.md#) for data backup, to prevent data loss caused by any errors.
2.  Check whether you need to [update the RedHat VirtIO SICI driver](reseller.en-US/Block Storage/Block storage/Resize cloud disks/Resize a cloud disk online/Update a Red Hat VirtIO SICI driver in Windows.md#) for the instance if your Windows instance was created earlier than March 30, 2019.

## Procedure {#section_ak2_3zq_dhb .section}

Perform the following steps to resize a cloud disk in the ECS console:

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, choose **Storage & Snapshots** \> **Disks**.
3.  Locate the cloud disk to be extended. Choose **More** \> **Resize Disk** in the **Actions** column.
4.  Select ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/145922/156273603841189_en-US.png)**Resize Online**. You do not need to restart the instance to validate new capacity changes \(resize and partition operations\).
5.  Set the extended capacity, which must be greater than the current capacity.
6.  Confirm the fee, read ECS Service Terms and Product Terms of Service, and then click **Confirm to Resize**.
7.  Complete the payment.

**Note:** If you do not select **Resize Online** or ECS does not meet the conditions for **Resize Online**, you must log on to the console or use the API \([RebootInstance](../reseller.en-US/API Reference/Instances/RebootInstance.md#)\) to restart the instance for the changes to take effect.

Related API: You can also call [ResizeDisk](../reseller.en-US/API Reference/Disk/ResizeDisk.md#) to perform the resize operation.

## Next operations {#section_fvh_w2r_dhb .section}

The following table lists the available operations after you resize a cloud disk. However, this depends on whether the cloud disk is attached and partitioned.

|**Disk status**|A disk that is not attached or partitioned|A disk that is attached but not partitioned|A disk that is attached and partitioned|
|**Next**| If a data disk is in the **available** \(Available\) state, the extended capacity takes effect after you complete the payment. Then you can perform the following steps:

 1.  Log on to the console or use the API \(AttachDisk\) to [attach a cloud disk](reseller.en-US/Block Storage/Block storage/Attach a cloud disk.md#).
2.  Resize or format a partition:
    -   [Partition or format a Linux data disk of less than 2 TiB](../reseller.en-US/Quick Start for Entry-Level Users/Step 4. Format a data disk/Format a data disk of a Linux instance.md#)
    -   [Partition or format a Windows data disk of less than 2 TiB](../reseller.en-US/Quick Start for Entry-Level Users/Step 4. Format a data disk/Format a data disk for Windows instances.md#)
    -   [Partition or format a data disk of more than 2 TiB](reseller.en-US/Block Storage/Block storage/Format a data disk/Partition and format data disk more than 2 TiB.md#)

 |You can perform the following steps: 1.  Resize or format a partition:
    -   [Partition or format a Linux data disk of less than 2 TiB](../reseller.en-US/Quick Start for Entry-Level Users/Step 4. Format a data disk/Format a data disk of a Linux instance.md#)
    -   [Partition or format a Windows data disk of less than 2 TiB](../reseller.en-US/Quick Start for Entry-Level Users/Step 4. Format a data disk/Format a data disk for Windows instances.md#)
    -   [Partition or format a data disk of more than 2 TiB](reseller.en-US/Block Storage/Block storage/Format a data disk/Partition and format data disk more than 2 TiB.md#)
2.  Resize a file system:
    -   For a Linux instance, see [Resize a partition and file system of a Linux data disk](reseller.en-US/ECS/Increase disk size online/Extend the file system of the Linux system disk.md#) or [Resize a partition and file system of a Linux system disk](reseller.en-US/ECS/Increase disk size online/Extend the file system of a Linux data disk.md#)
    -   For a Windows instance, see [Resize a file system of a Windows disk](reseller.en-US/ECS/Increase disk size online/Extend a Windows file system.md#)

 | Resize a partition and file system:

 -   For a Linux instance, see [Resize a partition and file system of a Linux data disk](reseller.en-US/ECS/Increase disk size online/Extend the file system of the Linux system disk.md#) or [Resize a partition and file system of a Linux system disk](reseller.en-US/ECS/Increase disk size online/Extend the file system of a Linux data disk.md#)
-   For a Windows instance, see [Resize a file system of a Windows disk](reseller.en-US/ECS/Increase disk size online/Extend a Windows file system.md#)

 |

