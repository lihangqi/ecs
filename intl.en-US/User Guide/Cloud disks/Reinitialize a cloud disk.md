# Reinitialize a cloud disk {#concept_stg_xd3_ydb .concept}

When a cloud disk is attached to an ECS instance, you can **reinitialize the disk** to restore the system disk or the data disks to the status when they were created. After a cloud disk is reinitialized:

-   The system disk is restored to the initial status when it was created. For example, if you select a public image to create an ECS instance, after the system disk is reinitialized, the operating system is retained, but all other applications that were installed after the instance creation are deleted.

    **Note:** After you change the operating system or resize the system disk, the instance is not fully restored to the status at which it was created, but only to the status of the new system disk when it was created.

-   Depending on how the data disk was created, it is restored to the following initial status:
    -   Restored to an empty disk if it was an empty disk
    -   Restored to a disk with only the data of the source snapshot if it was [created from a snapshot](reseller.en-US/User Guide/Cloud disks/Create a cloud disk from a snapshot.md#)
-   If an automatic snapshot policy is applied to a cloud disk, the policy is retained and does not need to be applied again after reinitialization.
-   If an automatic snapshot policy is applied to a cloud disk, the policy is retained and does not need to be applied again after reinitialization.
-   After a cloud disk is reinitialized, all the snapshots, both automatically and manually created, are retained. You can use them to [roll back a cloud disk](reseller.en-US/User Guide/Cloud disks/Roll back a cloud disk.md#).

**Warning:** 

-   Because you must stop your ECS instance to reinitialize a cloud disk, your business services may be disrupted. Exercise caution when performing this action
-   After a cloud disk is reinitialized, its data is lost. Therefore, we recommend you back up the data. To do so, you can [create snapshots](reseller.en-US/User Guide/Snapshots/Create a snapshot.md#).

## Reinitialize a system disk {#InitSys .section}

**Prerequisites**

If an SSH key pair is used as the authentication method, check that you have [created an SSH key pair](reseller.en-US/User Guide/Key pairs/Create an SSH key pair.md#) or [import ed an SSH key pair](reseller.en-US/User Guide/Key pairs/Import an SSH key pair.md#).

**Procedure**

To reinitialize a system disk, follow these steps:

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  Select the target region.
3.  In the left-side navigation pane, click **Instances**.
4.  Find the target ECS instance and click its ID to go to its Instance Details page.
5.  Click **Stop**.

    **Note:** For a Pay-As-You-Go VPC-Connected ECS instance, if the [No fees for stopped VPC instances](../../../../reseller.en-US/Pricing/No fees for stopped VPC instances.md#) feature is enabled, in the Notice dialog box, click **OK**, and then in the Stop dialog box, select **Keep Instance with Fees**. If you select the **No Fees for Stopped Instances \(VPC-Connected\)** mode, you may not be able to start the instance successfully after you reinitialize the system disk.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9676/15432250535328_en-US.png)

6.  After the instance is **stopped**, in the left-side navigation pane, click **Disks**.
7.  Find the system disk and then, in the **Actions** column, click **Reinitialize Disk**.
8.  In the Reinitialize Disk dialog box, complete the following configuration:
    1.  Authentication method:
        -   For a Windows instance, you must specify a logon password. You can either use a previous password or specify a new one.

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9679/154322505333021_en-US.jpg)

        -   For a Linux instance, select **Set SSH Key** or **Set Password** as the security setting. If Key Pair is selected, bind a key pair. If Password is selected, specify a logon password.

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9679/154322505333022_en-US.jpg)

    2.  \(Optional\) **Security Enhancement**: Select **Activate**. After the security enhancement feature is enabled, ECS security components are loaded. These components provide security features such as backdoor detection, remote logon reminders, brute-force cracking prevention mechanisms, and more.
    3.  \(Optional\) **Instance Startup**: Select **Start Instance Resetting Disk**. .
    4.  Click **Confirm**.
9.  For Linux instances: If you have attached a data disk to the instance, connect to the instance and [create a mounting point for the partitions of data disks](https://partners-intl.aliyun.com/help/faq-detail/40580.htm), because the mounting points are lost after the system disk is reinitialized.

    **Note:** For a Windows instance, both the system disk and the data disks are ready for use. No additional operations are needed.


After the system disk is reinitialized, you must deploy all applications to restore your business operations.

## Reinitialize a data disk {#InitData .section}

Once reinitialized, a data disk is in a different status according to its original status and the operating system of the instance:

-   For a Windows instance, the data disk is ready to use without any additional operations required.
-   For a Linux instance:
    -   If the data disk was an empty disk after it was created, then all the data and partitions on the disk are lost. You must partition and format the disk, and mount the partitions again.

        **Note:** If you configured the /etc/fstab file to automatically mount the disk partitions at startup of the instance, you must comment out the lines from the /etc/fstab file before reinitializing a data disk. Otherwise, your instance will fail to start.

    -   If the data disk was created from a snapshot, then the data disk is recovered to the point in time at which the snapshot was generated. You do not have to mount the partitions again, but all the data generated after the disk creation is lost.

In this section, /dev/vdb1 is the example partition and /InitTest is the example mounting point. Replace these details with your actual information.

**Prerequisites**

The data disk to be reinitialized must be attached to an ECS instance. For more information, see [attach a cloud disk](reseller.en-US/User Guide/Cloud disks/Attach a cloud disk.md#).

**Procedure**

To reinitialize a data disk, follow these steps:

1.  For Linux instances: If the data disk was an empty disk after it was created, and the mounting configuration was added to the /etc/fstab file, you must comment out the mounting configuration from the /etc/fstab file. To do so, follow these steps:
    1.  [Connect to the Linux instance](reseller.en-US/User Guide/Connect to instances/Overview.md#).
    2.  Run `vim /etc/fstab`.
    3.  Press the `i` key to enter the Insert mode.
    4.  Locate the mounting configuration lines and type \# before the lines. For example:

        ```
        # /dev/vdb1 /InitTest ext3 defaults 0 0
        ```

    5.  Press the `Esc` key to exit the Insert mode, and then run :wq to save and exit.
2.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
3.  In the left-side navigation pane, click **Instances**.
4.  Select the target region.
5.  Find the target ECS instance and click its ID to go to its Instance Details page.
6.  Click **Stop**.

    **Note:** For a Pay-As-You-Go VPC-Connected ECS instance, if the [No fees for stopped VPC instances](../../../../reseller.en-US/Pricing/No fees for stopped VPC instances.md#) feature is enabled, in the Notice dialog box, click **OK**, and then in the Stop dialog box, select **Keep Instance with Fees******. If you select the **No Fees for Stopped Instances \(VPC-Connected\)** mode, you may not be able to start the instance successfully after you reinitialize the system disk.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9676/15432250535328_en-US.png)

7.  After the instance is **stopped**, in the left-side navigation pane, click **Disks**.
8.  Find the target data disk and in the **Actions** column, click **Reinitialize Disk**.
9.  In the Reinitialize Disk dialog box, read the notes and click **Confirm**.
10. In the left-side navigation pane, click **Instance Details**.
11. Click **Start**.
12. For Linux instances: If the data disk was an empty disk after it was created, [format and mount data disks for Linux instances](../../../../reseller.en-US/Quick Start for Entry-Level Users/Step 4. Format a data disk/Format a data disk for Linux instance.md#).

After the data disk is reinitialized, you may need to deploy applications to restore your business operations.

## API {#section_yxg_323_ydb .section}

[ReInitDisk](../../../../reseller.en-US/API Reference/Disk/ReInitDisk.md#)

