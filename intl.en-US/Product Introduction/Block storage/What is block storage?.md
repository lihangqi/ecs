# What is block storage? {#concept_pl4_tzb_wdb .concept}

## Overview {#section_n5b_jzv_ydb .section}

Block storage is a high-performance, low latency block storage service for Alibaba Cloud ECS. Similar to a hard disk, you can format block storage and create a file system on it to easily meet the data storage needs of your business.

Alibaba Cloud provides a variety of block-level storage products based on a distributed storage architecture and local disks located on the physical servers where ECS instances are hosted. Specifically, the storage products are as follows:

-   [Cloud Disk](reseller.en-US/Product Introduction/Block storage/Cloud disks and Shared Block Storage.md#), which is a block-level data storage product provided by Alibaba Cloud for ECS, uses a [multiple distributed system](reseller.en-US/Product Introduction/Block storage/Triplicate technology.md#), and features low latency, high performance, persistence, high reliability, and more. Cloud disks can be created, resized, and released at any time.

-   Shared block storage is a block-level data storage device that supports simultaneous read and write access to multiple ECS instances. Similar to the cloud disk, shared block storage uses a [multiple distributed system](reseller.en-US/Product Introduction/Block storage/Triplicate technology.md#). It supports simultaneous access to multiple instances, and features low latency, high performance, and high reliability. Shared Block Storage applies to shared access scenarios for block storage devices under a shared everything architecture.

-   Local disks are the disks attached to the physical servers \(host machines\) on which ECS instances are hosted. They are designed for business scenarios requiring high storage I/O performance and massive storage cost performance. Local disks provide local storage and access for instances, and features low latency, high random IOPS, high throughput, and cost-effective performance.

For more information about the performance of block-level storage products, see [Storage parameters and performance test](reseller.en-US/Product Introduction/Block storage/Storage parameters and performance test.md#).

## Block storage, OSS and NAS {#section_p5b_jzv_ydb .section}

Currently, Alibaba Cloud provides three types of data storage products: block storage, Object Storage Service \(OSS\), and Network Attached Storage \(NAS\).

the following three types of data storage products:

-   Block storage: A high-performance and low-latency block-level storage device for ECS. It supports random reads and writes. You can format block storage and create a file system on it as you would with a hard disk. , thereby enabling block storage to meet the data needs of numerous business scenarios.

-   OSS: A huge storage space designed for storing massive amounts of unstructured data on the Internet, including images, audio, and video. You can access the data stored in OSS anytime, anywhere, by using APIs. Generally, OSS is applicable to business scenarios as website construction, separation of dynamic and static resources, and CDN acceleration.

-   NAS: A storage space designed to store massive amounts of unstructured data that can be accessed by using standard file access protocols , such as the Network File System \(NFS\) protocol for Linux, and the Common Internet File System \(CIFS\) protocol for Windows. You can set permissions to allow different clients to access the same file at the same time. NAS is suitable for business scenarios such as file sharing across departments, non-linear file editing, high-performance computing, and containerization \(such as with Docker\).


