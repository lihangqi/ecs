# Windows \_ Format a data disk {#concept_a3f_mg2_wdb .concept}

If you have already attached a data disk to your ECS instance, you must log on to the instance to partition and format the data disk for use.

This document describes how to create a single-partition data disk using a new data disk and format the partition. You can also create multiple partitions on a data disk according to your business needs. This document only applies to partitioning a data disk less than 2 TiB. If you want to partition and format a data disk more than 2 TiB, see [Partition and format data disk more than 2 TB](../../../../intl.en-US/User Guide/Cloud disks/Partition and format data disk more than 2 TB.md#).

**Warning:** 

-   Disk partitioning and formatting are high-risk operations, so please proceed with caution. This document describes how to deal with a new blank data disk. If you have data on a data disk, **make sure that you have created a snapshot of the data disk to avoid any possible data loss**.

-   ECS only supports partitioning **data disks**, not **system disks** . Forcibly partitioning a system disk using a third-party tool may cause unknown risks such as system crashes or data loss.


## Prerequisites {#section_dsm_sg2_wdb .section}

For a separately [purchased data disk](../../../../intl.en-US/User Guide/Cloud disks/Create a cloud disk.md#), you must [attach it to an instance in the ECS console](../../../../intl.en-US/User Guide/Cloud disks/Attach a cloud disk.md#) before partitioning and formatting.

A data disk purchased along with the instance can be partitioned and formatted without being attached.

## Procedure {#section_avp_tg2_wdb .section}

This example describes the steps to partition and format a 20 GiB data disk on the 64-bit Windows Server 2012 R2.

1.  [Connect to an instance](intl.en-US/Quick Start for Entry-Level Users/Step 3. Connect to an instance.md#).
2.  On the Windows Server desktop, right click the  **Start** icon, and select **Disk Management**.

    The data disk not formatted and partitioned \(in this example, Disk 2\) is in the **Offline** status.

3.  Right click the blank area around Disk 2, and select **Online** in the context menu.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9605/5091_en-US.png)

    After going online, the status of Disk 2 is displayed as **Not Initialized**.

4.  Right click the blank area around Disk 2, and select **Initialize Disk** in the context menu.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9605/5092_en-US.png)

5.  In the Initialize Disk dialog box, select **Disk 2**, and select a partitioning method:
    -   MBR is still the most common partitioning method. However, this method only supports a maximum partition size of 2 TB and creation of a maximum of four primary partitions. If you want to divide a disk into more than four partitions, you must take a primary partition as an extended partition and create logical partitions in it.

    -   GPT is a new partitioning method, which is not recognizable to earlier versions of Windows. The maximum partition size that GPT can support is determined by the operating system and the file system. On the Windows operating system, GPT supports creating up to 128 primary partitions.

        In this example, we select the MBR partitioning method, and click **Yes**.

6.  In the Disk Management window, right click the **Unallocated** area of Disk 2 and select **New Simple Volume**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9605/5094_en-US.png)

7.  In the New Simple Volume Wizard, follow these steps:
    1.  Click **Next**.
    2.  Specify Volume Size: Specify the size of the simple volume to create. If you need only one primary partition, use the default value, and then click Next. Click **Next**.
    3.  Assign Drive Letter or Path: Select a drive letter \(in this example, F\). Click **Next**.
    4.  Format Partition: Select the formatting settings, including file system, allocation unit size, and volume label, and confirm whether to **Perform a quick format** and **Enable file and folder compression**. Use the default value. Click **Next**.
    5.  Start creating a new simple volume. When a new simple volume has been created, click **Finish** to close New Simple Volume Wizard.

After the partition formatting is completed, the status of Disk 2 in **Disk Management** is as shown in the following screenshot.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9605/5103_en-US.png)

In **This PC**, you can view the new drive **New Volume \(F:\)**, which means the data disk is ready for use.

