# Local disks {#concept_g3w_qzv_tdb .concept}

Local disks are the disks attached to the physical servers \(host machines\) on which ECS instances are hosted. They are designed for business scenarios requiring high storage I/O performance. Local disks provide local storage and access for instances, and feature low latency, high random IOPS, high throughput, and cost-effective performance.

Because a local disk is attached to a single physical server, the data reliability depends on the reliability of the physical server, which may create single points of failure in your architecture. We recommend that you implement data redundancy at the application layer to guarantee data availability.

**Warning:** Using a local disk for data storage carries the risk of data loss \(for example, if the host machine is down\). Therefore, we recommend you never use a local disk to store any data that requires long-term persistence. If no data reliability architecture is available for your application, we strongly recommend that you build your ECS with [cloud disks or Shared Block Storage devices](reseller.en-US/Product Introduction/Block storage/Cloud disks and Shared Block Storage.md#).

This document details information about local disks and instances that support local disks. If you are using a previous generation local SSD disk, see [local SSD disks in the previous generation disks](https://partners-intl.aliyun.com/help/doc-detail/35241.htm).

## Disk types {#section_hdp_m2w_ydb .section}

Currently, Alibaba Cloud provides two types of local disks:

-   Local NVMe SSD: This disk is used together with instances of the following type families: i2, i1, and gn5. The instance type families i1 and i2 apply to the following scenarios:

    -   Online games, e-businesses, livestreaming, and other industries that provide online businesses and have low latency and high I/O performance requirements on block level storage for I/O-intensive applications.
    -   Business scenarios that have high requirements on the storage I/O performance and availability of the application layer, such as NoSQL non-relational databases, MPP data warehouses, and distributed file systems.
-   Local SATA HDD: This disk is used together with instances of the d1ne and d1 type families. It is applicable to businesses that require big data computing and storage analysis for massive data storage and offline computing business scenarios. It fully meets the needs of distributed computing business models \(such as those built on the Hadoop framework\) across instance storage performance, capacity, and intranet bandwidth.


## Performance of local NVMe SSD {#section_kdp_m2w_ydb .section}

The following table lists the performance of local NVMe SSD of an i1 ECS instance.

|Parameters|Local NVMe SSD|
|:---------|:-------------|
|Maximum capacity| Single disk: 1,456 GiB

 Total: 2,912 GiB

 |
|Maximum IOPS| Single disk: 240,000

 Total: 480,000

 |
|Maximum throughput| Read throughput per disk: 2 GBps

 Total read throughput: 4 GBps

 Write throughput per disk: 1.2 GBps

 Total write throughput: 2.4 GBps

 |
|Single-disk performance [\*](#singleDisk)|Write performance:-   Single-disk IOPS: IOPS = min\{165 \* capacity, 240,000\}
-   Single disk throughput: Throughput = min\{0.85 \* capacity, 1,200\} MBps

Read performance:-   Single disk IOPS: IOPS = min\{165 \* capacity, 240,000\}
-   Single disk throughput: Throughput = min\{1.4 \* capacity, 2,000\} MBps

|
|Access latency|Microsecond-level|

\* Single disk performance calculations are as follows:

-   Write IOPS for a single local NVMe SSD: 165 IOPS for each GiB, up to 240,000 IOPS.
-   Write throughput for a single local NVMe SSD: 0.85 MBps for each GiB, up to 1,200 Mbit/s.

## Performance of local SATA HDD {#section_qdp_m2w_ydb .section}

The following table lists the performance of local SATA HDD of a d1ne or d1 ECS instance.

|Parameters|Local SATA HDD|
|:---------|:-------------|
|Maximum capacity| Single disk: 5,500 GiB

 Total capacity per instance: 154,000 GiB

 |
|Maximum throughput| Single disk: 190 MBps

 Total throughput per instance: 5,320 MBps

 |
|Access latency|Millisecond-level|

## Billing {#section_sdp_m2w_ydb .section}

Local disks are charged according to the instances to which they are attached. For more information about instance billing methods, see [Subscription](../../../../reseller.en-US/Pricing/Subscription.md#) and [Pay-As-You-Go](../../../../reseller.en-US/Pricing/Pay-As-You-Go.md#).

## Lifecycle {#section_tdp_m2w_ydb .section}

A local disk has the same lifecycle as the instance that it is attached to. This means that:

-   You can create a local disk only when creating an instance that has local storage. The capacity of a local disk is determined by the ECS instance type. You cannot increase or decrease it.
-   When the instance is released, the local disk is released with it.

## Instance operations {#section_vdp_m2w_ydb .section}

The following table details how operations on an instance that has local storage affect the state of the data on the local disk.

|Operation|State of the data on the local disk|Result|
|:--------|:----------------------------------|:-----|
|Restart within the operating system/restart or force restart in the ECS console|Retained|Both the storage volumes and data on the local disk are retained.|
|Shutdown within the operating system/stop or force stop in the ECS console|Retained|Both the storage volumes and data on the local disk are retained.|
|Release in the ECS console|Erased|The storage volumes on the local disk are erased and the data on it is not retained.|
|Downtime migration|Erased|The storage volumes on the local disk are erased and the data on it is not retained.|
|Out-of-service \(before the computing resources of an instance is released\)|Retained|Both the storage volumes and data on the local disk are retained.|
|Out-of-service \(after the computing resources of an instance is released\)|Erased|The storage volumes on the local disk are erased and the data on it is not retained.|

## Related operations {#section_ydp_m2w_ydb .section}

If your ECS instance is attached with local disks, you must connect to the instance to [format the disk](../../../../reseller.en-US/Quick Start for Entry-Level Users/Step 4. Format a data disk/Format and mount data disks for Linux instances.md#). Unlike cloud disks, you cannot perform the following operations on local disks:

-   Independently create an empty local disk or create a local disk from a snapshot.
-   Attach a local disk in the ECS console.
-   Detach and release a local disk.
-   Increase the size of a local disk.
-   Re-initialize a local disk.
-   Create a snapshot for a local disk and use the snapshot to roll back the local disk.

