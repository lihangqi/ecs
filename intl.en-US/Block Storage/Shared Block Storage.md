# Shared Block Storage {#concept_abt_gpv_xgb .concept}

Shared Block Storage is a block-level storage device that supports concurrent read and write access from multiple ECS instances.

**Note:** Currently, Shared Block Storage is available only in public beta release. You can open a ticket to submit an application to join the testing group.

Shared Block Storage replicates data three times by default, and stores the data copies across different servers, to provide 99.9999999% data reliability for ECS instances. This means that if service disruptions occur \(for example, due to hardware failure\), Shared Block Storage can automatically copy your data within the target zone to help ensure data availability. You can partition and format Shared Block Storage attached to an ECS instance, and create a file system and store data on Shared Block Storage. For more information, see [Triplicate technology](Triplicate technologyEN-US_TP_9559.dita#concept_pnm_hdw_ydb).

**Note:** 

-   A single Shared Block Storage device can be attached to a maximum of eight ECS instances in the same zone and region at a time.
-   When attached to an ECS instance, Shared Block Storage shares the data disk quota with cloud disks, that is, up to 16 data disks can be attached to each ECS instance.
-   Shared Block Storage can only be created separately and used only as data disks.

## Background information {#section_c1n_z2w_xgb .section}

In a traditional cluster architecture, multiple computing nodes require access to the same copy of data so that the entire cluster can continue providing business services even when one or more computing nodes fail. If data files are stored in Shared Block Storage devices and these devices are managed through the cluster file system, data consistency can be guaranteed between multiple front-end computing nodes during concurrent read/write operations.

Shared Block Storage is designed for high-availability architectures required by enterprise-level applications.

## Limits {#section_fnr_hjr_f9t .section}

Before you use Shared Block Storage, note the following:

Shared Block Storage does not provide a cluster file system. However, you can install a cluster file system to manage Shared Block Storage. Specifically, you can use such cluster file systems as GFS and GPFS to manage Shared Block Storage. If your architecture is a typical Oracle RAC architecture, we recommend that you use ASM to manage storage volumes and data files.

If you use a traditional file system to manage Shared Block Storage that is attached to multiple ECS instances, the following two errors may occur:

-   Disk space allocation conflict

    If a Shared Block Storage device is attached to multiple instances and one of these instances \(for example, Instance A\) writes data to a file, Instance A checks the file system and available disk space. After the write operation is completed, the space allocation record of Instance A is changed, but the records of other instances are not updated. In this case, when another instance \(for example, Instance B\) tries to write data to the file, this instance may allocate the disk space that has been already allocated by Instance A, resulting in a disk space allocation conflict.

-   Data file inconsistency

    After an instance \(for example, Instance A\) reads and caches data, another process that accesses the same data will directly read the data from the cache. However, if a copy of the same data that is stored on another instance \(for example, Instance B\) is modified during this period, and Instance A does not update according to the latest data change, Instance A still reads the data from the cache. As a result, data inconsistency occurs.


## Types of Shared Block Storage {#sharedBlock .section}

The following table describes the available types of Shared Block Storage.

|Type|Description|
|:---|:----------|
|SSD|SSD Shared Block Storage, which uses SSDs as storage media to provide stable and high-performance storage with enhanced random I/O and data reliability.|
|Ultra|Ultra Shared Block Storage, which uses a combination of SSDs and HDDs as storage media.|

## Performance {#section_qhm_gfw_xgb .section}

For information about the performance indexes of Shared Block Storage, see [Block storage performance](reseller.en-US/Block Storage/Block storage performance.md#).

## Billing {#section_inz_nbw_ydb .section}

Currently, Shared Block Storage is available free of charge. We recommend that you check the official Alibaba Cloud website for the latest billing information.

