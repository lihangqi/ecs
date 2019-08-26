# Snapshot concepts {#concept_zbn_tzw_ydb .concept}

Alibaba Cloud ECS offers the snapshot service, which allows for the ability to create snapshots for cloud disks and Shared Block Storage \(hereinafter referred to as disks\) as scheduled operations. Such operations allow you to retain disk data at one or more specific points in time. Snapshots can effectively guarantee service security while also improving your overall application deployment efficiency.

## Incremental snapshots {#section_yvf_5zw_ydb .section}

After you format a disk, data blocks are divided based on Logical Blocking Addressing \(LBA\). All service data that is written in data blocks is measured by using snapshots. The first snapshot of a disk is a full snapshot that does not contain empty data blocks. Subsequent snapshots after the first snapshot are incremental snapshots, which are copies of service data and dirty data generated since the last snapshot. Therefore, each data block is copied multiple times and is stored across multiple snapshots. The following figure illustrates the preceding concepts. In the figure, snapshots 1, 2, and 3 represent the first, second, and third snapshots of a disk.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9575/15659412165243_en-US.jpg)

When a snapshot is created, the file system checks all data blocks, and only the data blocks with data changes are copied to the snapshot.

-   Snapshot 1 copies all data on the disk from a specific point in time.

-   Snapshot 2 copies only the changed data blocks B1 and C1. Data blocks A and D are taken from snapshot 1.

-   Snapshot 3 copies the changed data block B2. Data blocks A and D are taken from snapshot 1, and data block C1 from snapshot 2.

-   If you roll back the disk to snapshot 3, the **Roll Back Disk** feature simultaneously copies data blocks A, B2, C1, and D to the disk to replicate snapshot 3.

-   If you delete snapshot 2, data block B1 will be deleted, but data block C1 will be retained because data blocks that are taken by or from other snapshots will not be deleted. Therefore, if you roll back a disk to snapshot 3, data block C1 will be recovered.


## Snapshot chain {#SnapshotChain .section}

A snapshot chain contains all the snapshots of a disk. Each disk has a snapshot chain, whose ID is identical to the disk ID. A snapshot chain records the reference relationships among data blocks and contains the following information:

-   **Snapshot capacity**: the storage space occupied by all snapshots in the snapshot chain.

    **Note:** The snapshot service is billed by snapshot capacity. You can use the snapshot chain to check the snapshot capacity of each disk.

-   **Snapshot quota**: Each disk can have up to 64 snapshots. For more information, see [Limits](../../../../reseller.en-US/Product Introduction/Limits.md#).

    **Note:** If the snapshot quota is reached, but you need to create more automatic snapshots, the system will automatically delete automatic snapshots, starting with the oldest one first. If you want to create snapshots manually, then you must first delete unnecessary snapshots manually. For more information, see [Apply automatic snapshot policies to disks](../../../../reseller.en-US/Snapshots/Automatic snapshot policies/Apply or disable an automatic snapshot policy.md#) and [Delete snapshots or automatic snapshot policies](../../../../reseller.en-US/Snapshots/Use snapshots/Reduce snapshot fees.md#) in the *User Guide* .

-   **Snapshot node**: Each node in the snapshot chain represents a snapshot of a disk. Each snapshot chain can have up to 64 snapshot nodes, including both manual snapshots and automatic snapshots.


## Snapshot deletion {#section_dkx_mpl_xdb .section}

If you no longer need a snapshot, you can delete it. Note that if the number of snapshots exceeds the snapshot quota, you must delete some snapshots to release storage space. The following figure shows the workflow and logic for when you delete a snapshot from a snapshot chain. In this example, snapshot S1 is deleted.

![](https://gw.alipayobjects.com/zos/onekb/GEmePRxTvdRaZPCgtUhF.png)

1.  Alibaba Cloud ECS conducts an offline analysis on all the data blocks in snapshot S1 to be deleted, and then deletes the data blocks that are not taken by other snapshots in the snapshot chain.
2.  Alibaba Cloud ECS adds the dirty data blocks of snapshot S1 to snapshot S2. Other snapshots record the information of 10 data blocks altogether:
    -   Six of the data blocks of snapshot S0
    -   Two of the dirty data blocks of snapshot S1
    -   Two of the data blocks of snapshot S2

