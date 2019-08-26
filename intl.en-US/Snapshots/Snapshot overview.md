# Snapshot overview {#concept_qft_2zw_ydb .concept}

A snapshot is a copy of the data stored on a cloud disk or on Shared Block Storage \(hereinafter referred to as disks\) at a specified point in time. A snapshot is commonly used to back up data, recover data, and create custom images.

**Note:** When you create a snapshot, the I/O performance of block storage will be degraded by less than 10%, resulting in an instantaneous I/O speed decrease. Therefore, we recommend that you create snapshots during off-peak hours.

## Scenarios {#section_vsk_hzw_ydb .section}

You can create snapshots in the following scenarios:

-   **Disaster backup**: [Create a snapshot for a disk](../../../../reseller.en-US/Snapshots/Use snapshots/Create a snapshot.md#) and use the snapshot as base data of another disk.

-   **Version rollback**: [Roll back a disk by using a snapshot](reseller.en-US/Snapshots/Use snapshots/Roll back a disk by using a snapshot.md#) if a system error occurs after an upgrade.

-   **Environment duplication**: If you want to purchase an instance that has the same environment as an existing instance, [create a custom image by using the system disk snapshot](../../../../reseller.en-US/Images/Custom image/Create custom image/Create a custom image by using a snapshot.md#) of the existing instance, and then [create an instance by using the custom image](../../../../reseller.en-US/Instances/Create an instance/Create an instance by using a custom image.md#).

-   **Data development**: By creating a snapshot of production data, you can provide near-real-time data for data mining, report query, and development, and testing applications.

-   **Data recovery and restoration**:

-   Use a snapshot to recover and restore the data on your disk even if incorrect data is mistakenly stored in the disk, your ECS instance is mistakenly released, an application error results in a data error, or your disk data is hacked.
-   Use a snapshot to regularly back up your critical service data on your disk to eliminate the risk of data loss resulting from incorrect operations, attacks, or virus.
-   Create one or more snapshots when you replace your OS, update your applications, or migrate your service data. This way you can use the snapshots to recover your system data if any failure occurs.

## Snapshot types {#section_xsk_hzw_ydb .section}

Snapshots can be categorized into the following types depending on the method to create them:

-   **Manual snapshot**: a snapshot that you manually create for a disk.
-   **Automatic snapshot**: a snapshot that is created automatically according to an automatic snapshot policy. You can create an automatic snapshot policy and apply it to a disk. For more information, see [Apply automatic snapshot policies to disks](reseller.en-US/Snapshots/Use snapshots/Apply automatic snapshot policies to disks.md#). Then, ECS will create snapshots automatically for the disk at specified points in time.

Snapshots can also be categorized into the following types depending on the portion of data contained within them:

-   **Full snapshot**: the first snapshot of a disk that contains the complete data.
-   **Incremental snapshot**: a subsequent snapshot after the first snapshot of a disk. An incremental snapshot contains the copied portion of changed data relative to the preceding snapshot. For more information, see [Snapshot concepts](reseller.en-US/Snapshots/Snapshot concepts.md#).

## Billing details {#section_zsk_hzw_ydb .section}

Currently, the snapshot service is provided free of charge.

## Service advantages {#section_j5r_krq_wgb .section}

The Alibaba Cloud snapshot service provides higher snapshot quotas and more flexible snapshot policies. The following table describes the user benefits and typical scenarios of the service.

|Item|Description|User benefit|Typical scenario|
|:---|:----------|:-----------|:---------------|
|Snapshot quota|Each disk has a quota of 64 snapshots.|Longer protection cycle with a finer granularity.| -   A non-critical service data disk creates a snapshot at 0:00 every day. The snapshot can store backup data of more than two months.

-   A critical service data disk creates a snapshot every four hours. The snapshot can store backup data of more than 10 days.


 |
|Automatic snapshot policy|You can customize when a snapshot is created, how often a snapshot is created in a week, and how long a snapshot is stored. You can also query the number and other details relating to the disks associated with automatic snapshot policies.|More flexible protection policies| -   You can select up to 24 specific hour intervals \(from 00:00 to 23:00\) at which an automatic snapshot is created in each day.

-   Snapshots can be created automatically on multiple days during a week.

-   Snapshots can be stored for a specified period of time or stored permanently. When the snapshot quota is reached, the system deletes the oldest snapshot automatically.


 |

## Technical advantages {#section_q5r_krq_wgb .section}

The following table describes the advantages of the Alibaba Cloud ECS snapshot service over traditional snapshot services.

|Metric|ECS snapshot service|Traditional snapshot service|
|:-----|:-------------------|:---------------------------|
|Capacity|Unlimited capacity, allowing you to protect all of your service data.|Limited capacity. Only the initially purchased storage capacity is available and only critical service data can be protected.|
|Scalability|Support for Auto Scaling. You can quickly scale in or scale out the number of storage devices in one click.|Lower scalability. Storage scaling is limited by the storage performance, available capacity, and vendor support.|
|Security|Encryption available. You can set ECS disk encryption whenever necessary to encrypt all of your disk snapshots. However, a non-encrypted snapshot cannot be converted to an encrypted snapshot. Similarly, an encrypted snapshot cannot be converted to a non-encrypted snapshot. For more information, see [ECS disk encryption](reseller.en-US/Block Storage/Block storage/ECS disk encryption.md#).|Encryption attributes and policies are dependent on the underlying storage logic. Therefore, if the storage architecture has a security design defect, any created snapshots may not be secure as a result.|
|Impact on performance|Redirect-On-Write \(ROW\) -   The impact of snapshot tasks on storage I/O performance is reduced.
-   Snapshots are invisible to users and can be created at any time without affecting user experience.

 |Copy-On-Write \(COW\), or other techniques such as ROW. COW has impact on the data write capability of the target system.|

