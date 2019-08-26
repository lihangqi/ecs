# Data restoration in Linux instances {#concept_52046_zh .concept}

When solving problems related to disks, you may frequently encounter the loss of data disk partitions. This article describes common data partition loss problems and corresponding solutions in Linux, and provides common mistakes and best practices for cloud disks to avoid possible risks of data loss.

Before restoring data, you must create snapshots for data disks that lose partitions. If problems occur during the restoration process, you can roll back data disks to the status before restoration.

## Prerequisites {#section_bb4_b1f_hfb .section}

Before restoring data, you must create snapshots for data disks that lose partitions. If problems occur during the restoration process, you can roll back data disks to the status before restoration.

## Introduction to disk management tools {#section_bhg_b1f_hfb .section}

You can select one of the following tools to fix the disk partition and restore the data in a Linux instance:

-   fdisk : The default partitioning tool installed in Linux instances.
-   testdisk : It is primarily used to restore disk partitions or data in the Linux system. The tool is not installed by default in Linux. You must install it on your own. For example, in a CentOS system, you can run the yum install -y testdisk command to install it online.
-   partprobe : This is the default tool installed in the Linux system. It is primarily used to enable the kernel to re-read the partition without restarting the system.

## Handle data disk partition loss and data restoration in Linux {#section_ehg_b1f_hfb .section}

After you restart a Linux instance, you may encounter data disk partition loss or data loss issues. This may be because you have not set the partitions to be mounted automatically on startup of the instance in the etc/fstab file. In this case, you can manually mount the data disk partition first. If the system prompts partition table loss when you manually mount the data disk, you can try to solve the problem through the following three methods: [Restore partitions by using fdisk](#), [Restore partitions by using testdisk](#), or [Restore data by using testdisk](#).

-   **Restore partitions by using fdisk**

    Default values usually apply to the starting and ending sectors of the partition when you partition a data disk. You can then directly use fdisk to restore the partition. For more information about this tool, see [Linux Format and mount a data disk](../../../../intl.en-US/Quick Start for Entry-Level Users/Step 4. Format a data disk/Format a data disk of a Linux instance.md#).

    ![](images/13051_en-US_source.png)

    If the preceding operations do not help, you can try testdisk for the restoration.

-   **Restore partitions by using testdisk**

    Here we suppose the cloud disk device is named /dev/xvdb. Follow these steps to restore the partitions by using testdisk:

    1.  Run testdisk /dev/xvdb \(replace the device name as appropriate\), and then select Proceed \(default value\) and press the Enter key.

        ![](images/13052_en-US_source.png)

    2.  Select the partition table type for scanning: Intel by default. If your data disk uses the GPT format, select EFI GPT.

        ![](images/13053_en-US_source.png)

    3.  Select Analyse and then press the Enter key.

        ![](images/13054_en-US_source.png)

    4.  If you cannot see any partition, select Quick Search and then press the Enter key for a quick search.

        ![](images/13055_en-US_source.png)

        The partition information is displayed in the returned result, as shown in the following figure.

        ![](images/13056_en-US_source.png)

    5.  Select the partition and press the Enter key.
    6.  Select Write to save the partition.

        **Note:** Select Deeper Search to continue searching if the expected partition is not listed.

        ![](images/13057_en-US_source.png)

    7.  Press the Y key to save the partition.

        ![](images/13058_en-US_source.png)

    8.  Run partprobe /dev/xvdb \(replace the device name as appropriate\) to refresh the partition table manually.
    9.  Mount the partition again and view the data in the data disk.

        ![](images/13059_en-US_source.png)

-   **Restore data by using testdisk**

    In some cases, you can use testdisk to scan and locate the disk partition, but you cannot save the partition. In this case, you can try to restore files directly. Follow these steps:

    1.  Find the partition following Step 1 to Step 4 described in [Restore partitions by using teskdisk](#ol_jnv_4bf_hfb).
    2.  List files by pressing the P key. The returned result is shown in the following figure.

        ![](images/13060_en-US_source.png)

    3.  Select the files to restore, and press the C key.
    4.  Select a directory. In this example, the file is restored and copied to the /home directory.

        ![](images/13061_en-US_source.png)

        If you see `Copy done! 1 ok, 0 failed`, it indicates that copy was successful, as shown in the following figure.

        ![](images/13062_en-US_source.png)

    5.  Switch to the /home directory to view details. If you can see files, it indicates that files have been restored successfully.

        ![](images/13063_en-US_source.png)


## Common mistakes and best practices {#section_a3g_b1f_hfb .section}

Data is users’ core asset. Many users establish websites and databases \(MYSQL/MongoDB/Redis\) on ECS. Huge risks to the users’ services may occur when data is lost. Common mistakes and best practices are summarized as follows.

-   **Common mistakes**

    The bottom layer of Alibaba Cloud block-level storage is based on [triplicate technology](../../../../intl.en-US/Block Storage/Block storage/Triplicate technology.md#). Therefore, some users consider that no risk of data loss in the operating system exists. It is actually a misunderstanding. The three copies of data stored in the bottom layer provide physical layer protection for data disks. However, if problems occur to the cloud disk logic in the system, such as viruses, accidental data deletion, and file system damage, the data may still be lost. To guarantee data security, you have to use technologies such as Snapshot and backup.

-   **Best practices**

    Data disk partition restoration and data restoration are the final solutions for solving data loss problems, but it is never guaranteed. We strongly recommend that you follow the best practices to perform auto or manual snapshot on data and run different backup schemes to maximize your data security.

    -   **Enable automatic snapshots**

        Automatic snapshots are enabled for the system disk and data disk based on actual service conditions. Note that automatic snapshot may be released when the system disk is changed, the instance is expired, or the disk is manually released.

        You log on to the ECS console to change the attributes of the disks to enable **snapshot release with the disk**. Disable snapshot release with the disk if you want to retain the snapshots.

        For more information, see [FAQ about automatic snapshots](https://www.alibabacloud.com/help/faq-detail/40552.htm).

    -   **Create manual snapshots**

        Create snapshots manually before any important or risky operations such as:

        -   Upgrade the kernel
        -   Upgrade or change of applications
        -   Restoration of disk data
        You must create snapshots for disks before restoring them. After the snapshots are completed, you can perform other operations.

    -   **OSS, offline, or offsite backup**

        You can back up important data by means of OSS, offline, or offsite backup based on actual conditions.


