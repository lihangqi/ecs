# Compute optimized {#concept_w3g_z1z_wgb .concept}

This topic describes the ic5 compute-intensive instance family, c5 and c6 compute optimized instance families, and sn1ne compute optimized instance family with enhanced network performance and lists their instance types.

## ic5, compute-intensive instance family {#section_5hn_iox_k41 .section}

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

## c6, compute optimized instance family {#section_0yl_3wv_ims .section}

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

## c5, compute optimized instance family {#section_1zf_ox2_m08 .section}

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

## sn1ne, compute optimized instance family with enhanced network performance {#section_2mi_djo_dff .section}

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

