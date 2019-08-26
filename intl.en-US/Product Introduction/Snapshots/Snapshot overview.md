# Snapshot overview {#concept_qft_2zw_ydb .concept}

A snapshot is a copy of data on a cloud disk or Shared Block Storage \(hereinafter referred to as disks\) at a specified time point. A snapshot is commonly used for data backup, disk recovery, replacing the operating system on an instance, and creating custom images.

**Note:** Creation of a snapshot may temporarily reduce the I/O performance of a block storage device \(generally by no more than 10%\), resulting in an instantaneous decrease in the I/O speed. In this case, we recommend that you create snapshots during off-peak hours.

## Scenarios {#section_vsk_hzw_ydb .section}

We recommend that you create snapshots for the following scenarios:

-   [Create a snapshot for a disk](../../../../reseller.en-US/User Guide/Snapshots/Create a snapshot.md#), whose data serves as the base data for another disk.

-   You want to [roll back the disk with the snapshot](../../../../reseller.en-US/User Guide/Cloud disks/Roll back a cloud disk.md#) when the data is corrupted. Cloud disks, including Basic Cloud Disks, Ultra Cloud Disks, and SSD Cloud Disks, are a secure means of storage that protects your data assets against loss. If incorrect data is accidentally stored on a disk, application errors lead to data errors, or hackers exploit vulnerabilities in your system and gain access to your data, you can use a snapshot to restore the target disk to a desired state.

-   If you want to purchase an instance that has the same environment as an existing instance, you can [create a custom image from the system disk snapshot](../../../../reseller.en-US/User Guide/Images/Create custom image/Create a custom image by using a snapshot.md#) of the existing instance, and then [create an instance with the custom image](../../../../reseller.en-US/User Guide/Instances/Create an instance/Create an instance from a custom image.md#).

-   Regularly back up critical business data on the system disk and data disk with snapshots, mitigating data loss resulting from misoperations, attacks, and viruses.

-   Before any important operations \(such as replacing operating systems, upgrading application software, or migrating business data\), we recommend that you create one or more snapshots. In the case of any problems during the upgrade or migration, you can use snapshots to restore the normal system data state in a timely manner.

-   By creating snapshots for the production data, you can provide nearly real-time production data for such applications as data mining, report query, as well as development and testing.


## Features {#section_usk_hzw_ydb .section}

Currently, Alibaba Cloud provides the Snapshot 2.0 service. Compared with the typical snapshot service, Snapshot 2.0 performs better in terms of capacity, scalability, cost-effectiveness, and usability. For more information, see ECS Snapshot 2.0 vs. traditional storage products. Unless otherwise specified, snapshots in all ECS topics refer to the Snapshot 2.0 service.

## Classification {#section_xsk_hzw_ydb .section}

Snapshots are classified into two categories:

-   Manual snapshots, which are created manually. You can create snapshots for a disk at any time.

-   Auto snapshots, which are created automatically according to the automatic snapshot policy. You can [create an automatic snapshot policy](../../../../reseller.en-US/User Guide/Snapshots/Create and delete an automatic snapshot policy.md#) and [apply it to the storage device](../../../../reseller.en-US/User Guide/Snapshots/Apply automatic snapshot policies to disks.md#). The snapshots will then be created automatically at the specified time points.


## Billing details {#section_zsk_hzw_ydb .section}

## Encryption {#section_btk_hzw_ydb .section}

In scenarios where disk encryption is required, you can set up ECS disk encryption. After that, all snapshots of the disks are encrypted as well. However, any existing snapshots that are not encrypted cannot be converted to encrypted snapshots, the converse scenario is also prohibited. For more information, see [ECS disk encryption](reseller.en-US/Product Introduction/Block storage/ECS disk encryption.md#).

## View the size of snapshots {#section_atk_hzw_ydb .section}

You can [view the total size of the snapshots of the disk](../../../../reseller.en-US/User Guide/Snapshots/View a snapshot chain.md#) by using the **Snapshot Chains** feature in the ECS console.

You can also view the total snapshot size in a region by using the **Snapshot Size** feature in the ECS console.

## Delete snapshots {#section_ctk_hzw_ydb .section}

If you no longer need a snapshot, you can [delete the snapshot](../../../../reseller.en-US/User Guide/Snapshots/Delete snapshots or automatic snapshot policies.md#) to guarantee a sufficient snapshot quota. If you have applied an automatic snapshot policy to the disk, you need to [delete the automatic snapshot policy](../../../../reseller.en-US/User Guide/Snapshots/Delete snapshots or automatic snapshot policies.md#).

