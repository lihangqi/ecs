# Data restoration in Windows instances {#concept_52020_zh .concept}

When solving problems related to disks, you may frequently encounter the loss of data disk partitions. This article describes common data partition loss problems and corresponding solutions in Windows, and provides common mistakes and best practices for cloud disks to avoid possible risks of data loss.

## Prerequisites {#section_rnp_qyf_hfb .section}

Before restoring data, you must create snapshots for data disks that lose partitions. If problems occur during the restoration process, you can roll back data disks to the status before restoration.

## Introduction to disk management tools {#section_fnl_ryf_hfb .section}

In Windows instances, you can select either of the following tools for restoring data disk data:

-   Disk Management: A tool provided by Windows for partitioning and formatting the disk.
-   Data restoration software: Generally, they are commercial software, and can be downloaded from the providers' official websites. They are mainly used for restoring data in an abnormal file system.

## Status of the disk is Foreign and no partitions are displayed {#section_hnl_ryf_hfb .section}

In the Disk Management of Windows, the disk is in the **Foreign** status and displays no partitions.

Solution:

Right click the **Foreign** disk, select **Import Foreign Disks**, and then click **OK**.

## Status of the disk is Offline and no partitions are displayed {#section_knl_ryf_hfb .section}

In the Disk Management of Windows, the disk is in the **Offline** status and displays no partitions.

Solution:

Right click the **Offline** disk \(for example, **Disk 1**\), select **Online**, and then click **OK**.

## No drive letter assigned {#section_nnl_ryf_hfb .section}

In the Disk Management of Windows, you can view data disk information, but no drive letter is allocated to the data disk.

Solution:

Right click primary partition of the disk \(for example, **Disk 1**\), click **Change drive letter and paths**, and then complete operations by prompt.

## Error occurred during storage enumeration {#section_qnl_ryf_hfb .section}

In the Disk Management of Windows, you cannot view data disks. An error occurred during storage enumeration is reported in the system log.

**Note:** Some versions may report Error occurred during enumeration of volumes. They are the same.

Solution:

1.  Start Windows PowerShell.
2.  Run winrm quickconfig for restoring. When “Make these changes \[y/n\]?” is displayed on the interface, you must type y to run the command.

     


After the restoration, you can have the data disks in the Disk Management.

## Data disk is in RAW format {#section_vnl_ryf_hfb .section}

In some special circumstances, the disk in Windows is in RAW format.

If the file system of a disk is unrecognizable to Windows, it is displayed as a RAW disk. This usually occurs when the partition table or boot sector that records the type or location of the file system is lost or damaged. Common causes are listed as follows:

-   **Safely remove hardware** is not used when disconnecting the external disk.
-   Disk problems caused by power outages or unexpected shutdown.
-   Hardware layer failure may also cause information loss of the disk partition.
-   Bottom layer drivers or disk-related applications. For example, DiskProbe can be used to directly modify the disk table structure.
-   Computer viruses.

For more information about how to fix these problems, see [Dskprobe Overview](https://technet.microsoft.com/en-us/library/cc736327(v=ws.10).aspx) document.

Moreover, Windows also contains a large variety of free or commercial data restoration software to restore lost data. For example, you can try to use Disk Genius to scan and restore expected documents.

## Common mistakes and best practices {#section_xnl_ryf_hfb .section}

Data is users’ core asset. Many users establish websites and databases \(MYSQL/MongoDB/Redis\) on ECS. Huge risks to the users’ services may occur when data is lost. Common mistakes and best practices are summarized as follows.

-   **Common mistakes**

    The bottom layer of Alibaba Cloud block-level storage is based on [triplicate technology](../../../../reseller.en-US/Product Introduction/Block storage/Triplicate technology.md#). Therefore, some users consider that no risk of data loss in the operating system exists. It is actually a misunderstanding. The three copies of data stored in the bottom layer provide physical layer protection for data disks. However, if problems occur to the cloud disk logic in the system, such as viruses, accidental data deletion, and file system damage, the data may still be lost. To guarantee data security, you have to use technologies such as Snapshot and backup.

-   **Best practices**

    Data disk partition restoration and data restoration are the final solutions for solving data loss problems, but it is never guaranteed. We strongly recommend that you follow the best practices to perform auto or manual snapshot on data and run different backup schemes to maximize your data security.

    -   **Enable automatic snapshots**

        Automatic snapshots are enabled for the system disk and data disk based on actual service conditions. Note that automatic snapshot may be released when the system disk is changed, the instance is expired, or the disk is manually released.

        You log on to the ECS console to change the attributes of the disks to **enable snapshot release with the disk**. Disable snapshot release with the disk if you want to retain the snapshots.

        For more information, see [FAQ about automatic snapshots](https://partners-intl.aliyun.com/help/faq-detail/40552.htm).

    -   **Create manual snapshots**

        Create snapshots manually before any important or risky operations such as:

        -   Upgrade the kernel
        -   Upgrade or change of applications
        -   Restoration of disk data
        You must create snapshots for disks before restoring them. After the snapshots are completed, you can perform other operations.

    -   **OSS, offline, or offsite backup**

        You can back up important data by means of OSS, offline, or offsite backup based on actual conditions.


