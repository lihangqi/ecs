# Format a data disk for Windows instances {#concept_a3f_mg2_wdb .concept}

If data disks are selected when you create a Windows instance, you need to partition and format them for use.

This article describes how to create a single-partition data disk using a new data disk and how to mount a file system. You can also configure multiple partitions based on business needs. This article applies only to data disks that are not larger than 2 TiB. For those that are larger than 2 TiB, see [Partition and format data disk larger than 2 TiB](../../../../../intl.en-US/Block storage/Block storage/Format a data disk/Partition and format data disk more than 2 TiB.md#).

**Warning:** 

-   Disk partitioning and formatting are high-risk operations. Please proceed with caution. This article describes how to deal with a blank data disk. If you have data on a data disk, **be sure to create a snapshot for the data disk to avoid any possible data loss**.

-   ECS instances only support partitioning **data disks**, not  **system** disks. If you use a third-party tool to forcibly partition the system disk, unknown risks may occur, for example, system crash and data loss.


## Prerequisites {#section_dsm_sg2_wdb .section}

For a separately [purchased data disk](../../../../../intl.en-US/Block storage/Block storage/Create a cloud disk/Create a cloud disk.md#), you must [attach the data disk to an instance](../../../../../intl.en-US/Block storage/Block storage/Attach a cloud disk.md#) before partitioning and formatting.

A data disk purchased along with the instance can be partitioned and formatted without being attached.

## Procedure {#section_avp_tg2_wdb .section}

This example describes how to partition and format a 20 GiB data disk on the 64-bit Windows Server 2012 R2.

1.  [Connect to an instance](intl.en-US/Quick Start for Entry-Level Users/Step 3: Connect to an instance.md#).

2.  On Windows Server desktop, right click the **Start** icon, then select **Disk management**.

    The unformatted data disk \(Disk 2\) appears as **Offline**.

3.  Right click the blank area around Disk 2, and select **Online** in the context menu.

    After going online, the status of Disk 2 is displayed as **Not Initialized**.

4.  Right click the blank area around Disk 2, and then select **Initialize Disk** in the context menu.

5.  In the Initialize Disk dialog box, select **Disk 2** and a partitioning method:

    -   MBR is still the most common partitioning method. However, this method only supports data disks that no greater than 2 TB and can divide a disk into up to four primary partitions. If you want to divide a disk into more than four partitions, you need to take a primary partition as an extended partition and create logical partitions within it.

    -   GPT is a new partitioning method, and cannot be recognized by earlier versions of Windows. The size of GPT-partitioned data disk is determined by the operating system and the file system. In the Windows operating system, GPT supports up to 128 primary partitions.

        In this example, select the MBR partitioning method, and click **OK**.

6.  In the Disk Management window, right click the **Unallocated** area for Disk 2 and select **New Simple Volume**.

7.  In the New Simple Volume Wizard, follow these steps:

    1.  Click **Next**.

    2.  Specify Volume Size: Specify the size of the simple volume to create. If you need only one primary partition, use the default value, and then click **Next**.

    3.  Assign Drive Letter or Path: Select a drive letter \(in this example, F\). Click **Next**.

    4.  Format Partition: select format settings \(including the file system, allocation unit size, and volume label\), and confirm whether to enable **Quick Formatting** and **File and Folder Compression**. Use the default values,  then click **Next**.

    5.  Create a new simple volume. When the wizard shows the information below, a new simple volume is created. Click **Finish** to close the New Simple Volume Wizard.


After the partition formatting is completed, the status of Disk 2 in **Disk Management** is as shown in the following figure.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9605/15535927485103_en-US.png)

In **This PC**, you can view a new drive named **New Volume \(F:\)**. The data disk is now ready to use.

