# Replace the system disk \(public image\) {#concept_n4k_x3j_ydb .concept}

You can replace the system disk if you select an incorrect OS when creating an ECS instance or you need to replace the current OS. The new system disk will be allocated a new ID, and the previous system disk ID will be released.

You can replace the image of the system disk with a public image, shared image, customized image, or any other image from the Alibaba Cloud Marketplace.

**Note:** Microsoft has ended extended technical support for Windows Server 2003. For the purpose of data security, we recommend that you do not continue running Windows Server 2003 on your ECS instance. Its image is no longer provided. For more information, see [offline announcement of Windows Server 2003 system image](https://partners-intl.aliyun.com/help/faq-detail/59513.htm).

After you replace the system disk, note that:

-   A new system disk with a new disk ID is allocated to your instance, and the original ID is released.
-   The cloud type of the cloud disk cannot be replaced.
-   The IP address and the MAC address remain unchanged.
-   We recommend you [delete snapshots or automatic snapshot policies](reseller.en-US/User Guide/Snapshots/Delete snapshots or automatic snapshot policies.md#) to ensure sufficient snapshot quota for executing automatic snapshot policies of the new system disk.

This article describes how to replace an existing image with a public image. If you need to use a non-public image, see [replace the system disk \(non-public image\)](reseller.en-US/User Guide/Cloud disks/Replace the system disk (non-public image).md#).

## Precautions {#section_h1y_y3j_ydb .section}

Replacing the system disk exposes the system to multiple risks. Read the following precautions carefully before you begin:

**Risks**

The risks of replacing the system disk are as follows:

-   Replacing the system disk will stop your instances, which means your business services will be disrupted.

-   After replacing the system disk, you must redeploy the service running environment on the new system disk, which may result in a long interruption to services.

-   After you replace the system disk, a new system disk with a new disk ID will be assigned to your instance. This means that you cannot use snapshots of the original system disk to roll back the new system disk.

    **Note:** After you replace the system disk, the snapshots you have manually created are not affected. You can still use them to create customized images. If you have configured automatic snapshot policies for the original system disk to allow automatic snapshots to be released along with the disk, the snapshot policies no longer apply and all automatic snapshots of the original system disk will be automatically deleted.


**Precautions for cross-OS disk replacement**

Cross-OS disk replacement refers to replacing the system disk between Linux and Windows.

**Note:** Regions outside mainland China do not support disk replacement between Linux and Windows. Disk replacement between Linux editions or Windows editions are supported.

During cross-OS disk replacement, the file format of the data disk may be unidentifiable.

-   If no important data exists on the data disk, we recommend that you [reinitialize the disk](reseller.en-US/User Guide/Cloud disks/Reinitialize a cloud disk.md#) and format it to the default file system of your OS.

-   If important data exists in your data disk, perform the following actions as required:

    -   From Windows to Linux, you must install a software application, for example, NTFS-3G, because NTFS cannot be identified by Linux by default.
    -   From Linux to Windows, you must install a software application, for example, Ext2Read or Ext2Fsd, because ext3, ext4, and XFS cannot be recognized by Windows by default.

If you replace Windows with Linux, use a password or an SSH key pair for authentication.

## Preparations {#section_n1y_y3j_ydb .section}

-   Make sure that there is sufficient system disk space. We recommend that you reserve 1 GiB in case the OS cannot properly start after system disk replacement.

-   If you want to replace the OS to Linux and use an SSH key pair for authentication, [create an SSH key pair](reseller.en-US/User Guide/Key pairs/Create an SSH key pair.md#) first.

-   Replacing the system disk may cause data loss or service interruption. To minimize impact to your business services, we recommend that you [create snapshots](reseller.en-US/User Guide/Snapshots/Create a snapshot.md#) for the original system disk before replacement.

    **Note:** We recommend that you create snapshots during off-peak hours and plan for sufficient time. For example, to create a snapshot of 40 GiB for the first time, the process takes about 40 minutes. Additionally, creating a snapshot may reduce I/O performance of a block storage device by up to 10%.


## Procedure {#section_p1y_y3j_ydb .section}

To replace the system disk, follow these steps:

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left navigation pane, click **Instances**.
3.  Select the target region.
4.  In the **Actions** column of the target instance, select **More** \> **Instance Status** \> **Stop** and follow the instructions in the prompt to stop the instance.

    **Note:** If the instance is a Pay-As-You-Go instance using a VPC with the No Fees for Stopped Instances function enabled, in the displayed Notes dialog box, click **OK**. In the displayed Stop dialog box, select **Keep Stopped Instances and Continue Billing**. If you select **No Fees for Stopped Instances \(VPC-Connected\)**, the instance may not be properly started after system disk replacement.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9676/15508036635328_en-US.png)

5.  After the instance is stopped, in the **Actions** column, select **More** \> **Disk and Image** \> **Replace System Disk**.
6.  In the displayed dialog box, read the precautionary statement about system disk replacement and then click **OK**.
7.  On the Replace System Disk page, configure the following:
    1.  **Image Type**: Select **Public Image** and then select the image version.

        **Note:** If you need to use a non-public image, see [replace the system disk \(non-public image\)](reseller.en-US/User Guide/Cloud disks/Replace the system disk (non-public image).md#).

    2.  **System Disk**: Unchangeable. However, you can expand the disk space to meet the requirements of your system disk and services. The maximum disk space is 500 GiB. The minimum space of the system disk you can configured is determined by the current disk space and image type.

        |Image|Allowed range \(GiB\)|
        |:----|:--------------------|
        |Linux \(excluding CoreOS\) + FreeBSD|20-500|
        |CoreOS|30-500|
        |Windows|40-500|

        **Note:** If your instance has been configured with renewal for configuration downgrade, you cannot change the system disk space until the next billing cycle.

    3.  **Security enhancement**:
        -   If the new OS is Windows, you can only use a password for authentication.

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9682/15508036635517_en-US.png)

        -   If the instance is an I/O optimized instance, and the new OS is Linux, you can use either a password or an SSH key pair for authentication. In this case, we recommend you set a login password or bind an SSH key pair.

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9682/15508036635518_en-US.png)

    4.  Confirm **Instance Cost**, which includes the image fee and system disk fee. For more information about system disk price, see the pricing page of ECS.
    5.  Check the configuration and click **Confirm to change**.

Log on to the ECS console to monitor the system status. It may take about 10 minutes to replace the OS and update the system status. After the OS is replaced, the instance automatically starts.

## Additional operations {#section_bby_y3j_ydb .section}

After replacing the system disk, you can perform the following operations:

-   \(Optional\) [Apply automatic snapshot policies to disks](reseller.en-US/User Guide/Snapshots/Apply automatic snapshot policies to disks.md#). Automatic snapshot policies are bound to the disk ID. After the system disk is replaced, automatic snapshot policies applied on the original disk automatically fail. You need to configure automatic snapshot policies for the new system disk.

-   If the OS before and after disk replacement is Linux, and if a data disk is mounted to the instance and the partition is set to be mounted automatically at instance startup, then all mounting information will be lost. In this case, you need to write the new partition information into the /etc/fstab file of the new system disk and mount the partition, but do not need to partition or format the data disk for another time. The steps are described as follows. For more information about operation commands, see [format and mount data disks for Linux instances](../../../../../reseller.en-US/Quick Start for Entry-Level Users/Step 4. Format a data disk/Format a data disk for Linux instance.md#).

    1.  \(Recommended\) Back up the /etc/fstab file.
    2.  Write information about the new partition into the /etc/fstab file.
    3.  Check the information in the /etc/fstab file.
    4.  Run `mount` to mount the partition.
    5.  Run `df-h -h` to check the file system space and usage.

        After the data partition is mounted, the data disk is ready for use without the need for instance restart.


## Related API {#section_eby_y3j_ydb .section}

[ReplaceSystemDisk](../../../../../reseller.en-US/API Reference/Disk/ReplaceSystemDisk.md#)

