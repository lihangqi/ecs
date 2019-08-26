# View a snapshot chain {#concept_w51_1rl_xdb .concept}

The snapshot service fee is related to the snapshot size. This article describes how to view the snapshot size on a single disk or under a region.

## View the snapshot size on a single disk {#section_cx4_3rl_xdb .section}

When you create snapshots of a cloud disk or a shared block storage device, you can view the snapshot size of the device by using the **Snapshot Chains** feature in the ECS console.

A snapshot chain is composed of all the snapshots of a cloud disk or shared block storage device. After you create a snapshot, the device has a snapshot chain. The snapshot chain uses an identical ID with that of the disk, and provides the following information:

-   Snapshot nodes, whereby each snapshot node of the chain represents one snapshot of the device.
-   Snapshot size, indicating the storage space occupied by all snapshots of the device.
-   Snapshot quota, whereby each device can have up to 64 snapshots, including those created manually or automatically.

## Prerequisite {#section_gfm_srl_xdb .section}

You have [created snapshots](reseller.en-US/User Guide/Snapshots/Create a snapshot.md#).

## Procedure {#section_a25_trl_xdb .section}

To view the total size of all the snapshots of a cloud disk or shared block storage device, follow these steps:

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  Select the target region.
3.  In the left-side navigation pane, select **Snapshots and Images** \> **Snapshots** .
4.  Find the disk ID of the target snapshot.
5.  In the left-side navigation pane, click **Snapshot Chains**.
6.  View the size of all snapshots on the disk according to the disk ID found in step 4. You can view the total number and size of snapshots of the disk in the list.

In the **Actions** column, click **Details** to go to the Snapshot Chain Details page to see all snapshots of the disk. Here, you can choose to [roll back a cloud disk](reseller.en-US/User Guide/Cloud disks/Roll back a cloud disk.md#) or [create a custom image by using a snapshot](reseller.en-US/User Guide/Images/Create custom image/Create a custom image by using a snapshot.md#).

## View the snapshot size under a region {#section_sbv_2sl_xdb .section}

Follow these steps:

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  Select the target region.
3.  In the left-side navigation pane, select **Snapshots and Images** \> **Snapshots**.

Here, you can view the total number and size of snapshots of the disk in the list.

