# Change the system disk \(custom image\) {#concept_vbb_ckj_ydb .concept}

**By changing a system disk, ** the system disk of your instance is replaced with a new cloud disk with a new disk ID, and the original system disk is released. If you want to change the operating system running on your instance, you can use  the **Change System Disk**  feature to complete it.  You can replace the OS image with a public image, shared image, custom image, or an image from the image marketplace.

**Note:** Microsoft has terminated technical support for Windows Server 2003. To guarantee your data security, we do not recommend that you continue running Windows Server 2003 on your ECS instance,   and we have stopped providing Windows Server 2003 image. For more information, see [Offline announcement of Windows Server 2003 system image](https://www.alibabacloud.com/help/faq-detail/59513.htm).

After a system disk is changed,

-   A new system disk with a new disk ID is assigned to your instance, and the original one is released.

-   The cloud disk category is retained.

-   The IP addresses and the MAC address of the instance are retained.

-   To make sure that your account have enough snapshot quota for the new system disk, you can delete unnecessary snapshots of the original system disk.


This article describes how to replace an existing image with a non-public image. If you want to use a public image, see [Change a system disk \(public image\)](intl.en-US/User Guide/Cloud disks/Change a system disk (public image).md#).

## Note {#section_zdm_dkj_ydb .section}

Before you begin, consider the following.

**Risks**

Changing a system disk has the following risks:

-   You have to stop your instance to change its system disk, which may interrupt your business operations.

-   Once you change the system disk, you have to deploy your runtime environment on the new system disk, which may cause prolonged interruption to business operations.

-   Once you change the system disk, a new system disk with a new disk ID is assigned. It means you cannot use all the snapshots of the original system disk to roll back the new system disk.

    **Note:** Changing a system disk has no effect on all the manual snapshots. You can use them to create custom images.  If you have applied automatic snapshot policies to the original system disk, and set the auto snapshots to be released with the disk, the snapshot policies cannot work any more and all the auto snapshots of the original system disk are deleted automatically.


**Considerations for changing between Windows and Linux**

Regions that are not in mainland China do not support replacement between Linux and Windows. 

**Note:** For instances in those regions, a Linux or Windows edition can be only replaced by another edition of the same operating system type.

After the OS is changed between Windows and Linux, the file systems of the data disks cannot be recognized.

-   If you do not have important data on the data disk, we recommend that you reinitialize the disk and format it to a recognizable file system.

-   If you have important data on the data disk, follow these tips:

    -   Replacing Windows with Linux: Install a software application, such as NTFS-3G, because the NTFS file system cannot be recognized by a Linux OS by default.
    -   Replacing Linux with Windows: Install a software application, such as Ext2Read or Ext2Fsd, because ext3, ext4, and xfs cannot be recognized by a Windows OS by default.

When you replace a Windows edition with a Linux edition, two authentication methods are available: a password and an SSH key pair.

## Prerequisites {#section_f2m_dkj_ydb .section}

Before replacing the existing image with a non-public image, complete the following:

-   To replace the existing image with a custom image:If you change to a custom mirror:

    -   To use an image running on an ECS instance,   create a snapshot for the system disk of the instance, and create a custom image from the snapshot.  If both the instances are not in the same region, copy the image.
    -   To use an on-premises image, import it in the ECS console or use Packer to create and import an image. The image and the instance must be in the same region.
    -   To use an image in a region other than that of the instance, copy the image.

        **Note:** When you change a system disk, all the images obtained by using the preceding methods are displayed in the drop-down list of **Custom Image**.

-   To use an image owned by other Alibaba Cloud account, share the image.

-   If you want to change the OS to a Linux edition and to use an SSH key pair as the authentication method, create an SSH key pair.


Changing a system disk is so highly risky that it may cause data loss and business interruption. To minimize the impact of the operation, we recommend that you create a snapshot for the system disk.

**Note:** 

-   We recommend that you create snapshots at off-peak business hours.  It may take about 40 minutes to create a snapshot of 40 GiB.  to create a snapshot of 40 GiB.  Therefore, leave sufficient time to create a snapshot. Creation of a snapshot may reduce the I/O performance of a block storage device, generally it is less than 10%, which results in sharp decrease in I/O speed.
-   To create a snapshot, make sure the system disk has sufficient space available. We recommend that at least 1 GiB storage space is reserved. Otherwise, the instance cannot be started after the system disk is changed.

## Procedure {#section_k2m_dkj_ydb .section}

1.  Log on to the [ECS console](https://ecs.console.aliyun.com/#/home).
2.  In the left-side navigation pane, click **Instances**.
3.  Select a region.
4.  Find an instance, and in the **Actions column**, select  **More** \> **Stop**.

    When the instance is in the **Stopped** status, 

5.  in the **Actions** column, select  **More** \> **Change System Disk**.
6.  In the dialog box, read the note and click **Yes. Change system disk**.
7.  On the Change System Disk page, complete the configurations:
    1.  **Image type**: Select **Custom Image**, **Shared Image** , or **Marketplace Image**, and select an image from the drop-down list.
    2.  **System Disk**: You cannot change the cloud disk category. However, you can change the size of the disk to meet the requirements of your system disk. The maximum size is 500  GiB.   The minimum size of the system disk is determined by the current size of the system disk and the image size.

        |Image|Size limit \(GiB\)|
        |:----|:-----------------|
        |Linux \(excluding CoreOS\) + FreeBSD|\[Max\{20, current size of the system disk\}, 500\]|
        |CoreOS|\[Max\{30, current size of the system disk\}, 500\]|
        |Windows|\[Max\{40, current size of the system disk\}, 500\]|

        **Note:**  If your instance was renewed for configuration downgrade, you cannot change the system disk size until the next billing cycle.

    3.  **Security**:
        -   If the new operating system is a Windows edition, a password is the only authentication method. 
        -   If you are changing the system disk of an I/O optimized instance, and the new operating system is a Linux edition, a password or an SSH key pair can be used as the authentication method. Set a password or bind an SSH key pair. 
    4.  Confirm the cost, which includes cost of the image and the system disk. For more information about pricing, see [Pricing of Elastic Compute Service](https://www.alibabacloud.com/zh/product/ecs#pricing).
    5.  Click **Confirm** to change and follow the prompts to complete the order.

Log on to the ECS console to monitor the system status. It may take about 10 minutes to change the system disk. After the system disk is changed, the instance starts automatically.

## Follow-up operations {#section_v2m_dkj_ydb .section}

After the system disk is changed, you may have to perform the following:

-   Optional. Apply an automatic snapshot policy to the new system disk. The auto-Snapshot policy is bound to the disk ID. The automatic snapshot policy applied on the old disk automatically fails after a new system disk has been replaced. You need to set up an automatic snapshot policy for the new system disk.

-   If the original operating system is a Linux edition, data disks are attached to the instance, and the disks are set to be mounted automatically at startup of the instance, all mounting information is lost.  Follow these steps to add new partition and mounting information to the /etc/fstab file. You do not have to partition or format the data disks again.  For more information, see  Linux \_ Format and mount a data disk.

    1.  Optional. Back up /etc/fstab.
    2.  Write new partition information to the /etc/fstab file.
    3.  Check new partition information in the /etc/fstab file.
    4.  Run `mount` to mount the partitions.
    5.  Run `df  -h` to check the file system space and usage.

        After the data partitions are mounted, the data disks are ready for use. You do not have to restart the instance.


## Related APIs {#section_y2m_dkj_ydb .section}

[ReplaceSystemDisk](../../../../intl.en-US/API Reference/Disk/ReplaceSystemDisk.md#)

