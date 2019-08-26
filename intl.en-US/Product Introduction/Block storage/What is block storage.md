# What is block storage {#concept_pl4_tzb_wdb .concept}

## Overview {#section_n5b_jzv_ydb .section}

Alibaba Cloud provides a wide variety of block-level storage products for your ECS, including elastic block storage based on the distributed storage architecture and local disks located on the physical server that an ECS instance is hosted on. Specifically:

-   [Elastic block storage](intl.en-US/Product Introduction/Block storage/Elastic block storage.md#), is a low-latency, persistent, and high-reliability random block-level data storage service provided by Alibaba Cloud to ECS users. It uses a [triplicate distributed system](intl.en-US/Product Introduction/Block storage/Triplicate technology.md#) to provide 99.9999999% data reliability for ECS instances. Elastic block storage can be created, released, and resized at any time.

-   [Local disks](intl.en-US/Product Introduction/Block storage/Local disks.md#) are the disks attached to the physical servers \(host machines\) that ECS instances are hosted on. They provide temporary block-level storage for instances, featuring low latency, high random IOPS, and high I/O throughput. They are designed for business scenarios requiring high storage I/O performance.


For more information about the performance of block-level storage products, see [Storage parameters and performance test](intl.en-US/Product Introduction/Block storage/Storage parameters and performance test.md#).

## Block storage, OSS, vs. NAS {#section_p5b_jzv_ydb .section}

Currently, Alibaba Cloud provides three types of data storage products, namely block storage, [Network Attached Storage \(NAS\)](https://www.alibabacloud.com/help/product/27516.htm) and [Object Storage Service \(OSS\)](https://www.alibabacloud.com/help/product/31815.htm).

The differences are as follows:

-   Block storage: A high-performance and low-latency block-level storage device provided by Alibaba Cloud to ECS users. It supports random reads/writes. You can format the block storage and create a file system on it like what you can do with a hard disk. It can be used for data storage in most common business scenarios.

-   OSS: You can treat it as a huge storage space, which is suitable for storing massive unstructured data, including images, short videos, and audios generated on the Internet. You can access the data stored in the OSS anytime and anywhere by using APIs. Generally, OSS is used for such business scenarios as Internet business website construction, separation of dynamic and static resources, and CDN acceleration.

-   NAS: Like OSS, it is suitable for storing massive unstructured data. But you must access the data by using standard file access protocols, such as the Network File System \(NFS\) protocol for the Linux system and the Common Internet File System \(CIFS\) protocol for the Windows system. You can set the permissions to allow different clients to access the same file at the same time.  NAS is applicable to such business scenarios as file sharing across departments, radio and television non-linear editing, high-performance computing, and Docker.


