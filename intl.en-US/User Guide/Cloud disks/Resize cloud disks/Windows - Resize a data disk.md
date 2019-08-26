# Windows - Resize a data disk {#concept_rjc_l5h_ydb .concept}

As your business grows, the current capacity of your data disks may not be able to meet your data storage needs. You can use the **Resize Disk** function to resize your data disks as necessary.

**Note:** 

-   We recommend that you manually create a snapshot to back up your data before resizing a data disk.
-   You can resize a data disk when the data disk is either in the **Available** status or in the **In Use** status.
-   If a snapshot is being created for a data disk, you cannot resize the data disk.
-   If you have renewed a Subscription ECS instance for configration downgrade \([renew for configuration downgrade](../../../../../reseller.en-US/Pricing/Renew instances/Renew for configuration downgrade.md#)\) during its current billing cycle, you cannot resize the attached Subscription cloud disks, including its data or system disks.
-   You can resize data disks, but not file system.
-   You can resize data disks, but not system disks or local disks.
-   Resize the data disks that are attached to the instance only when the instance is in the **Running** \(`Running`\) or **Stopped** \(`Stopped`\) status. The changes are applied when you restart the instance in the ECS console. This action stops your instance from working and interrupts your business. Hence, proceed with caution.

This example uses a data disk of the ultra cloud disk type and an ECS instance running 64-bit Windows Server 2008 R2 Enterprise Edition to show how to resize a data disk and extend the available capacity. In this example, the current disk capacity is 20 GiB, and we resize it to 24 GiB.

To resize a data disk, follow these steps:

[Step 1. Resize a data disk in the ECS console](#)

[Step 2. Log on to the instance to enable the extended storage space](#)

## Step 1. Resize a data disk in the ECS console {#ResizeInConsole .section}

To resize a data disk in the ECS console, follow these steps:

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, select **Block Storage** \> **Disks**.

    **Note:** If the data disk you want to resize is attached to an instance, click **Instances** in the left-side navigation pane, find the instance, go to the Instance Details page, and then click **Disks**.

3.  Select a region.
4.  Find the disk to be resized, and in the **Actions** column, select **More** \> **Resize Disk**.
5.  On the Resize Disk page, set **Capacity after resizing**. In this example, 24 GiB. The capacity after resizing must be larger than the current capacity.
6.  When the cost is calculated, click **Confirm to resize**.

    **Note:** If your data disk is attached to an instance, [restart the instance](reseller.en-US/User Guide/Instances/Restart an instance.md#) in the ECS console to make the disk resize take effect.


Once the data disk resizing completes, you can do the following:

-   If the data disk is attached to an instance, [log on to the instance to enable the extended storage space](reseller.en-US/User Guide/Cloud disks/Resize cloud disks/Windows - Resize a data disk.md#ResizeInInstance).
-   If the data disk is not attached to an instance, attach the disk to an instance in the console first, and then proceed depending on the data disk:
    -   If it is not formatted or partitioned, format and mount the data disk. For more information, see [format a data disk for Windows instances](../../../../../reseller.en-US/Quick Start for Entry-Level Users/Step 4. Format a data disk/Format a data disk for Windows instances.md#).
    -   If it is formatted and partitioned, [log on to the instance to enable the extended storage space](reseller.en-US/User Guide/Cloud disks/Resize cloud disks/Windows - Resize a data disk.md#ResizeInInstance).

## Step 2. Log on to the instance to enable the extended storage space {#ResizeInInstance .section}

To resize a data disk within the instance, follow these steps:

1.  [Connect to a Windows instance](reseller.en-US/User Guide/Connect to instances/Connect to a Windows instance.md#).
2.  On the Windows Server desktop, click the Server Manager icon ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9678/15482306145356_en-US.png).
3.  In the left-side navigation pane of **Server Manager**, select **Storage** \> **Disk Management**. In the disk management area, you can see the relationship between the new and the original data disk spaces. In this example, **Disk 1** is the resized data disk. ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9678/154823061437961_en-US.png) 
4.  Right click an empty area of the **New Volume** of **Disk 1**, and select **Extend Volume**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9678/154823061437962_en-US.png)

5.  Follow the Extend Volume Wizard to extend the volume.

    When the wizard is complete, the new data disk space is automatically merged into the original volume and the **Disk 1** information showed in the Disk Manager as follows. 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9678/154823061437963_en-US.png)

    **Note:** On Windows Server 2003, the extended storage space is added to the data disk but it is displayed as a separate volume in Disk Manager. On Windows Server 2003, one separate volume is created for each expansion and is not merged into the original volume, which does not affect the availability of the extended storage space.


You have resized a data disk successfully and the extended storage space is ready for use.

