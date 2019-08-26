# Create a cloud disk from a snapshot {#concept_yyn_11b_ydb .concept}

This article describes how to create a cloud disk from a snapshot in the ECS console. You can take a snapshot of an existing system disk, or data disk, and create a cloud disk from the snapshot. The new disk can be attached to any instance in the same zone of the same region. 

## Scenario {#section_bbc_ybb_ydb .section}

If you need to access data from a snapshot, but do not want to [roll back a cloud disk](reseller.en-US/User Guide/Cloud disks/Roll back a cloud disk.md#) , you can create a cloud disk from the snapshot to access data that you need. For example, if your instance encounters a system disk failure, you can use an existing snapshot to create a cloud disk, and attach the disk to a healthy instance. By doing so, you can restore the data of the affected instance.

## Disk Performance {#section_cbc_ybb_ydb .section}

If a cloud disk is created from a snapshot, the initial disk performance decreases because data needs to be accessed from OSS before being written into the disk. We recommend that you write and read every data block at least once before production use. For more information about OSS, see [what is OSS](../../../../reseller.en-US/Product Introduction/What is OSS?.md#).

## Considerations {#section_dbc_ybb_ydb .section}

-   Only [Pay-As-You-Go](../../../../reseller.en-US/Pricing/Pay-As-You-Go.md#) cloud disks can be created in this way, and they can only be used as data disks.

    **Note:** You can set cloud disks as data disks when creating an ECS instance. The disks then have the same billing method as that of the instance.

-   You can create a new empty cloud disk. For more information, see [create a cloud disk](reseller.en-US/User Guide/Cloud disks/Create a cloud disk.md#).
-   The quota of Pay-As-You-Go cloud disks that are used as data disks of each account in all regions is five times the quota of Pay-As-You-Go instances. For more information, see [limits](reseller.en-US/User Guide/Limits.md#).
-   Currently, you cannot merge multiple cloud disks. After cloud disks are created, they are independent from each other, and you cannot merge their space by formatting. We recommend that you confirm the amount and size required before you create cloud disks.
-   You can create a snapshot for a single cloud disk, so we do not recommend that you create LVM \(Logical Volume Manager\) volumes, which may cause data loss when you use the snapshot to rollback the cloud disk.
-   After a Pay-As-You-Go cloud disk is created, you can convert its billing method to Subscription:
    -   If it is attached to a Subscription instance, use the [upgrade configurations of Subscription instances](reseller.en-US/User Guide/Instances/Change configurations/Upgrade configurations of Subscription instances.md#) feature.
    -   If it is attached to a Subscription instance, use the [switch from Pay-As-You-Go to Subscription](../../../../reseller.en-US/Pricing/Switch from Pay-As-You-Go to Subscription billing.md#) feature.
-   If a cloud disk is created in this way, and its billing method is not converted, you can [detach a cloud disk](reseller.en-US/User Guide/Cloud disks/Detach a cloud disk.md#) and [release a cloud disk](reseller.en-US/User Guide/Cloud disks/Release a cloud disk.md#) at any time.

## Prerequisites {#section_hbc_ybb_ydb .section}

-   You have created a snapshot for your instance, and you make sure the region and zone. For specific actions, see [create snapshots](reseller.en-US/User Guide/Snapshots/Create a snapshot.md#).
-   [Attach a cloud disk](reseller.en-US/User Guide/Cloud disks/Attach a cloud disk.md#). The instance and the cloud disk must be in the same region and zone.

## Procedure {#section_lbc_ybb_ydb .section}

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, select **Block Storage** \> **Disks**.
3.  In the upper-right corner of the Disks list page, click **Create Disk**.
4.  Select a region and zone.

    **Note:** If you want to attach the cloud disk to an ECS instance, they must be in the same zone of the same region.

5.  Configure the cloud disk:
    1.  Select a cloud disk category. The category of the source disk of the snapshot does not modify the configuration.
    2.  Click **Create from snapshot** and select a snapshot.
    3.  Specify the size of the cloud disk. The size range is 20 GiB to 32768 GiB. If the selected snapshot is smaller than 20 GiB, you can adjust the size manually. For a snapshot larger than 20 GiB, the size is adjusted automatically according to the snapshot size. However, if you replace the snapshot, you must manually set the size.
    4.  For Purchase Plan, set the quantity.
6.  Check the cost.
7.  Click **Preview**, confirm you order, and click **Create**.

After you complete the payment, return to the Disks page and refresh it. The new disk is displayed and its status is **Available**.

## Additional operation {#section_pbc_ybb_ydb .section}

[Attach a cloud disk](reseller.en-US/User Guide/Cloud disks/Attach a cloud disk.md#).

## Related API {#section_qbc_ybb_ydb .section}

Create a cloud disk: [CreateDisk](../../../../reseller.en-US/API Reference/Disk/CreateDisk.md#)

