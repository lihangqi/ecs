# Increase system disk size {#concept_kj1_mqg_ydb .concept}

You can increase the size of the system disk of your ECS instance by using **Change System Disk** feature. This article describes how to increase the size of a system disk while keeping the operating system and environment intact.

**Note:** You can change the operating system while increasing the size of a system disk. For more information, see [change the operating system](reseller.en-US/User Guide/Instances/Change the operating system.md#).

## Notes {#section_bff_fwh_ydb .section}

Before you begin, consider the following.

**Risks**

Risks that may occur when you replace a system disk are as follows:

-   If you attempt to replace the system disk while the instance is running, your business services may be disrupted. We recommend you stop your instance before replacing the system disk.
-   After disk replacement, you must redeploy the business runtime environment on the new system disk. This may result in a long period of disruption to your business services.
-   After the system disk is changed, a new cloud disk with a new disk ID is assigned, and the old disk ID is released. Therefore, you cannot roll back the system disk by using any snapshot of the released cloud disk.

    **Note:** After the system disk is changed, you can still use manually created snapshots of the released disk to create custom images. If you have applied an automatic snapshot policy to the old system disk and set the automatic snapshots to release when the disk is released, you must apply the policy to the new disk. Furthermore, all the automatic snapshots of the old disk are released.


**Limits and recommendations**

When changing the system disk, you must consider the following:

-   After the system disk is changed, your instance is assigned a new cloud disk as the system disk, with a new disk ID, and the old one is released.
-   You cannot replace the Cloud Type of the system disk.
-   You cannot reduce the capacity of a system disk. You can only increase it. The maximum capacity of a system disk is 500 GiB.
-   You cannot increase the size of the system disk that runs Windows 2003.
-   If your Subscription instance has been [renewed for configuration downgrade](../../../../reseller.en-US/Pricing/Renew instances/Renew for configuration downgrade.md#), you cannot modify the system disk capacity until you enter the next billing cycle.
-   The IP address and the MAC address remain unchanged after the system disk is changed.
-   We recommend that you create a snapshot for the system disk before you change the disk. When creating a snapshot, consider the following:
    -   We recommend that you create snapshots during off-peak business hours as it may take an extended amount of time to complete. For example, it takes about 40 minutes to create a snapshot of 40 GiB. Creation of a snapshot may also reduce the I/O performance of a block storage device.
    -   Make sure the system disk has enough available storage space when creating a snapshot \(at least 1 GiB\). Otherwise, the system may fail to start after the system disk is changed.
-   To make sure you have enough quota for automatic snapshots of the new system disk, delete any unnecessary snapshots of the old system disk. For more information, see [delete snapshots or automatic snapshot policies](reseller.en-US/User Guide/Snapshots/Delete snapshots or automatic snapshot policies.md#).

## Procedure {#section_hff_fwh_ydb .section}

If you want to increase the size of the system disk while keeping the operating system and environment intact, follow these steps:

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, click **Instances**.
3.  Select the target region.
4.  Find the instance for which to change the system disk and click its instance ID to go to the Instance Details page.
5.  Follow these steps to create a snapshot of the system disk:
    1.  In the left-side navigation pane, click **Disks**.
    2.  Locate the required system disk and then, in the **Actions** column, click **Create Snapshot**.

        **Note:** For more information about the limits or note for creating a snapshot, see [create snapshots](reseller.en-US/User Guide/Snapshots/Create a snapshot.md#).

6.  Follow these steps to create a custom image by using the snapshot:
    1.  In the left-side navigation pane, click **Instance Snapshots** to check the creation status and progress. When the progress is 100% and the status is **Success**, go to the **Actions** column and click **Create Custom Image**.

        **Note:** 

        -   For more information about the limitations of creating a custom image, see [create a custom mirror using a snapshot](reseller.en-US/User Guide/Images/Create custom image/Create a custom image by using a snapshot.md#).
        -   The custom image is displayed in the dropdown ist of the **Custom Image** l on the Replace System Disk page.
    2.  Go back to the Instances page and then, in the left-side navigation pane, select **Snapshots and Images** \> **Image** to check the creation status and progress of the custom image.
7.  When the progress is 100% and the status is **Available**, in the left-side navigation pane, click **Instances**.
8.  In the Instances list, find the instance, and in the **Actions** column, select **More** \> **Instance Status** \> **Stop**.

    **Note:** For a Pay-As-You-Go VPC-Connected ECS instance, if the [No fees for stopped instances \(VPC-Connected\)](../../../../reseller.en-US/Pricing/No fees for stopped VPC instances.md#) feature is enabled, in the Notes dialog box, click **OK**. Then, in the Stop dialog box, select **Keep Stopped Instances and Continue Billing**, and click **OK**. If you use the **No Fees for Stopped Instances \(VPC-Connected\)**, you may not be able to start the instance successfully after changing the system disk.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9676/15432240115328_en-US.png)

9.  When the instance is in the **Stopped** status, go to the **Actions** column and select **More** \> **Disk and Image** \> **Replace System Disk**.
10. In the pop-up dialog box, read and confirm you agree to the notice by clicking **OK**.
11. On the Replace System Disk page, complete the configurations as follows:
    1.  **Image Type**: Click the **Custom Image** tab and select the created custom image in the drop-down list.
    2.  **Security enhancement**:
        -   **System Disk**: Specify a new size for the system disk according to your business needs. The maximum size is 500 GiB. The size limit for changing is determined by the image and the current size of the system disk, as displayed in the following table.

            |Image|Limit for capacity expansion \(GiB\)|
            |:----|:-----------------------------------|
            |Linux \(excluding CoreOS\) and FreeBSD|20-500|
            |CoreOS|30-500|
            |Windows|40-500|

            **Note:** You cannot modify the Cloud Type of the system tray.

        -   If a Windows image is used, set a logon password.
        -   If a Linux image is used and the instance is I/O optimized,  you can choose to set a password or bind an SSH key pair for logon.
    3.  Confirm the **Instance Cost**, which includes the price of the mirror and the price of the system disk.
    4.  Read and confirm you agree to the ECS Service Terms and Product Terms of Service, check the box, and then click **Confirm to change**.

Go back to the ECS console to check the status of the process. It may take a few minutes to process the change. After the system disk is changed, the instance starts automatically.

## Follow-up operations {#section_xff_fwh_ydb .section}

After the system disk is changed, you may have to perform the following:

-   If your instance is running a Linux image, and a data disk was attached to the instance and set to automatically mount the file systems at the beginning, the mount information is now lost while changing the system disk. Therefore, you must write the new partition and mounting information to the /etc/fstab file on the new system disk and mount the file systems. You must not partition or format the data disk again. For more information about the commands, see [Linux \_ Format and mount a data disk](../../../../reseller.en-US/Quick Start for Entry-Level Users/Step 4. Format a data disk/Format a data disk for Linux instance.md#). Follow these steps to mount the file systems:
    1.  \(Optional\) Create a backup of /etc/fstab file.
    2.  Write the new partition and mounting information to the /etc/fstab file.
    3.  Check the new partition information in the /etc/fstab file.
    4.  Mount the file systems.
    5.  To view disk space and usage: run the command `df -h`.

        After mounting, you do not need to restart the instance to use the new file system directly.

-    [Apply automatic snapshot policies to disks](reseller.en-US/User Guide/Snapshots/Apply automatic snapshot policies to disks.md#). Note that the link between an automatic snapshot policy ID and a disk ID is broken after the system disk is changed. You must set up an automatic snapshot policy for the new system disk.

