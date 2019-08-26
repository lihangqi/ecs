# Format a data disk for a Windows instance {#concept_a3f_mg2_wdb .concept}

This topic describes how to format a new data disk for a Windows instance, create a single partition in the data disk, and mount a file system on the data disk. You can use the procedures provided in this topic to create multiple partitions as needed.

**Warning:** 

-   Disk partitioning and formatting are high-risk operations. Exercise caution when performing these operations. The following procedure uses a newly purchased data disk as an example. If you partition or format an existing data disk, [create a snapshot of the data disk](../../../../intl.en-US/Snapshots/Use snapshots/Create a snapshot.md#) to avoid data loss.

-   We strongly recommend that you do not partition the system disk of an ECS instance. Failure to comply can result in unknown risks, such as system failure and data loss. You can only extend a partition of, or add a partition to, a system disk after you resize the system disk. For more information, see [Extend a Windows file system](../../../../intl.en-US/ECS/Increase disk size online/Extend a Windows file system.md#).


## Procedure {#section_bx0_5rf_awx .section}

The following procedure applies only to data disks less than 2 TiB. If your data disk is greater than 2 TiB, see [Partition and format a data disk greater than 2 TiB](../../../../intl.en-US/Block Storage/Block storage/Format a data disk/Partition and format data disk more than 2 TiB.md#).

In this example, a new 20 GiB data disk is partitioned and formatted. An instance running Windows Server 2012 R2 64-bit is used.

1.  [Connect to the instance](intl.en-US/Quick Start for Entry-Level Users/Step 3. Connect to an instance.md#).
2.  On the Windows Server desktop, right-click the **Start** icon, and then select **Disk management**.
3.  Locate the data disk that is not formatted \(Disk 2 in this example\) and check that the disk is in the **Offline** state.
4.  Right-click in the blank space in the **Disk 2** area, and then select **Online**.

    After Disk 2 goes online, it enters the **Not Initialized** state.

5.  Right-click in the blank space in the **Disk 2** area, and then select **Initialize Disk**.
6.  In the Initialize Disk dialog box, select **Disk 2**, and then select either of the following partitioning methods:
    -   MBR

        This method only supports data disks less than 2 TiB and can divide a disk into a maximum of four primary partitions. If you want to divide a disk into more than four partitions, you need to use a primary partition as an extended partition and create logical partitions in it.

    -   GPT

        Although GPT is a newer partitioning method, it is not recognized by earlier versions of Windows. The data disk size that GPT can support is determined by the operating system and the file system. In Windows, GPT supports up to 128 primary partitions.

        In this example, select MBR, and then click **OK**.

7.  In the Disk Management window, right-click the **Unallocated** area of Disk 2, and then select **New Simple Volume**.
8.  In the New Simple Volume Wizard dialog box, complete the following operations:
    1.  Click **Next**.
    2.  Specify the size of the simple volume. If you only need one primary partition, use the default value. Then, click **Next**.
    3.  Select a drive letter \(in this example, F\), and then click **Next**.
    4.  Select the required formatting settings \(including the file system, allocation unit size, and volume label\), and confirm whether to enable **Quick Formatting** and **File and Folder Compression**. In this example, use the default settings, and then click **Next**.
    5.  After the simple volume is created, click **Finish** to close the New Simple Volume Wizard.

After Disk 2 is partitioned and formatted, its status is displayed in the **Disk Management** window, as shown in the following figure.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9605/15664379995103_en-US.png)

In **This PC**, you can view a new drive named **New Volume \(F:\)**. The data disk is ready to use.

