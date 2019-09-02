# General purpose {#concept_kmv_f1z_wgb .concept}

This topic describes the g5 and g6 general purpose instance families, and sn2ne general purpose instance family with enhanced network performance and lists their instance types.

## g6, general purpose instance family {#section_gck_bi6_q6l .section}

Features

-   Provides predictable stable and high performance and reduces virtualization overheads with the use of the X-Dragon architecture
-   I/O optimized
-   Supports enhanced SSDs, standard SSDs, and ultra disks
-   CPU-to-memory ratio of 1:4
-   Ultra high packet forwarding rate
-   Equipped with 2.5 GHz Second Generation Intel ® Xeon ® Scalable processors, up to 3.2 GHz Turbo Boost
-   Provides strong network performance based on sufficient computing capacity
-   Does not support instance upgrades or downgrades
-   Suitable for the following scenarios:
    -   Scenarios where large volumes of packets are received and transmitted, such as bullet screen and re-transmission of telecommunication information
    -   Enterprise-level applications of various types and sizes
    -   Websites and application servers
    -   Game servers
    -   Small and medium-sized database systems, cache, and search clusters
    -   Data analysis and computing
    -   Computing clusters and memory-intensive data processing

Instance types

|Instance type|vCPU|Memory \(GiB\)|Local storage \(GiB\)|Base bandwidth \(Gbit/s\)|Burstable bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|IPv6 support|NIC queue|ENI|Private IP address of a single ENI|Disk IOPS|Disk bandwidth \(Gbit/s\)|
|:------------|:---|:-------------|:--------------------|:------------------------|------------------------------|:------------------------------|:-----------|:--------|:--|----------------------------------|---------|-------------------------|
|ecs.g6.large|2|8.0|N/A|1.0|3.0|300|Yes|2|2|6|10,000|1|
|ecs.g6.xlarge|4|16.0|N/A|1.5|5.0|500|Yes|4|3|10|20,000|1.5|
|ecs.g6.2xlarge|8|32.0|N/A|2.5|8.0|800|Yes|8|4|10|25,000|2|
|ecs.g6.3xlarge|12|48.0|N/A|4.0|10.0|900|Yes|8|6|10|30,000|2.5|
|ecs.g6.4xlarge|16|64.0|N/A|5.0|10.0|1,000|Yes|8|8|20|40,000|3|
|ecs.g6.6xlarge|24|96.0|N/A|7.5|10.0|1,500|Yes|12|8|20|50,000|4|
|ecs.g6.8xlarge|32|128.0|N/A|10.0|N/A|2,000|Yes|16|8|20|60,000|5|
|ecs.g6.13xlarge|52|192.0|N/A|12.5|N/A|3,000|Yes|32|7|20|100,000|8|
|ecs.g6.26xlarge|104|384.0|N/A|25.0|N/A|6,000|Yes|32|15|20|200,000|16|

**Note:** 

-   您可以前往[ECS实例可购买地域](https://ecs-buy4service.aliyun.com/instanceTypes/#/instanceTypeByRegion)，查看本实例的可购情况。
-   For more information about these specifications, see [Instance specification metrics](reseller.en-US/Instances/Instance families.md#section_e9r_xkf_z15).

## g5, general purpose instance family {#section_kwi_d9k_sbx .section}

Features

-   I/O optimized
-   Supports enhanced SSDs, standard SSDs, and ultra disks
-   CPU-to-memory ratio of 1:4
-   Ultra high packet forwarding rate
-   Equipped with 2.5 GHz Intel ® Xeon ® Platinum 8163 \(Skylake\) processors
-   Provides strong network performance based on sufficient computing capacity
-   Suitable for the following scenarios:
    -   Scenarios where large volumes of packets are received and transmitted, such as bullet screen and re-transmission of telecommunication information
    -   Enterprise-level applications of various types and sizes
    -   Small and medium-sized database systems, cache, and search clusters
    -   Data analysis and computing
    -   Computing clusters and memory-intensive data processing

Instance types

|Instance type|vCPU|Memory \(GiB\)|Local storage \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|IPv6 support|NIC queue|ENI|Private IP address of a single ENI|
|:------------|:---|:-------------|:--------------------|:-------------------|:------------------------------|:-----------|:--------|:--|----------------------------------|
|ecs.g5.large|2|8.0|N/A|1.0|300|Yes|2|2|6|
|ecs.g5.xlarge|4|16.0|N/A|1.5|500|Yes|2|3|10|
|ecs.g5.2xlarge|8|32.0|N/A|2.5|800|Yes|2|4|10|
|ecs.g5.3xlarge|12|48.0|N/A|4.0|900|Yes|4|6|10|
|ecs.g5.4xlarge|16|64.0|N/A|5.0|1,000|Yes|4|8|20|
|ecs.g5.6xlarge|24|96.0|N/A|7.5|1,500|Yes|6|8|20|
|ecs.g5.8xlarge|32|128.0|N/A|10.0|2,000|Yes|8|8|20|
|ecs.g5.16xlarge|64|256.0|N/A|20.0|4,000|Yes|16|8|20|

**Note:** 

-   您可以前往[ECS实例可购买地域](https://ecs-buy4service.aliyun.com/instanceTypes/#/instanceTypeByRegion)，查看本实例的可购情况。
-   For more information about these specifications, see [Instance specification metrics](reseller.en-US/Instances/Instance families.md#section_e9r_xkf_z15).

## sn2ne, general purpose instance family with enhanced network performance {#section_1ki_kxs_w47 .section}

Features

-   I/O optimized
-   Supports standard SSDs and ultra disks
-   CPU-to-memory ratio of 1:4
-   Ultra high packet forwarding rate
-   Equipped with 2.5 GHz Intel ® Xeon ® E5-2682 v4 \(Broadwell\) or Platinum 8163 \(Skylake\) processors
-   Provides strong network performance based on sufficient computing capacity
-   Suitable for the following scenarios:
    -   Scenarios where large volumes of packets are received and transmitted, such as bullet screen and re-transmission of telecommunication information
    -   Enterprise-level applications of various types and sizes
    -   Small and medium-sized database systems, cache, and search clusters
    -   Data analysis and computing
    -   Computing clusters and memory-intensive data processing

Instance types

|Instance type|vCPU|Memory \(GiB\)|Local storage \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|IPv6 support|NIC queue|ENI|Private IP address of a single ENI|
|:------------|:---|:-------------|:--------------------|:-------------------|:------------------------------|:-----------|:--------|:--|----------------------------------|
|ecs.sn2ne.large|2|8.0|N/A|1.0|300|Yes|2|2|6|
|ecs.sn2ne.xlarge|4|16.0|N/A|1.5|500|Yes|2|3|10|
|ecs.sn2ne.2xlarge|8|32.0|N/A|2.0|1,000|Yes|4|4|10|
|ecs.sn2ne.3xlarge|12|48.0|N/A|2.5|1,300|Yes|4|6|10|
|ecs.sn2ne.4xlarge|16|64.0|N/A|3.0|1,600|Yes|4|8|20|
|ecs.sn2ne.6xlarge|24|96.0|N/A|4.5|2,000|Yes|6|8|20|
|ecs.sn2ne.8xlarge|32|128.0|N/A|6.0|2,500|Yes|8|8|20|
|ecs.sn2ne.14xlarge|56|224.0|N/A|10.0|4,500|Yes|14|8|20|

**Note:** 

-   您可以前往[ECS实例可购买地域](https://ecs-buy4service.aliyun.com/instanceTypes/#/instanceTypeByRegion)，查看本实例的可购情况。
-   For more information about these specifications, see [Instance specification metrics](reseller.en-US/Instances/Instance families.md#section_e9r_xkf_z15).

