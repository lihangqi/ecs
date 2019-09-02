# Instance families {#concept_sx4_lxv_tdb .concept}

This topic describes available ECS instance families and their features, specifications, and application scenarios.

An ECS instance is the smallest unit that can provide compute capabilities and services for your business.

ECS instances are categorized into different instance families based on the business scenarios to which they can be applied. Each instance family is divided into different instance types based on their CPU and memory specifications. ECS instance type defines the basic properties of an ECS instance: CPU \(including CPU model and clock speed\) and memory. In addition to the instance type, you must also configure the block storage, image, and network type when you create an instance.

**Note:** The available instance families and types varies from region to region. You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy4service.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.

Enterprise scenarios have high business stability requirements. Alibaba Cloud ECS instance families are divided into enterprise-level and entry-level based on whether the instance families are suitable for enterprise scenarios. Enterprise-level instance families offer consistent performance and dedicated resources. In enterprise-level instance families, each vCPU corresponds to an Intel Xeon core hyperthread.

**Note:** For the differences between enterprise-level and entry-level instance families, see [Instance FAQ](reseller.en-US/Instances/Instance FAQ.md#).

You can upgrade or downgrade instances within or between certain instance families. For such instance families and the corresponding upgrade and downgrade rules, see [Instance type families that support instance type upgrades](../../../../reseller.en-US/Instances/Change configurations/Instance type families that support instance type upgrades.md#).

Some instance families are no longer available for purchase. For more information, see [Phased-out instance types](reseller.en-US/Instances/Instance type families/Phased-out instance types.md#).

Alibaba Cloud ECS instances are categorized into the following instance families:

-   Enterprise-level computing instance families based on the x86 architecture:
    -   [g5, general purpose instance family](#)
    -   [g6, general purpose instance family](#)
    -   [sn2ne, general purpose instance family with enhanced network performance](#)
    -   [ic5, compute intensive instance family](#)
    -   [c5, compute optimized instance family](#)
    -   [c6, compute optimized instance family](#)
    -   [sn1ne, compute optimized instance family with enhanced network performance](#)
    -   [r5, memory optimized instance family](#)
    -   [r6, memory optimized instance family](#)
    -   [re4, memory optimized instance family with enhanced performance](#)
    -   [re4e, memory optimized instance family with enhanced performance](#)
    -   [se1ne, memory optimized instance family with enhanced network performance](#)
    -   [se1, memory optimized instance family](#)
    -   [d1ne, big data instance family with enhanced network performance](#)
    -   [d1, big data instance family](#)
    -   [i2, instance family with local SSDs](#)
    -   [i2g, instance family with local SSDs](#)
    -   [i1, instance family with local SSDs](#)
    -   [hfc5, compute optimized instance family with high clock speed](#)
    -   [hfg5, general purpose instance family with high clock speed](#)
-   Enterprise-level heterogeneous computing instance families:
    -   [vgn5i, lightweight compute optimized instance family with GPU capabilities](#)
    -   [gn6i, compute optimized instance family with GPU capabilities](#)
    -   [gn6v, compute optimized instance family with GPU capabilities](#)
    -   [gn5, compute optimized instance family with GPU capabilities](#)
    -   [gn5i, compute optimized instance family with GPU capabilities](#)
    -   [gn4, compute optimized family with GPU capabilities](#)
    -   [ga1, visualization and compute optimized instance family with GPU capabilities](#)
    -   [f1, compute optimized instance family with FPGAs](#)
    -   [f3, compute optimized instance family with FPGAs](#)
-   ECS Bare Metal Instance families and Super Computing Cluster \(SCC\) instance families:
    -   [ebmc5s, compute optimized ECS Bare Metal Instance family with enhanced network performance](#)
    -   [ebmg5s, general purpose ECS Bare Metal Instance family with enhanced network performance](#)
    -   [ebmr5s, memory optimized ECS Bare Metal Instance family with enhanced network performance](#)
    -   [ebmhfg5, ECS Bare Metal Instance family with high clock speed](#)
    -   [ebmc4, compute optimized ECS Bare Metal Instance family](#)
    -   [ebmg5, general purpose ECS Bare Metal Instance family](#)
    -   [scch5, SCC instance family with high clock speed](#)
    -   [sccg5, general purpose SCC instance family](#)
    -   [sccgn6, compute optimized SCC instance family with GPU capabilities](#)
-   Entry-level computing instance families based on the x86 architecture:
    -   [t5, burstable instance family](#)
    -   [xn4, previous-generation entry-level computing instance family](#)
    -   [n4, previous-generation entry-level computing instance family](#)
    -   [mn4, previous-generation entry-level computing instance family](#)
    -   [e4, previous-generation entry-level computing instance family](#)

## g5, general purpose instance family {#g5 .section}

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

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy4service.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Instance specification metrics](reseller.en-US/Instances/Instance families.md#section_e9r_xkf_z15).

## g6, general purpose instance family {#g6 .section}

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

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy4service.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Instance specification metrics](reseller.en-US/Instances/Instance families.md#section_e9r_xkf_z15).

## sn2ne, general purpose instance family with enhanced network performance {#sn2ne .section}

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

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy4service.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Instance specification metrics](reseller.en-US/Instances/Instance families.md#section_e9r_xkf_z15).

## ic5, compute-intensive instance family {#ic5 .section}

Features

-   I/O optimized
-   Supports enhanced SSDs, standard SSDs, and ultra disks
-   CPU-to-memory ratio of 1:1
-   Ultra high packet forwarding rate
-   Equipped with 2.5 GHz Intel ® Xeon ® Platinum 8163 \(Skylake\) processors
-   Provides strong network performance with large computing capacity
-   Suitable for the following scenarios:
    -   Web front-end servers
    -   Data analysis, batch compute, and video encoding
    -   Scenarios where large volumes of packets are received and transmitted, such as bullet screen and re-transmission of telecommunication information
    -   Massively Multiplayer Online \(MMO\) game frontends

Instance types

|Instance type|vCPU|Memory \(GiB\)|Local storage \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|IPv6 support|NIC queue|ENI|Private IP address of a single ENI|
|:------------|:---|:-------------|:--------------------|:-------------------|:------------------------------|:-----------|:--------|:--|----------------------------------|
|ecs.ic5.large|2|2.0|N/A|1.0|300|No|2|2|6|
|ecs.ic5.xlarge|4|4.0|N/A|1.5|500|No|2|3|10|
|ecs.ic5.2xlarge|8|8.0|N/A|2.5|800|No|2|4|10|
|ecs.ic5.3xlarge|12|12.0|N/A|4.0|900|No|4|6|10|
|ecs.ic5.4xlarge|16|16.0|N/A|5.0|1,000|No|4|8|20|

**Note:** 

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy4service.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Instance specification metrics](reseller.en-US/Instances/Instance families.md#section_e9r_xkf_z15).

## c5, compute optimized instance family {#c5 .section}

Features

-   I/O optimized
-   Supports enhanced SSDs, standard SSDs, and ultra disks
-   CPU-to-memory ratio of 1:2
-   Ultra high packet forwarding rate
-   Equipped with 2.5 GHz Intel ® Xeon ® Platinum 8163 \(Skylake\) processors
-   Provides strong network performance with large computing capacity
-   Suitable for the following scenarios:
    -   Scenarios where large volumes of packets are received and transmitted, such as bullet screen and re-transmission of telecommunication information
    -   Web front-end servers
    -   Massively Multiplayer Online \(MMO\) game frontends
    -   Data analysis, batch compute, and video encoding
    -   High-performance science and engineering applications

Instance types

|Instance type|vCPU|Memory \(GiB\)|Local storage \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|IPv6 support|NIC queue|ENI|Private IP address of a single ENI|
|:------------|:---|:-------------|:--------------------|:-------------------|:------------------------------|:-----------|:--------|:--|----------------------------------|
|ecs.c5.large|2|4.0|N/A|1.0|300|Yes|2|2|6|
|ecs.c5.xlarge|4|8.0|N/A|1.5|500|Yes|2|3|10|
|ecs.c5.2xlarge|8|16.0|N/A|2.5|800|Yes|2|4|10|
|ecs.c5.3xlarge|12|24.0|N/A|4.0|900|Yes|4|6|10|
|ecs.c5.4xlarge|16|32.0|N/A|5.0|1,000|Yes|4|8|20|
|ecs.c5.6xlarge|24|48.0|N/A|7.5|1,500|Yes|6|8|20|
|ecs.c5.8xlarge|32|64.0|N/A|10.0|2,000|Yes|8|8|20|
|ecs.c5.16xlarge|64|128.0|N/A|20.0|4,000|Yes|16|8|20|

**Note:** 

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy4service.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Instance specification metrics](reseller.en-US/Instances/Instance families.md#section_e9r_xkf_z15).

## c6, compute optimized instance family {#c6 .section}

Features

-   Provides predictable stable and high performance and reduces virtualization overheads with the use of the X-Dragon architecture
-   I/O optimized
-   Supports enhanced SSDs, standard SSDs, and ultra disks
-   CPU-to-memory ratio of 1:2
-   Ultra high packet forwarding rate
-   Equipped with 2.5 GHz Second Generation Intel ® Xeon ® Scalable processors, up to 3.2 GHz Turbo Boost
-   Provides strong network performance with large computing capacity
-   Does not support instance upgrades or downgrades
-   Suitable for the following scenarios:
    -   Scenarios where large volumes of packets are received and transmitted, such as bullet screen and re-transmission of telecommunication information
    -   Web front-end servers
    -   Massively Multiplayer Online \(MMO\) game frontends
    -   Data analysis, batch compute, and video encoding
    -   High-performance science and engineering applications

Instance types

|Instance type|vCPU|Memory \(GiB\)|Local storage \(GiB\)|Base bandwidth \(Gbit/s\)|Burstable bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|IPv6 support|NIC queue|ENI|Private IP address of a single ENI|Disk IOPS|Disk bandwidth \(Gbit/s\)|
|:------------|:---|:-------------|:--------------------|:------------------------|------------------------------|:------------------------------|:-----------|:--------|:--|----------------------------------|---------|-------------------------|
|ecs.c6.large|2|4.0|N/A|1.0|3.0|300|Yes|2|2|6|10,000|1|
|ecs.c6.xlarge|4|8.0|N/A|1.5|5.0|500|Yes|4|3|10|20,000|1.5|
|ecs.c6.2xlarge|8|16.0|N/A|2.5|8.0|800|Yes|8|4|10|25,000|2|
|ecs.c6.3xlarge|12|24.0|N/A|4.0|10.0|900|Yes|8|6|10|30,000|2.5|
|ecs.c6.4xlarge|16|32.0|N/A|5.0|10.0|1,000|Yes|8|8|20|40,000|3|
|ecs.c6.6xlarge|24|48.0|N/A|7.5|10.0|1,500|Yes|12|8|20|50,000|4|
|ecs.c6.8xlarge|32|64.0|N/A|10.0|N/A|2,000|Yes|16|8|20|60,000|5|
|ecs.c6.13xlarge|52|96|N/A|12.5|N/A|3,000|Yes|32|7|20|100,000|8|
|ecs.c6.26xlarge|104|192.0|N/A|25.0|N/A|6,000|Yes|32|15|20|200,000|16|

**Note:** 

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy4service.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Instance specification metrics](reseller.en-US/Instances/Instance families.md#section_e9r_xkf_z15).

## sn1ne, compute optimized instance family with enhanced network performance {#sn1ne .section}

Features

-   I/O optimized
-   Supports standard SSDs and ultra disks
-   CPU-to-memory ratio of 1:2
-   Ultra high packet forwarding rate
-   Equipped with 2.5 GHz Intel ® Xeon ® E5-2682 v4 \(Broadwell\) or Platinum 8163 \(Skylake\) processors
-   Provides strong network performance with large computing capacity
-   Suitable for the following scenarios:
    -   Scenarios where large volumes of packets are received and transmitted, such as bullet screen and re-transmission of telecommunication information
    -   Web front-end servers
    -   Massively Multiplayer Online \(MMO\) game frontends
    -   Data analysis, batch compute, and video encoding
    -   High-performance science and engineering applications

Instance types

|Instance type|vCPU|Memory \(GiB\)|Local storage \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|IPv6 support|NIC queue|ENI|Private IP address of a single ENI|
|:------------|:---|:-------------|:--------------------|:-------------------|:------------------------------|:-----------|:--------|:--|----------------------------------|
|ecs.sn1ne.large|2|4.0|N/A|1.0|300|Yes|2|2|6|
|ecs.sn1ne.xlarge|4|8.0|N/A|1.5|500|Yes|2|3|10|
|ecs.sn1ne.2xlarge|8|16.0|N/A|2.0|1,000|Yes|4|4|10|
|ecs.sn1ne.3xlarge|12|24.0|N/A|2.5|1,300|Yes|4|6|10|
|ecs.sn1ne.4xlarge|16|32.0|N/A|3.0|1,600|Yes|4|8|20|
|ecs.sn1ne.6xlarge|24|48.0|N/A|4.5|2,000|Yes|6|8|20|
|ecs.sn1ne.8xlarge|32|64.0|N/A|6.0|2,500|Yes|8|8|20|

**Note:** 

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy4service.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Instance specification metrics](reseller.en-US/Instances/Instance families.md#section_e9r_xkf_z15).

## r5, memory optimized instance family {#r5 .section}

Features

-   I/O optimized
-   Supports enhanced SSDs, standard SSDs, and ultra disks
-   Ultra high packet forwarding rate
-   Equipped with 2.5 GHz Intel ® Xeon ® Platinum 8163 \(Skylake\) processors
-   Provides strong network performance with large computing capacity
-   Suitable for the following scenarios:
    -   Scenarios where large volumes of packets are received and transmitted, such as bullet screen and re-transmission of telecommunication information
    -   High-performance and in-memory databases
    -   Data analysis and mining, and distributed memory cache
    -   Hadoop, Spark, and other memory-intensive enterprise applications

Instance types

|Instance type|vCPU|Memory \(GiB\)|Local storage \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|IPv6 support|NIC queue|ENI|Private IP address of a single ENI|
|:------------|:---|:-------------|:--------------------|:-------------------|:------------------------------|:-----------|:--------|:--|----------------------------------|
|ecs.r5.large|2|16.0|N/A|1.0|300|Yes|2|2|6|
|ecs.r5.xlarge|4|32.0|N/A|1.5|500|Yes|2|3|10|
|ecs.r5.2xlarge|8|64.0|N/A|2.5|800|Yes|2|4|10|
|ecs.r5.3xlarge|12|96.0|N/A|4.0|900|Yes|4|6|10|
|ecs.r5.4xlarge|16|128.0|N/A|5.0|1,000|Yes|4|8|20|
|ecs.r5.6xlarge|24|192.0|N/A|7.5|1,500|Yes|6|8|20|
|ecs.r5.8xlarge|32|256.0|N/A|10.0|2,000|Yes|8|8|20|
|ecs.r5.16xlarge|64|512.0|N/A|20.0|4,000|Yes|16|8|20|

**Note:** 

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy4service.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Instance specification metrics](reseller.en-US/Instances/Instance families.md#section_e9r_xkf_z15).

## r6, memory optimized instance family {#r6 .section}

Features

-   Provides predictable stable and high performance and reduces virtualization overheads with the use of the X-Dragon architecture
-   I/O optimized
-   Supports enhanced SSDs, standard SSDs, and ultra disks
-   Ultra high packet forwarding rate
-   Equipped with 2.5 GHz Second Generation Intel ® Xeon ® Scalable processors, up to 3.2 GHz Turbo Boost
-   Provides strong network performance with large computing capacity
-   Does not support instance upgrades or downgrades
-   Suitable for the following scenarios:
    -   Scenarios where large volumes of packets are received and transmitted, such as bullet screen and re-transmission of telecommunication information
    -   High-performance and in-memory databases
    -   Data analysis and mining, and distributed memory cache
    -   Hadoop, Spark, and other memory-intensive enterprise applications

Instance types

|Instance type|vCPU|Memory \(GiB\)|Local storage \(GiB\)|Base bandwidth \(Gbit/s\)|Burstable bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|IPv6 support|NIC queue|ENI|Private IP address of a single ENI|Disk IOPS|Disk bandwidth \(Gbit/s\)|
|:------------|:---|:-------------|:--------------------|:------------------------|------------------------------|:------------------------------|:-----------|:--------|:--|----------------------------------|---------|-------------------------|
|ecs.r6.large|2|16.0|N/A|1.0|3.0|300|Yes|2|2|6|10,000|1|
|ecs.r6.xlarge|4|32.0|N/A|1.5|5.0|500|Yes|4|3|10|20,000|1.5|
|ecs.r6.2xlarge|8|64.0|N/A|2.5|8.0|800|Yes|8|4|10|25,000|2|
|ecs.r6.3xlarge|12|96.0|N/A|4.0|10.0|900|Yes|8|6|10|30,000|2.5|
|ecs.r6.4xlarge|16|128.0|N/A|5.0|10.0|1,000|Yes|8|8|20|40,000|3|
|ecs.r6.6xlarge|24|192.0|N/A|7.5|10.0|1,500|Yes|12|8|20|50,000|4|
|ecs.r6.8xlarge|32|256.0|N/A|10.0|N/A|2,000|Yes|16|8|20|60,000|5|
|ecs.r6.13xlarge|52|384|N/A|12.5|N/A|3,000|Yes|32|7|20|100,000|8|
|ecs.r6.26xlarge|104|768.0|N/A|25.0|N/A|6,000|Yes|32|15|20|200,000|16|

**Note:** 

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy4service.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Instance specification metrics](reseller.en-US/Instances/Instance families.md#section_e9r_xkf_z15).

## re4, memory optimized instance family with enhanced performance {#re4 .section}

Features

-   I/O optimized
-   Supports standard SSDs and ultra disks
-   Optimized for high-performance databases, in-memory databases, and other memory-intensive enterprise applications
-   Equipped with 2.2 GHz Intel ® Xeon ® E7 8880 v4 \(Broadwell\) processors, up to 2.4 GHz Turbo Boost
-   CPU-to-memory ratio of 1:12, up to 1920.0 GiB memory
-   ecs.re4.20xlarge and ecs.re4.40xlarge have been certified by SAP HANA
-   Suitable for the following scenarios:
    -   High-performance databases and in-memory databases \(for example, SAP HANA\)
    -   Memory-intensive applications
    -   Big data processing engines such as Apache Spark or Presto

Instance types

|Instance type|vCPU|Memory \(GiB\)|Local storage \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|IPv6 support|NIC queue|ENI|Private IP address of a single ENI|
|:------------|:---|:-------------|:--------------------|:-------------------|:------------------------------|:-----------|:--------|:--|----------------------------------|
|ecs.re4.20xlarge|80|960.0|N/A|15.0|2,000|Yes|16|8|20|
|ecs.re4.40xlarge|160|1920.0|N/A|30.0|4,500|Yes|16|8|20|

**Note:** 

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy4service.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Instance specification metrics](reseller.en-US/Instances/Instance families.md#section_e9r_xkf_z15).

## re4e, memory optimized instance family with enhanced performance {#re4e .section}

Features

-   I/O optimized
-   Supports standard SSDs and ultra disks
-   Optimized for high-performance databases, in-memory databases, and other memory-intensive enterprise applications
-   Equipped with 2.2 GHz Intel ® Xeon ® E7 8880 v4 \(Broadwell\) processors, up to 2.4 GHz Turbo Boost
-   CPU-to-memory ratio of 1:24, up to 3840.0 GiB memory
-   Suitable for the following scenarios:
    -   High-performance databases and in-memory databases \(for example, SAP HANA\)
    -   Memory-intensive applications
    -   Big data processing engines such as Apache Spark or Presto

Instance types

|Instance type|vCPU|Memory \(GiB\)|Local storage \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|IPv6 support|NIC queue|ENI|Private IP address of a single ENI|
|:------------|:---|:-------------|:--------------------|:-------------------|:------------------------------|:-----------|:--------|:--|----------------------------------|
|ecs.re4e.40xlarge|160|3840.0|N/A|30.0|4,500|Yes|16|15|20|

**Note:** 

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy4service.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Instance specification metrics](reseller.en-US/Instances/Instance families.md#section_e9r_xkf_z15).

## se1ne, memory optimized instance family with enhanced network performance {#se1ne .section}

Features

-   I/O optimized
-   Supports standard SSDs and ultra disks
-   CPU-to-memory ratio of 1:8
-   Ultra high packet forwarding rate
-   Equipped with 2.5 GHz Intel ® Xeon ® E5-2682 v4 \(Broadwell\) or Platinum 8163 \(Skylake\) processors
-   Provides strong network performance with large computing capacity
-   Suitable for the following scenarios:
    -   Scenarios where large volumes of packets are received and transmitted, such as bullet screen and re-transmission of telecommunication information
    -   High-performance and in-memory databases
    -   Data analysis and mining, and distributed memory cache
    -   Hadoop, Spark, and other memory-intensive enterprise applications

Instance types

|Instance type|vCPU|Memory \(GiB\)|Local storage \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|IPv6 support|NIC queue|ENI|Private IP address of a single ENI|
|:------------|:---|:-------------|:--------------------|:-------------------|:------------------------------|:-----------|:--------|:--|----------------------------------|
|ecs.se1ne.large|2|16.0|N/A|1.0|300|Yes|2|2|6|
|ecs.se1ne.xlarge|4|32.0|N/A|1.5|500|Yes|2|3|10|
|ecs.se1ne.2xlarge|8|64.0|N/A|2.0|1,000|Yes|4|4|10|
|ecs.se1ne.3xlarge|12|96.0|N/A|2.5|1,300|Yes|4|6|10|
|ecs.se1ne.4xlarge|16|128.0|N/A|3.0|1,600|Yes|4|8|20|
|ecs.se1ne.6xlarge|24|192.0|N/A|4.5|2,000|Yes|6|8|20|
|ecs.se1ne.8xlarge|32|256.0|N/A|6.0|2,500|Yes|8|8|20|
|ecs.se1ne.14xlarge|56|480.0|N/A|10.0|4,500|Yes|14|8|20|

**Note:** 

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy4service.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Instance specification metrics](reseller.en-US/Instances/Instance families.md#section_e9r_xkf_z15).

## se1, memory optimized instance family {#se1 .section}

Features

-   I/O optimized
-   Supports standard SSDs and ultra disks
-   CPU-to-memory ratio of 1:8
-   Equipped with 2.5 GHz Intel ® Xeon ® E5-2682 v4 \(Broadwell\) processors
-   Provides strong network performance with large computing capacity
-   Suitable for the following scenarios:
    -   High-performance and in-memory databases
    -   Data analysis and mining, and distributed memory cache
    -   Hadoop, Spark, and other memory-intensive enterprise applications

Instance types

|Instance type|vCPU|Memory \(GiB\)|Local storage \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|IPv6 support|NIC queue|ENI|Private IP address of a single ENI|
|:------------|:---|:-------------|:--------------------|:-------------------|:------------------------------|:-----------|:--------|:--|----------------------------------|
|ecs.se1.large|2|16.0|N/A|0.5|100|No|1|2|6|
|ecs.se1.xlarge|4|32.0|N/A|0.8|200|No|1|3|10|
|ecs.se1.2xlarge|8|64.0|N/A|1.5|400|No|1|4|10|
|ecs.se1.4xlarge|16|128.0|N/A|3.0|500|No|2|8|20|
|ecs.se1.8xlarge|32|256.0|N/A|6.0|800|No|3|8|20|
|ecs.se1.14xlarge|56|480.0|N/A|10.0|1,200|No|4|8|20|

**Note:** 

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy4service.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Instance specification metrics](reseller.en-US/Instances/Instance families.md#section_e9r_xkf_z15).

## ebmc5s, compute optimized ECS Bare Metal Instance family with enhanced network performance {#ebmc5s .section}

Features

-   I/O optimized
-   Supports enhanced SSDs, standard SSDs, and ultra disks
-   CPU-to-memory ratio of 1:2
-   Equipped with 2.5 GHz Intel ® Xeon ® Platinum 8163 \(Skylake\) processors, 96 vCPUs, up to 2.7 GHz Turbo Boost
-   High network performance: 4.5 million pps packet forwarding rate
-   Supports VPC networks only
-   Provides dedicated hardware resources and physical isolation
-   Suitable for the following scenarios:
    -   Scenarios where large volumes of packets are received and transmitted, such as bullet screen and re-transmission of telecommunication information
    -   Workloads that require direct access to physical resources, or scenarios that require a license to be bound to the hardware
    -   Third-party virtualization \(includes but is not limited to Xen and KVM\), and AnyStack \(includes but is not limited to OpenStack and ZStack\)
    -   Containers \(includes but is not limited to Docker, Clear Containers, and Pouch\)
    -   Video encoding, decoding, and rendering

Instance types

|Instance type|vCPU|Memory \(GiB\)|Local storage \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|IPv6 support|NIC queue|ENI|Private IP address of a single ENI|
|:------------|:---|:-------------|:--------------------|:-------------------|:------------------------------|:-----------|:--------|:--|----------------------------------|
|ecs.ebmc5s.24xlarge|96|192.0|N/A|30.0|4,500|No|8|32|10|

**Note:** 

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy4service.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Instance specification metrics](reseller.en-US/Instances/Instance families.md#section_e9r_xkf_z15).

## ebmg5s, general purpose ECS Bare Metal Instance family with enhanced network performance {#ebmg5s .section}

Features

-   I/O optimized
-   Supports enhanced SSDs, standard SSDs, and ultra disks
-   CPU-to-memory ratio of 1:4
-   Equipped with 2.5 GHz Intel ® Xeon ® Platinum 8163 \(Skylake\) processors, 96 vCPUs, up to 2.7 GHz Turbo Boost
-   High network performance: 4.5 million pps packet forwarding rate
-   Supports VPC networks only
-   Provides dedicated hardware resources and physical isolation
-   Suitable for the following scenarios:
    -   Workloads that require direct access to physical resources, or scenarios that require a license to be bound to the hardware
    -   Third-party virtualization \(includes but is not limited to Xen and KVM\), and AnyStack \(includes but is not limited to OpenStack and ZStack\)
    -   Containers \(includes but is not limited to Docker, Clear Containers, and Pouch\)
    -   Enterprise-level applications, such as large and medium-sized databases
    -   Video encoding

Instance types

|Instance type|vCPU|Memory \(GiB\)|Local storage \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|IPv6 support|NIC queue|ENI|Private IP address of a single ENI|
|:------------|:---|:-------------|:--------------------|:-------------------|:------------------------------|:-----------|:--------|:--|----------------------------------|
|ecs.ebmg5s.24xlarge|96|384.0|N/A|30.0|4,500|No|8|32|10|

**Note:** 

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy4service.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Instance specification metrics](reseller.en-US/Instances/Instance families.md#section_e9r_xkf_z15).

## ebmr5s, memory optimized ECS Bare Metal Instance family with enhanced network performance {#ebmr5s .section}

Features

-   I/O optimized
-   Supports enhanced SSDs, standard SSDs, and ultra disks
-   CPU-to-memory ratio of 1:8
-   Equipped with 2.5 GHz Intel ® Xeon ® Platinum 8163 \(Skylake\) processors, 96 vCPUs, up to 2.7 GHz Turbo Boost
-   High network performance: 4.5 million pps packet forwarding rate
-   Supports VPC networks only
-   Provides dedicated hardware resources and physical isolation
-   Suitable for the following scenarios:
    -   Workloads that require direct access to physical resources, or scenarios that require a license to be bound to the hardware
    -   Third-party virtualization \(includes but is not limited to Xen and KVM\), and AnyStack \(includes but is not limited to OpenStack and ZStack\)
    -   Containers \(includes but is not limited to Docker, Clear Containers, and Pouch\)
    -   High-performance databases and in-memory databases
    -   Data analysis and mining and distributed memory cache
    -   Hadoop, Spark, and other memory-intensive enterprise applications

Instance types

|Instance type|vCPU|Memory \(GiB\)|Local storage \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|IPv6 support|NIC queue|ENI|Private IP address of a single ENI|
|:------------|:---|:-------------|:--------------------|:-------------------|:------------------------------|:-----------|:--------|:--|----------------------------------|
|ecs.ebmr5s.24xlarge|96|768.0|N/A|30.0|4,500|No|8|32|10|

**Note:** 

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy4service.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Instance specification metrics](reseller.en-US/Instances/Instance families.md#section_e9r_xkf_z15).

## ebmhfg5, ECS Bare Metal Instance family with high clock speed {#ebmhfg5 .section}

Features

-   I/O optimized
-   Supports standard SSDs and ultra disks
-   CPU-to-memory ratio of 1:4
-   Equipped with 3.7 GHz Intel ® Xeon ® E3-1240v6 \(Skylake\) processors, 8 vCPUs, up to 4.1 GHz Turbo Boost
-   High network performance: 2 million pps packet forwarding rate
-   Supports VPC networks only
-   Provides dedicated hardware resources and physical isolation
-   Does not support automatic recovery
-   Supports Intel ® SGX
-   Suitable for the following scenarios:
    -   Workloads that require direct access to physical resources, or scenarios that require a license to be bound to the hardware
    -   Gaming or finance applications requiring high performance
    -   High-performance Web servers
    -   Enterprise-level applications such as high-performance databases

Instance types

|Instance type|vCPU|Memory \(GiB\)|Local storage \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|IPv6 support|NIC queue|ENI|Private IP address of a single ENI|
|:------------|:---|:-------------|:--------------------|:-------------------|:------------------------------|:-----------|:--------|:--|----------------------------------|
|ecs.ebmhfg5.2xlarge|8|32.0|N/A|6.0|2,000|No|8|6|8|

**Note:** 

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy4service.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Instance specification metrics](reseller.en-US/Instances/Instance families.md#section_e9r_xkf_z15)v.

## ebmc4, compute optimized ECS Bare Metal Instance family {#ebmc4 .section}

Features

-   I/O optimized
-   Supports standard SSDs and ultra disks
-   CPU-to-memory ratio of 1:2
-   Equipped with 2.5 GHz Intel ® Xeon ® E5-2682 v4 \(Broadwell\) processors, up to 2.9 GHz Turbo Boost
-   High network performance: 4 million pps packet forwarding rate
-   Supports VPC networks only
-   Provides dedicated hardware resources and physical isolation
-   Suitable for the following scenarios:
    -   Workloads that require direct access to physical resources, or scenarios that require a license to be bound to the hardware
    -   Third-party virtualization \(includes but is not limited to Xen and KVM\), and AnyStack \(includes but is not limited to OpenStack and ZStack\)
    -   Containers \(includes but is not limited to Docker, Clear Containers, and Pouch\)
    -   Enterprise-level applications, such as large and medium-sized databases
    -   Video encoding

Instance types

|Instance type|vCPU|Memory \(GiB\)|Local storage \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|IPv6 support|NIC queue|ENI|Private IP address of a single ENI|
|:------------|:---|:-------------|:--------------------|:-------------------|:------------------------------|:-----------|:--------|:--|----------------------------------|
|ecs.ebmc4.8xlarge|32|64.0|N/A|10.0|4,000|No|8|12|10|

**Note:** 

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy4service.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Instance specification metrics](reseller.en-US/Instances/Instance families.md#section_e9r_xkf_z15).

## ebmg5, general purpose ECS Bare Metal Instance family {#ebmg5 .section}

Features

-   I/O optimized
-   Supports standard SSDs and ultra disks
-   CPU-to-memory ratio of 1:4
-   Equipped with 2.5 GHz Intel ® Xeon ® Platinum 8163 \(Skylake\) processors, 96 vCPUs, up to 2.7 GHz Turbo Boost
-   High network performance: 4 million pps packet forwarding rate
-   Supports VPC networks only
-   Provides dedicated hardware resources and physical isolation
-   Suitable for the following scenarios:
    -   Workloads that require direct access to physical resources, or scenarios that require a license to be bound to the hardware
    -   Third-party virtualization \(includes but is not limited to Xen and KVM\), and AnyStack \(includes but is not limited to OpenStack and ZStack\)
    -   Containers \(includes but is not limited to Docker, Clear Containers, and Pouch\)
    -   Enterprise-level applications, such as large and medium-sized databases
    -   Video encoding

Instance types

|Instance type|vCPU|Memory \(GiB\)|Local storage \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|IPv6 support|NIC queue|ENI|Private IP address of a single ENI|
|:------------|:---|:-------------|:--------------------|:-------------------|:------------------------------|:-----------|:--------|:--|----------------------------------|
|ecs.ebmg5.24xlarge|96|384.0|N/A|10.0|4,000|No|8|32|10|

**Note:** 

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy4service.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Instance specification metrics](reseller.en-US/Instances/Instance families.md#section_e9r_xkf_z15).

## scch5, SCC instance type family with high clock speed {#scch5 .section}

Features

-   I/O optimized
-   Supports only standard SSDs and ultra disks
-   Supports both RoCE and VPC networks, of which RoCE is dedicated to RDMA communication
-   With all features of ECS Bare Metal Instances
-   Equipped with 3.1 GHz Intel ® Xeon ® Gold 6149 \(Skylake\)
-   CPU-to-memory ratio of 1:3
-   Suitable for the following scenarios:
    -   Large-scale machine learning training
    -   Large-scale high performance scientific computing and simulations
    -   Large-scale data analysis, batch computing, and video encoding

Instance types

|Instance type|vCPU|Physical core|Memory \(GiB\)|GPU|Bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|RoCE \(Gbit/s\)|IPv6 support|NIC queue|ENI|Private IP address of a single ENI|
|:------------|:---|:------------|--------------|:--|:-------------------|:------------------------------|:--------------|:-----------|:--------|:--|----------------------------------|
|ecs.scch5.16xlarge|64|32|192.0|N/A|10.0|4,500|46|No|8|32|10|

**Note:** 

-   ecs.scch5.16xlarge provides 64 logical processors on 32 physical cores.
-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy4service.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Instance specification metrics](reseller.en-US/Instances/Instance families.md#section_e9r_xkf_z15).

## sccg5, general purpose SCC instance family {#sccg5 .section}

Features

-   I/O optimized
-   Supports only standard SSDs and ultra disks
-   Supports both RoCE and VPC networks, of which RoCE is dedicated to RDMA communication
-   With all features of ECS Bare Metal Instances
-   Equipped with 2.5 GHz Intel ® Xeon ® Platinum 8163 \(Skylake\) processors
-   CPU-to-memory ratio of 1:4
-   Suitable for the following scenarios:
    -   Large-scale machine learning training
    -   Large-scale high performance scientific computing and simulations
    -   Large-scale data analysis, batch computing, and video encoding

Instance types

|Instance type|vCPU|Physical core|Memory \(GiB\)|GPU|Bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|RoCE \(Gbit/s\)|IPv6 support|NIC queue|ENI|Private IP address of a single ENI|
|:------------|:---|:------------|--------------|:--|:-------------------|:------------------------------|:--------------|:-----------|:--------|:--|----------------------------------|
|ecs.sccg5.24xlarge|96|48|384.0|N/A|10.0|4,500|46|No|8|32|10|

**Note:** 

-   ecs.sccg5.24xlarge provides 96 logical processors on 48 physical cores.
-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy4service.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Instance specification metrics](reseller.en-US/Instances/Instance families.md#section_e9r_xkf_z15).

## sccgn6, compute optimized SCC GPU instance family {#sccgn6 .section}

Features

-   I/O-optimized
-   CPU-to-memory ratio of 1:4
-   Equipped with 2.5 GHz Intel ® Xeon ® Platinum 8163 \(Skylake\) processors
-   With all features of ECS Bare Metal Instances
-   Storage:
    -   Supports enhanced SSDs \(million-level IOPS\), standard SSDs, and ultra disks
    -   Supports high performance Cloud Parallel File System \(CPFS\)
-   Networking:
    -   Supports VPC networks equipped with two 25 Gbps ports
    -   Supports RoCE v2 networks, which is dedicated to RDMA communication
-   Uses NVIDIA V100 GPU processors \(with the SXM2 module\):
    -   Based on the new NVIDIA Volta architecture
    -   16 GB HBM2 memory capacity
    -   Up to 5,120 CUDA Cores
    -   Up to 640 Tensor Cores
    -   Offers a 900 GB/s memory bandwidth
    -   Supports up to six NVLink connections and total bandwidth of 300 GB/s \(25 GB/s per connection\)
-   Suitable for the following scenarios:
    -   Ultra-large-scale machine learning training on a distributed GPU cluster
    -   Large-scale high performance scientific computing and simulations
    -   Large-scale data analysis, batch computing, and video encoding

Instance types

|Instance type|vCPU|Memory \(GiB\)|Local storage \(GiB\)|GPU|Bandwidth \(Gbit/s\)|Packet forwarding rate \(Kpps\)|RoCE \(Gbit/s\)|IPv6 support|NIC queue|ENI|Private IP address of a single ENI|
|:------------|:---|:-------------|:--------------------|:--|:-------------------|:------------------------------|---------------|:-----------|:--------|:--|----------------------------------|
|ecs.sccgn6.24xlarge|96|384|N/A|8 × V100|30|4,500|2 × 25|Yes|8|32|10|

**Note:** 

-   You can go to the [ECS Instance Types Available for Each Region page](https://ecs-buy4service.aliyun.com/instanceTypes/#/instanceTypeByRegion) to view the instance types available in each region.
-   For more information about these specifications, see [Instance specification metrics](reseller.en-US/Instances/Instance families.md#section_e9r_xkf_z15).

## Instance specification metrics {#section_e9r_xkf_z15 .section}

|Metric|Description|
|------|-----------|
|Local storage|Local storage, also called cache disks or local disks, refers to the disks attached to the physical servers where ECS instances are hosted. Local storage provides temporary block storage for instances. Local storage capacity is measured in GiB. Data stored in the local disks may be lost in some cases, such as when the compute resources \(vCPU and memory\) of an instance are released or an instance is migrated because the physical server is down. For more information, see [Local disks](../../../../reseller.en-US/Block Storage/Local disks.md#).|
|Bandwidth|The maximum bandwidth in one direction. Inbound bandwidth and outbound bandwidth are calculated separately.|
|Packet forwarding rate|The maximum sum of inbound and outbound packet forwarding rates. For details about how to test the packet forwarding rate, see [Test network performance](https://partners-intl.aliyun.com/help/faq-detail/55757.htm).|
|NIC queues|The maximum number of NIC queues that the primary NIC of an instance supports. If your instance type is not of an ECS Bare Metal Instance family, the maximum number of NIC queues supported by the secondary NIC is the same as that supported by the primary NIC.|
|ENIs|Enterprise-level instance types that are equipped with two or more vCPU cores support Elastic Network Interfaces \(ENIs\). Entry-level instance types that are equipped with four or more vCPU cores support ENIs. For more information, see [ENI overview](../../../../reseller.en-US/Network/Elastic Network Interfaces/ENI overview.md#).|

