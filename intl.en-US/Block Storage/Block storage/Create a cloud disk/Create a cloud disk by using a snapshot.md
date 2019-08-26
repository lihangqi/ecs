# Create a cloud disk by using a snapshot {#concept_yyn_11b_ydb .concept}

This topic describes how to create a cloud disk by using a snapshot of a system disk or data disk in the ECS console. After you create a cloud disk, you can attach it to any ECS instance in the same zone of the same region. Note that a cloud disk created by a snapshot can only be used as a data disk.

## Scenarios {#section_bbc_ybb_ydb .section}

We recommend that you create a cloud disk by using a snapshot in the following scenarios:

-   If you need to obtain data from a snapshot, but you do not want to [roll back a cloud disk](reseller.en-US/Block Storage/Block storage/Roll back a cloud disk.md#).
-   If your instance encounters a system disk failure, you can use an existing system disk snapshot to create a cloud disk. Then, you can attach the cloud disk as a data disk to a healthy ECS instance so that you can continue to read the data of the system disk.

## Limits {#section_olo_310_40d .section}

-   By default, a cloud disk created by using a snapshot uses the [Pay-As-You-Go](../reseller.en-US/Pricing/Pay-As-You-Go.md#) billing method, and can only be used as a data disk. However, you can change the billing method of the cloud disk. For more information, see [What to do next](#section_pbc_ybb_ydb).
-   When you access a cloud disk created by a snapshot the first time, the performance is reduced because it takes some time for ECS to read data from OSS and write data to the cloud disk. Therefore, we recommend that you do not use the cloud disk until it has read from all data blocks. For more information, see [What is OSS?](../../../../../reseller.en-US/Product Introduction/What is OSS?.md#)
-   Across all regions, the number of Pay-As-You-Go data disks that you can create cannot be more than five times the number of Pay-As-You-Go instances under your account. For more information, see [Limits](../reseller.en-US/Product Introduction/Limits.md#).
-   You cannot merge multiple cloud disks by formatting them because they are independent of each other. Therefore, we recommend that you estimate the number and size of cloud disks required before you create them.
-   We recommend that you do not use Logical Volume Manager \(LVM\) to create logical volumes for multiple cloud disks. This is because a snapshot can only back up data of a single cloud disk. If you use LVM, data discrepancies will occur when you roll back these cloud disks.

## Prerequisites {#section_6wy_nxy_elm .section}

A system disk snapshot or a data disk snapshot is created and its ID is obtained. For more information, see [Create a snapshot](../reseller.en-US/Snapshots/Use snapshots/Create a snapshot.md#).

## Procedure {#section_lbc_ybb_ydb .section}

You can create a cloud disk through the ECS console or by calling [CreateDisk](../reseller.en-US/API Reference/Disk/CreateDisk.md#). To create a cloud disk through the ECS console, follow these steps:

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, choose **Storage & Snapshots** \> **Disks**.
3.  In the upper-right corner of the Disks page, click **Create Disk**.
4.  Select the target region and zone.

    **Note:** If you want to attach the cloud disk to an ECS instance, they must be in the same zone of the same region.

5.  Complete the following settings:
    1.  Select a disk type: **Ultra Disk**, **ESSD Cloud Disk**, or **SSD Cloud Disk**.
    2.  Click **Create from snapshot**, and then select a snapshot.
    3.  Set the capacity of the cloud disk. Note that it must be greater than 20 GiB and less than 32768 GiB.

        **Note:** 

        -   If you do not set the capacity of the cloud disk, the system automatically sets a capacity for the new cloud disk according to the cloud disk corresponding to the snapshot.
        -   If you set a capacity greater than the snapshot size, you must partition the cloud disk before you can use the full capacity.
        -   If the snapshot size is less than 2048 GiB and the cloud disk to be created is greater than 2048 GiB, you must ensure that the cloud disk corresponding to the snapshot uses GPT partitions \(Globally Unique Identifier Partition Table\). Otherwise, we recommend that you set the cloud disk size to less than 2048 GiB to avoid data loss that may occur in partitioning. For more information, see [Partition and format data disk more than 2 TiB](reseller.en-US/Block Storage/Block storage/Format a data disk/Partition and format data disk more than 2 TiB.md#).
    4.  Set the Quantity of cloud disks that you want to create.
    5.  Read and confirm that you agree with the **ECS Service Level Agreement** by selecting the check box.
6.  Confirm your settings and the estimated cost displayed.
7.  Click **Preview**, and then click **Create** in the displayed dialog box.

After you complete the payment, go back to the Disks page and refresh the disk list. The new disk is displayed in the **Unmounted** state.

## What to do next {#section_pbc_ybb_ydb .section}

After you create a cloud disk, you can:

-   [Attach the cloud disk](reseller.en-US/Block Storage/Block storage/Attach a cloud disk.md#).
-   Change the billing method of the cloud disk from Pay-As-You-Go to Subscription.
    -   If the cloud disk is attached to a Subscription instance, see [Upgrade configurations of Subscription instances](../reseller.en-US/Instances/Change configurations/Upgrade configurations/Upgrade configurations of Subscription instances.md#).
    -   If the cloud disk is attached to a Pay-As-You-Go instance, see [Switch from Pay-As-You-Go to Subscription billing](../reseller.en-US/Pricing/Switch from Pay-As-You-Go to Subscription billing.md#).

You can also create a cloud disk by using a system disk snapshot or a data disk snapshot when you [create an ECS instance](../reseller.en-US/Instances/Create an instance/Create an instance by using the wizard.md#). In this case, the cloud disk uses the same billing method as the ECS instance.

