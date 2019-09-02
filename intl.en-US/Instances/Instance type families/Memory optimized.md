# Memory optimized {#concept_mvj_hbz_wgb .concept}

This topic describes the r5 and r6 memory optimized instance families, re4 memory optimized instance family with enhanced performance, re4e memory optimized instance family with enhanced performance, se1ne memory optimized instance family with enhanced network performance, and se1 memory optimized instance family and lists their instance types.

## r6, memory optimized instance family {#section_qcw_6gn_p4u .section}

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

## r5, memory optimized instance family {#section_5vq_ldx_j20 .section}

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

## re4, memory optimized instance family with enhanced performance {#section_i3s_oh8_6q4 .section}

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

## re4e, memory optimized instance family with enhanced performance {#section_6zy_cbu_zum .section}

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

## se1ne, memory optimized instance family with enhanced network performance {#section_k1p_8hm_72f .section}

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

## se1, memory optimized instance family {#section_s5w_lh9_07j .section}

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

