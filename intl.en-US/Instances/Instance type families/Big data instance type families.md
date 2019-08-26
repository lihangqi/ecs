# Big data instance type families {#concept_wsn_pcz_wgb .concept}

This topic describes the big data instance type family d1 and the big data instance type family with enhanced network performance d1ne, and lists the specific instance types within each instance type family.

## Overview {#section_b3z_bzs_qgb .section}

The big data instance type families d1 and d1ne are designed to compute and store massive amounts of data on the cloud, allowing you to achieve big data solutions at an enterprise level. Moreover, these instance family types can be used to build a Hadoop distributed computing architecture that is supplemented by self-hosted storage at your on-premises data center. This way, you can build a Hadoop cluster at costs similar to that of building a self-hosted cluster in your on-premises data center, while at the same time also guarantee increased storage space with improved performance.

d1ne and d1 instances have the following benefits:

-   Provide stable computing power by using enterprise-level architecture to ensure efficient processing of computing operations.
-   Achieve higher network performance \(specifically, greater maximum intranet bandwidth and packet forwarding rate per instance\) to achieve optimal data transfer among instances during peak periods.
-   Support 190 MiB/s of sequential read/write speeds for each disk and 5 GiB/s of storage throughput for each instance, reducing the overall HDFS file read/write time. Note that disks need to be fully initialized for optimal performance when an instance is newly created.
-   Provide local storage at a price 97% lower than that of SSD cloud disks, greatly reducing the cost to build a Hadoop cluster.

d1ne and d1 instances have the following limits:

-   The configurations of d1 and d1ne instances cannot be modified after they are created.
-   Downtime migration is not supported currently.
-   You cannot purchase a local disk separately. You can only purchase a local disk when you create a d1 or d1ne instance. The number and capacity of local disks that you can purchase is determined by the instance type you choose.
-   Snapshots are not supported currently. Therefore, if you need to create a full image for a d1 or d1ne instance, we recommend that you create one by combining the system disk snapshot and data disk \(only cloud disks are supported\) snapshots.
-   Currently you cannot create a full image based on an instance ID, so you cannot create a d1 or d1ne instance with a custom image either.
-   The data disks of d1 and d1ne instances are local disks that are subject to data loss. If your application cannot implement the data reliability architecture, we recommend the following:
    -   Use cloud disks for your instances, rather than local disks to store business data that needs to be stored long term.
    -   Back up your data regularly and adopt a high-availability architecture in which SSD cloud disks are attached your d1 and d1ne instances.
-   The following table shows how the operations on instances with local disks impact the disk data.

    |Operations|Status of disk data|Description|
    |----------|-------------------|-----------|
    |Restart the OS, restart an instance in the console, and force restart an instance|Retained|Local disk volumes and data are retained.|
    |Shut down the OS, stop an instance in the console, and force stop an instance|Retained|Local disk volumes and data are retained.|
    |Release an instance in the console|Erased|Local disk volumes and data are erased.|


## d1ne, big data type family with enhanced network performance {#section_xht_212_xgb .section}

**Features**

-   I/O-optimized
-   Supports SSD Cloud Disks and Ultra Disks
-   High-volume local SATA HDD disks with high I/O throughput and up to 35 Gbit/s of bandwidth for a single instance
-   Equipped with a vCPU to memory ratio of 1:4, designed for big data scenarios
-   Equipped with 2.5 GHz Intel Xeon E5-2682 v4 \(Broadwell\) processors
-   Supports strong network performance through sufficient computing capacity
-   Suitable for the following scenarios:
    -   Hadoop MapReduce, HDFS, Hive, HBase, and so on
    -   Spark in-memory computing, MLlib, and so on
    -   Enterprises that require big data computing and storage analysis, such as those in the Internet and finance industries, to store and compute massive volumes of data
    -   Elasticsearch, logs, and so on

**Instance types**

|Instance type |vCPU|Memory \(GiB\) |Local disks \(GiB\)[\*](reseller.en-US/Instances/Instance type families/Instance type families.md#)|Bandwidth \(Gbit/s\)[\*\*](reseller.en-US/Instances/Instance type families/Instance type families.md#) |Packet forwarding rate \(Thousand pps\)[\*\*\*](reseller.en-US/Instances/Instance type families/Instance type families.md#)|NIC queues[\*\*\*\*](reseller.en-US/Instances/Instance type families/Instance type families.md#)|ENIs[\*\*\*\*\*](reseller.en-US/Instances/Instance type families/Instance type families.md#)|
|:-------------|:---|:--------------|:-----------------------------------------|:---------------------------------------------|:-----------------------------------------------------------------|:--------------------------------------|:----------------------------------|
|ecs.d1ne.2xlarge|8|32.0|4 \* 5500|6.0|1,000|4|4|
|ecs.d1ne.4xlarge|16|64.0|8 \* 5500|12.0|1,600|4|8|
|ecs.d1ne.6xlarge|24|96.0|12 \* 5500|16.0|2,000|6|8|
|ecs.d1ne-c8d3.8xlarge|32|128.0|12 \* 5500|20.0|2,000|6|8|
|ecs.d1ne.8xlarge|32|128.0|16 \* 5500|20.0|2,500|8|8|
|ecs.d1ne-c14d3.14xlarge|56|160.0|12 \* 5500|35.0|4,500|14|8|
|ecs.d1ne.14xlarge|56|224.0|28 \* 5500|35.0|4,500|14|8|

**Note:** 

-   You cannot change configurations of d1ne instances.
-   For more information about d1ne type families, see [FAQ on d1 and d1ne](https://partners-intl.aliyun.com/help/faq-detail/52993.htm).

See [other instance type families](reseller.en-US/Instances/Instance type families/Instance type families.md#).

## d1, big data type family {#section_rgp_f12_xgb .section}

**Features**

-   I/O-optimized
-   Supports SSD Cloud Disks and Ultra Disks
-   High-volume local SATA HDD disks with high I/O throughput and up to 17 Gbit/s of bandwidth for a single instance
-   Equipped with a vCPU to memory ratio of 1:4, designed for big data scenarios
-   Equipped with 2.5 GHz Intel Xeon E5-2682 v4 \(Broadwell\) processors
-   Supports strong network performance through sufficient computing capacity
-   Suitable for the following scenarios:
    -   Hadoop MapReduce, HDFS, Hive, and HBase
    -   Spark in-memory computing and MLlib
    -   Enterprises that require big data computing and storage analysis, such as those in the Internet and finance industries, to store and compute massive volumes of data
    -   Elasticsearch and logs

**Instance types**

|Instance type |vCPU|Memory \(GiB\) |Local disks \(GiB\)[\*](reseller.en-US/Instances/Instance type families/Instance type families.md#)|Bandwidth \(Gbit/s\)[\*\*](reseller.en-US/Instances/Instance type families/Instance type families.md#) |Packet forwarding rate \(Thousand pps\)[\*\*\*](reseller.en-US/Instances/Instance type families/Instance type families.md#)|NIC queues[\*\*\*\*](reseller.en-US/Instances/Instance type families/Instance type families.md#)|ENIs[\*\*\*\*\*](reseller.en-US/Instances/Instance type families/Instance type families.md#)|
|:-------------|:---|:--------------|:-----------------------------------------|:---------------------------------------------|:-----------------------------------------------------------------|:--------------------------------------|:----------------------------------|
|ecs.d1.2xlarge|8|32.0|4 \* 5500|3.0|300|1|4|
|ecs.d1.3xlarge|12|48.0|16 \* 5500|4.0|400|1|6|
|ecs.d1.4xlarge|16|64.0|8 \* 5500|6.0|600|2|8|
|ecs.d1.6xlarge|24|96.0|12 \* 5500|8.0|800|2|8|
|ecs.d1-c8d3.8xlarge|32|128.0|12 \* 5500|10.0|1,000|4|8|
|ecs.d1.8xlarge|32|128.0|16 \* 5500|10.0|1,000|4|8|
|ecs.d1-c14d3.14xlarge|56|160.0|12 \* 5500|17.0|1,800|6|8|
|ecs.d1.14xlarge|56|224.0|28 \* 5500|17.0|1,800|6|8|

**Note:** For more information about d1 type families, see [FAQ on d1 and d1ne](https://partners-intl.aliyun.com/help/faq-detail/52993.htm).

See [other instance type families](reseller.en-US/Instances/Instance type families/Instance type families.md#).

