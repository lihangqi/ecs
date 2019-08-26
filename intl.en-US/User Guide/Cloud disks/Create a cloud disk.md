# Create a cloud disk {#concept_jx1_tx1_ydb .concept}

You can create a cloud disk to work as a data disk in the ECS console or by using the API. This article introduces how to create a new empty cloud disk in the ECS console.

## Notes {#section_twr_tx1_ydb .section}

Before you create a cloud disk, consider the following:

-   Only [Pay-As-You-Go](../../../../reseller.en-US/Pricing/Pay-As-You-Go.md#) cloud disks can be created in this way, and they can be used as data disks only.

    **Note:** You can create cloud disks as data disks when creating an ECS instance.  Those disks have the same billing method of the instance.

-   You can create a new empty cloud disk or [create a cloud disk from a snapshot](reseller.en-US/User Guide/Cloud disks/Create a cloud disk from a snapshot.md#).
-   The quota of the Pay-As-You-Go cloud disks that are used as data disks of each account in all regions is five times than that of the Pay-As-You-Go instances. For more information, see [limits](reseller.en-US/User Guide/Limits.md#).
-   Currently, you cannot merge multiple cloud disks. After cloud disks are created, they are independent from each other, and you cannot merge their space by formatting.  We recommend that you determine the number of disks and disk sizes required for your business before you create cloud disks.
-   Because you can create a snapshot for a single cloud disk, we do not recommend that you create LVM \(Logical Volume Manager\) volumes as the volumes may result in data loss if you use the snapshot to roll back the cloud disk.
-   You can convert a Pay-As-You-Go billed cloud disk to Subscription as follows:
    -   [Upgrade configurations of Subscription instances](reseller.en-US/User Guide/Instances/Change configurations/Upgrade configurations of Subscription instances.md#).
    -   [Switch from Pay-As-You-Go to subscription](../../../../reseller.en-US/Pricing/Switch from Pay-As-You-Go to Subscription billing.md#).
-   If a cloud disk is created in this way, and its billing method is retained as Pay-As-You-Go, you can [detach a cloud disk](reseller.en-US/User Guide/Cloud disks/Detach a cloud disk.md#) and [release a cloud disk](reseller.en-US/User Guide/Cloud disks/Release a cloud disk.md#) at any time.

## Prerequisites {#section_vzk_3z1_ydb .section}

If you want to [attach a cloud disk](reseller.en-US/User Guide/Cloud disks/Attach a cloud disk.md#) to an instance, make sure they are in the same region and zone.

## Procedure {#section_axr_tx1_ydb .section}

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, select **Block Storage** \> **Disks**.
3.  In the upper-right corner of the Disks list page, click **Create Disk** to go to the Create page.
4.  Select the target region and zone.

    **Note:** If you want to attach the cloud disk to an ECS instance, they must be in the same zone and the same region.

5.  Select a cloud disk category and specify the disk size and the quantity. You can also select [create a cloud disk from a snapshot](reseller.en-US/User Guide/Cloud disks/Create a cloud disk from a snapshot.md#).
6.  Confirm the configuration and the **Total** cost.
7.  Click **Preview**, confirm you order, and click **Create**.

After you complete the payment, return to the Disks page and refresh it. The new disk is displayed and its status is **Available**.

## Additional operations {#section_exr_tx1_ydb .section}

[Attach a cloud disk](reseller.en-US/User Guide/Cloud disks/Attach a cloud disk.md#).

## Related APIs {#section_gxr_tx1_ydb .section}

To create a disk after creating an instance, see [CreateDisk](../../../../reseller.en-US/API Reference/Disk/CreateDisk.md#).

To create a cloud disk when creating an instance, see [RunInstances](../../../../reseller.en-US/API Reference/Instances/RunInstances.md#) or [CreateInstance](../../../../reseller.en-US/API Reference/Instances/CreateInstance.md#).

