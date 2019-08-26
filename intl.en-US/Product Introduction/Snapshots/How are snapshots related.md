# How are snapshots related {#concept_zbn_tzw_ydb .concept}

Alibaba Cloud ECS provides a snapshot feature, which allows you to create snapshots of cloud disks and Shared Block Storage \(hereinafter referred to as disks\) as scheduled, thus retaining the data at one or more points in time for a disk. Snapshots effectively guarantee your business security and improve your application deployment efficiency.

## Incremental snapshot {#section_yvf_5zw_ydb .section}

In this method, two snapshots are compared and only the data that has changed is copied. As shown in the following figure, Snapshot 1, Snapshot 2, and Snapshot 3 are the first, second, and third snapshots of a disk. When a snapshot is created, only the blocks with changed data are copied to the snapshot. In this example:

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9575/15433015965243_en-US.jpg)

-   In Snapshot 1, all data on the disk is copied because it is the first snapshot.

-   Snapshot 2 only copies the changed data blocks B1 and C1. Data blocks A and D are referenced from Snapshot 1.

-   Snapshot 3 copies the changed data block B2, but references data blocks A and D from Snapshot 1, and block C1 from Snapshot 2.

-   If you want to roll back the disk to Snapshot 3, the **Disk Rollback** feature simultaneously copies blocks A, B2, C1, and D to the disk, thus replicating Snapshot 3.

-   If you delete Snapshot 2, block B1 is deleted, but block C1 is retained because blocks that are referenced by other snapshots cannot be deleted. This means that if you roll back a disk to Snapshot 3, block C1 is recovered.


## Snapshot chains {#SnapshotChain .section}

A snapshot chain contains all snapshots of a disk. Each disk has one snapshot chain, and the snapshot chain ID is identical to the disk ID. A snapshot chain records the reference relationships of data blocks. A snapshot chain has the following information:

-   Snapshot capacity, which is the storage space that all the snapshots in the chain occupy.

    **Note:** The snapshot service charges according to the snapshot capacity. You can use the snapshot chain to check the snapshot capacity of each disk.

-   Snapshot quota, whereby each disk can have a maximum of 64 snapshots. For more information, see [Limitations](../../../../reseller.en-US/User Guide/Limits.md#).

    **Note:** If the snapshot quota is reached, but you require more automatic snapshots to be created, the automatic snapshots are deleted automatically in chronological order. If you want to create more snapshots manually, you must delete unnecessary snapshots manually. For more information, see [Apply an automatic snapshot policy to a disk](../../../../reseller.en-US/User Guide/Snapshots/Apply automatic snapshot policies to disks.md#) and [Delete a snapshot](../../../../reseller.en-US/User Guide/Snapshots/Delete snapshots or automatic snapshot policies.md#) in the User Guide.

-   Snapshot node, whereby each node in the snapshot chain represents a snapshot of a disk. Each snapshot chain has a maximum of 64 nodes, including manually and automatically created snapshots.


