# Instance type families {#concept_sx4_lxv_tdb .concept}

This topic describes the available ECS instance type families.

An ECS instance is the minimal unit that can provide computing capabilities and services for your business.

ECS instances are categorized into specification types, which are called type families, based on the business scenarios they can be applied to. You may select multiple type families for one business scenario. Each type family contains multiple ECS instance types with different CPU and memory specifications, including the CPU model and clock speed. Besides the instance type, you must also define a block storage, an image, and the network service when you create an instance.

**Note:** The availability of instance type families and their types varies from region to region. Go to the purchase page to check the available instance types.

Alibaba Cloud ECS provides two kinds of instance type families: enterprise-level instance type families and entry-level instance type families. Type families for enterprise-level computing offer stable performance and dedicated resources, while entry-level type families are ideal for small and mid-sized websites, or individual customers. For the differences, see [Enterprise-level instances and entry-level instances FAQ](https://partners-intl.aliyun.com/help/faq-detail/44078.htm).

**Note:** 

-   Some instance types are no longer available for purchase. For more information, see [Phased-out instance types](reseller.en-US/Instances/Instance type families/Phased-out instance types.md#).
-   Upgrading instance types is supported within or between certain instance type families. For such families and corresponding upgrade rules, see [Instance type families that support upgrading instance types](../../../../reseller.en-US/Instances/Change configurations/Instance type families that support instance type upgrades.md#).
-   Upgrading instance types is not supported within or between the following instance type families: d1, d1ne, i1, i2, i2g, vgn5i, ga1, gn5, gn6i, f1, f3, ebmc4, ebmg5, sccg5, scch5, and sccgn6.

Alibaba Cloud ECS instances are categorized into the following type families:

-   Type families for enterprise-level computing on the x86-architecture:
    -   [g5, general-purpose type family](#)
    -   [sn2ne, general-purpose type family with enhanced network performance](#)
    -   [ic5, intensive compute instance type family](#)
    -   [c5, compute instance type family](#)
    -   [sn1ne, compute optimized type family with enhanced network performance](#)
    -   [r5, memory instance type family](#)
    -   [re4, memory optimized type family with enhanced performance](#)
    -   [re4e, memory optimized type family with enhanced performance](#)
    -   [se1ne, memory optimized type family with enhanced network performance](#)
    -   [se1, memory optimized type family](#)
    -   [d1ne, big data type family with enhanced network performance](#)
    -   [d1, big data type family](#)
    -   [i2, type family with local SSD disks](#)
    -   [i2g, type family with local SSD disks](#)
    -   [i1, type family with local SSD disks](#)
    -   [hfc5, compute optimized type family with high clock speed](#)
    -   [hfg5, general-purpose type family with high clock speed](#)
-   Type families for enterprise-level heterogeneous computing:
    -   [vgn5i, light-weight compute optimized type family with GPU](#)
    -   [gn6i, compute optimized type family with GPUs](reseller.en-US/Instances/Instance type families.md#gn6i)
    -   [gn6v, compute optimized type family with GPU](#)
    -   [gn5, compute optimized type family with GPU](#)
    -   [gn5i, compute optimized type family with GPU](#)
    -   [gn4, compute optimized type family with GPU](#)
    -   [ga1, visualization compute optimized type family with GPU](#)
    -   [f1, compute optimized type family with FPGA](#)
    -   [f3, compute optimized type family with FPGA](#)
-   ECS Bare Metal Instance type families and Super Computing Cluster \(SCC\) instance type families:
    -   [ebmhfg5, ECS Bare Metal Instance type family with high clock speed](#)
    -   [ebmc4, computing ECS Bare Metal Instance type family](#)
    -   [ebmg5, general-purpose ECS Bare Metal Instance type family](#)
    -   [scch5, Super Computing Cluster \(SCC\) instance type family with high clock speed](#)
    -   [sccg5, general-purpose Super Computing Cluster \(SCC\) instance type family](#)
    -   [sccgn6, compute optimized Super Computing Cluster \(SCC\) instance type family with GPUs](reseller.en-US/Instances/Instance type families.md#sccgn6)
-   Type families for entry-level computing on the x86-architecture:
    -   [t5, burstable instances](#)
    -   [xn4/n4/mn4/e4, type families of previous generations for entry-level users, computing on the x86-architecture](#)

## g5, general-purpose type family {#g5 .section}

**Features**

-   I/O-optimized
-   Supports SSD Cloud Disks and Ultra Disks
-   Equipped with a vCPU to memory ratio of 1:4
-   Ultra high packet forwarding rate
-   Equipped with 2.5 GHz Intel Xeon Platinum 8163 \(Skylake\) processors
-   Supports strong network performance through sufficient computing capacity
-   Suitable for the following scenarios:
    -   Scenarios where a large volume of packets are received and transmitted, such as the re-transmission of telecommunication information
    -   Enterprise-level applications of various types and sizes
    -   Medium and small database systems, cache, and search clusters
    -   Data analysis and computing
    -   Computing clusters and data processing reliant on memory

**Instance types**

|Instance type|vCPU|Memory \(GiB\)|Local disks \(GiB\)[ \* ](#)|Bandwidth \(Gbit/s\)[ \*\* ](#)|Packet forwarding rate \(Thousand pps\)[ \*\*\* ](#)|NIC queues[ \*\*\*\* ](#)|ENIs[ \*\*\*\*\* ](#)|Private IP address of a single ENI|
|:------------|:---|:-------------|:---------------------------|:------------------------------|:---------------------------------------------------|:------------------------|:--------------------|----------------------------------|
|ecs.g5.large|2|8.0|N/A|1.0|300|2|2|6|
|ecs.g5.xlarge|4|16.0|N/A|1.5|500|2|3|10|
|ecs.g5.2xlarge|8|32.0|N/A|2.5|800|2|4|10|
|ecs.g5.3xlarge|12|48.0|N/A|4.0|900|4|6|10|
|ecs.g5.4xlarge|16|64.0|N/A|5.0|1,000|4|8|20|
|ecs.g5.6xlarge|24|96.0|N/A|7.5|1,500|6|8|20|
|ecs.g5.8xlarge|32|128.0|N/A|10.0|2,000|8|8|20|
|ecs.g5.16xlarge|64|256.0|N/A|20.0|4,000|16|8|20|

See [other instance type families](#).

## sn2ne, general-purpose type family with enhanced network performance {#sn2ne .section}

**Features**

-   I/O-optimized
-   Supports SSD Cloud Disks and Ultra Disks
-   Equipped with a vCPU to memory ratio of 1:4
-   Ultra high packet forwarding rate
-   Equipped with 2.5 GHz Intel Xeon E5-2682 v4 \(Broadwell\) or Platinum 8163 \(Skylake\) processors
-   Supports strong network performance through sufficient computing capacity
-   Suitable for the following scenarios:
    -   Scenarios where a large volume of packets are received and transmitted, such as the re-transmission of telecommunication information
    -   Enterprise-level applications of various types and sizes
    -   Medium and small database systems, cache, and search clusters
    -   Data analysis and computing
    -   Computing clusters and data processing depending on memory

**Instance types**

|Instance type|vCPU|Memory \(GiB\)|Local disks \(GiB\)[ \* ](#)|Bandwidth \(Gbit/s\)[ \*\* ](#)|Packet forwarding rate \(Thousand pps\)[ \*\*\* ](#)|NIC queues[ \*\*\*\* ](#)|ENIs[ \*\*\*\*\* ](#)|Private IP address of a single ENI|
|:------------|:---|:-------------|:---------------------------|:------------------------------|:---------------------------------------------------|:------------------------|:--------------------|----------------------------------|
|ecs.sn2ne.large|2|8.0|N/A|1.0|300|2|2|6|
|ecs.sn2ne.xlarge|4|16.0|N/A|1.5|500|2|3|10|
|ecs.sn2ne.2xlarge|8|32.0|N/A|2.0|1,000|4|4|10|
|ecs.sn2ne.3xlarge|12|48.0|N/A|2.5|1,300|4|6|10|
|ecs.sn2ne.4xlarge|16|64.0|N/A|3.0|1,600|4|8|20|
|ecs.sn2ne.6xlarge|24|96.0|N/A|4.5|2,000|6|8|20|
|ecs.sn2ne.8xlarge|32|128.0|N/A|6.0|2,500|8|8|20|
|ecs.sn2ne.14xlarge|56|224.0|N/A|10.0|4,500|14|8|20|

See [other instance type families](#).

## ic5, intensive compute instance type family {#ic5 .section}

**Features**

-   I/O-optimized
-   Supports SSD Cloud Disks and Ultra Disks
-   Equipped with a vCPU to memory ratio of 1:1
-   Ultra high packet forwarding rate
-   Equipped with 2.5 GHz Intel Xeon Platinum 8163 \(Skylake\) processors
-   Supports strong network performance through sufficient computing capacity
-   Suitable for the following scenarios:
    -   Web front-end servers
    -   Data analysis, batch compute, and video coding
    -   Scenarios where a large volume of packets are received and transmitted, such as the re-transmission of telecommunication information
    -   Massively Multiplayer Online \(MMO\) game frontends

**Instance types**

|Instance type|vCPU|Memory \(GiB\)|Local disks \(GiB\)[ \* ](#)|Bandwidth \(Gbit/s\)[ \*\* ](#)|Packet forwarding rate \(Thousand pps\)[ \*\*\* ](#)|NIC queues[ \*\*\*\* ](#)|ENIs[ \*\*\*\*\* ](#)|Private IP address of a single ENI|
|:------------|:---|:-------------|:---------------------------|:------------------------------|:---------------------------------------------------|:------------------------|:--------------------|----------------------------------|
|ecs.ic5.large|2|2.0|N/A|1.0|300|2|2|6|
|ecs.ic5.xlarge|4|4.0|N/A|1.5|500|2|3|10|
|ecs.ic5.2xlarge|8|8.0|N/A|2.5|800|2|4|10|
|ecs.ic5.3xlarge|12|12.0|N/A|4.0|900|4|6|10|
|ecs.ic5.4xlarge|16|16.0|N/A|5.0|1,000|4|8|20|

See [other instance type families](#).

## c5, compute instance type family {#c5 .section}

**Features**

-   I/O-optimized
-   Supports SSD Cloud Disks and Ultra Disks
-   Equipped with a vCPU to memory ratio of 1:2
-   Ultra high packet forwarding rate
-   Equipped with 2.5 GHz Intel Xeon Platinum 8163 \(Skylake\) processors
-   Supports strong network performance through sufficient computing capacity
-   Suitable for the following scenarios:
    -   Scenarios where a large volume of packets are received and transmitted, such as the re-transmission of telecommunication information
    -   Web front-end servers
    -   Massively Multiplayer Online \(MMO\) game frontends
    -   Data analysis, batch compute, and video coding
    -   High-performance science and engineering applications

**Instance types**

|Instance type|vCPU|Memory \(GiB\)|Local disks \(GiB\)[ \* ](#)|Bandwidth \(Gbit/s\)[ \*\* ](#)|Packet forwarding rate \(Thousand pps\)[ \*\*\* ](#)|NIC queues[ \*\*\*\* ](#)|ENIs[ \*\*\*\*\* ](#)|Private IP address of a single ENI|
|:------------|:---|:-------------|:---------------------------|:------------------------------|:---------------------------------------------------|:------------------------|:--------------------|----------------------------------|
|ecs.c5.large|2|4.0|N/A|1.0|300|2|2|6|
|ecs.c5.xlarge|4|8.0|N/A|1.5|500|2|3|10|
|ecs.c5.2xlarge|8|16.0|N/A|2.5|800|2|4|10|
|ecs.c5.3xlarge|12|24.0|N/A|4.0|900|4|6|10|
|ecs.c5.4xlarge|16|32.0|N/A|5.0|1,000|4|8|20|
|ecs.c5.6xlarge|24|48.0|N/A|7.5|1,500|6|8|20|
|ecs.c5.8xlarge|32|64.0|N/A|10.0|2,000|8|8|20|
|ecs.c5.16xlarge|64|128.0|N/A|20.0|4,000|16|8|20|

See [other instance type families](#).

## sn1ne, compute optimized type family with enhanced network performance {#sn1ne .section}

**Features**

-   I/O-optimized
-   Supports SSD Cloud Disks and Ultra Disks
-   Equipped with a vCPU to memory ratio of 1:2
-   Ultra high packet forwarding rate
-   Equipped with 2.5 GHz Intel Xeon E5-2682 v4 \(Broadwell\) or Platinum 8163 \(Skylake\) processors
-   Supports strong network performance through sufficient computing capacity
-   Suitable for the following scenarios:
    -   Scenarios where a large volume of packets are received and transmitted, such as the re-transmission of telecommunication information
    -   Web front-end servers
    -   Massively Multiplayer Online \(MMO\) game frontends
    -   Data analysis, batch compute, and video coding
    -   High-performance science and engineering applications

**Instance types**

|Instance type|vCPU|Memory \(GiB\)|Local disks \(GiB\)[ \* ](#)|Bandwidth \(Gbit/s\)[ \*\* ](#)|Packet forwarding rate \(Thousand pps\)[ \*\*\* ](#)|NIC queues[ \*\*\*\* ](#)|ENIs[ \*\*\*\*\* ](#)|Private IP address of a single ENI|
|:------------|:---|:-------------|:---------------------------|:------------------------------|:---------------------------------------------------|:------------------------|:--------------------|----------------------------------|
|ecs.sn1ne.large|2|4.0|N/A|1.0|300|2|2|6|
|ecs.sn1ne.xlarge|4|8.0|N/A|1.5|500|2|3|10|
|ecs.sn1ne.2xlarge|8|16.0|N/A|2.0|1,000|4|4|10|
|ecs.sn1ne.3xlarge|12|24.0|N/A|2.5|1,300|4|6|10|
|ecs.sn1ne.4xlarge|16|32.0|N/A|3.0|1,600|4|8|20|
|ecs.sn1ne.6xlarge|24|48.0|N/A|4.5|2,000|6|8|20|
|ecs.sn1ne.8xlarge|32|64.0|N/A|6.0|2,500|8|8|20|

See [other instance type families](#).

## r5, memory instance type family {#r5 .section}

**Features**

-   I/O-optimized
-   Supports SSD Cloud Disks and Ultra Disks
-   Ultra high packet forwarding rate
-   Equipped with 2.5 GHz Intel Xeon Platinum 8163 \(Skylake\) processors
-   Supports strong network performance through sufficient computing capacity
-   Suitable for the following scenarios:
    -   Scenarios where a large volume of packets are received and transmitted, such as the re-transmission of telecommunication information
    -   High-performance databases and high memory databases
    -   Data analysis and mining, and distributed memory cache
    -   Hadoop, Spark, and other enterprise-level applications with large memory requirements

**Instance types**

|Instance type|vCPU|Memory \(GiB\)|Local disks \(GiB\)[ \* ](#)|Bandwidth \(Gbit/s\)[ \*\* ](#)|Packet forwarding rate \(Thousand pps\)[ \*\*\* ](#)|NIC queues[ \*\*\*\* ](#)|ENIs[ \*\*\*\*\* ](#)|Private IP address of a single ENI|
|:------------|:---|:-------------|:---------------------------|:------------------------------|:---------------------------------------------------|:------------------------|:--------------------|----------------------------------|
|ecs.r5.large|2|16.0|N/A|1.0|300|2|2|6|
|ecs.r5.xlarge|4|32.0|N/A|1.5|500|2|3|10|
|ecs.r5.2xlarge|8|64.0|N/A|2.5|800|2|4|10|
|ecs.r5.3xlarge|12|96.0|N/A|4.0|900|4|6|10|
|ecs.r5.4xlarge|16|128.0|N/A|5.0|1,000|4|8|20|
|ecs.r5.6xlarge|24|192.0|N/A|7.5|1,500|6|8|20|
|ecs.r5.8xlarge|32|256.0|N/A|10.0|2,000|8|8|20|
|ecs.r5.16xlarge|64|512.0|N/A|20.0|4,000|16|8|20|

See [other instance type families](#).

## re4, memory optimized instance type family with enhanced performance {#re4 .section}

**Features**

-   Supports SSD Cloud Disks and Ultra Disks
-   I/O-optimized
-   Optimized for high-performance databases, high memory databases, and other memory-intensive enterprise applications
-   2.2 GHz Intel Xeon E7 8880 v4 \(Broadwell\) processors, up to 2.4 GHz Turbo Boot
-   Equipped with a vCPU to memory ratio of 1:12, up to 1920.0 GiB memory
-   ecs.re4.20xlarge and ecs.re4.40xlarge have been certified by SAP HANA
-   Suitable for the following scenarios:
    -   High-performance databases and high memory databases \(for example, SAP HANA\)
    -   Memory intensive applications
    -   Big Data processing engines, such as Apache spark or Presto

**Instance types**

|Instance type|vCPU|Memory \(GiB\)|Local disks \(GiB\)[ \* ](#)|Bandwidth \(Gbit/s\)[ \*\* ](#)|Packet forwarding rate \(Thousand pps\)[ \*\*\* ](#)|NIC queues[ \*\*\*\* ](#)|ENIs[ \*\*\*\*\* ](#)|Private IP address of a single ENI|
|:------------|:---|:-------------|:---------------------------|:------------------------------|:---------------------------------------------------|:------------------------|:--------------------|----------------------------------|
|ecs.re4.20xlarge|80|960.0|N/A|15.0|2,000|16|8|20|
|ecs.re4.40xlarge|160|1920.0|N/A|30.0|4,500|16|8|20|

See [other instance type families](#).

## re4e, memory optimized type family with enhanced performance {#re4e .section}

**Features**

-   I/O-optimized
-   Supports SSD Cloud Disks and Ultra Disks
-   Optimized for high-performance databases, high memory databases, and other memory-intensive enterprise applications
-   2.2 GHz Intel Xeon E7 8880 v4 \(Broadwell\) processors, up to 2.4 GHz Turbo Boot
-   Equipped with a vCPU to memory ratio of 1:24, up to 3840.0 GiB memory
-   Suitable for the following scenarios:
    -   High-performance databases and high memory databases \(for example, SAP HANA\)
    -   Memory intensive applications
    -   Big Data processing engines, such as Apache spark or Presto

**Instance types**

|Instance type|vCPU|Memory \(GiB\)|Local disks \(GiB\)[ \* ](#)|Bandwidth \(Gbit/s\)[ \*\* ](#)|Packet forwarding rate \(Thousand pps\)[ \*\*\* ](#)|NIC queues[ \*\*\*\* ](#)|ENIs[ \*\*\*\*\* ](#)|Private IP address of a single ENI|
|:------------|:---|:-------------|:---------------------------|:------------------------------|:---------------------------------------------------|:------------------------|:--------------------|----------------------------------|
|ecs.re4e.40xlarge|160|3840.0|N/A|30.0|4,500|16|15|20|

See [other instance type families](#).

## se1ne, memory optimized type family with enhanced network performance {#se1ne .section}

**Features**

-   I/O-optimized
-   Supports SSD Cloud Disks and Ultra Disks
-   Equipped with a vCPU to memory ratio of 1:8
-   Ultra high packet receive and forwarding rate
-   Equipped with 2.5 GHz Intel Xeon E5-2682 v4 \(Broadwell\) or Platinum 8163 \(Skylake\) processors
-   Supports strong network performance through sufficient computing capacity
-   Suitable for the following scenarios:
    -   Scenarios where a large volume of packets are received and transmitted, such as the re-transmission of telecommunication information
    -   High-performance databases and large memory databases
    -   Data analysis and mining, and distributed memory cache
    -   Hadoop, Spark, and other enterprise-level applications with large memory requirements

**Instance types**

|Instance type|vCPU|Memory \(GiB\)|Local disks \(GiB\)[ \* ](#)|Bandwidth \(Gbit/s\)[ \*\* ](#)|Packet forwarding rate \(Thousand pps\)[ \*\*\* ](#)|NIC queues[ \*\*\*\* ](#)|ENIs[ \*\*\*\*\* ](#)|Private IP address of a single ENI|
|:------------|:---|:-------------|:---------------------------|:------------------------------|:---------------------------------------------------|:------------------------|:--------------------|----------------------------------|
|ecs.se1ne.large|2|16.0|N/A|1.0|300|2|2|6|
|ecs.se1ne.xlarge|4|32.0|N/A|1.5|500|2|3|10|
|ecs.se1ne.2xlarge|8|64.0|N/A|2.0|1,000|4|4|10|
|ecs.se1ne.3xlarge|12|96.0|N/A|2.5|1,300|4|6|10|
|ecs.se1ne.4xlarge|16|128.0|N/A|3.0|1,600|4|8|20|
|ecs.se1ne.6xlarge|24|192.0|N/A|4.5|2,000|6|8|20|
|ecs.se1ne.8xlarge|32|256.0|N/A|6.0|2,500|8|8|20|
|ecs.se1ne.14xlarge|56|480.0|N/A|10.0|4,500|14|8|20|

See [other instance type families](#).

## se1, memory optimized type family {#se1 .section}

**Features**

-   I/O-optimized
-   Supports SSD Cloud Disks and Ultra Disks
-   Equipped with a vCPU to memory ratio of 1:8
-   Equipped with 2.5 GHz Intel Xeon E5-2682 v4 \(Broadwell\) processors
-   Supports strong network performance through sufficient computing capacity
-   Suitable for the following scenarios:
    -   High-performance databases and large memory databases
    -   Data analysis and mining, and distributed memory cache
    -   Hadoop, Spark, and other enterprise-level applications with large memory requirements

**Instance types**

|Instance type|vCPU|Memory \(GiB\)|Local disks \(GiB\)[ \* ](#)|Bandwidth \(Gbit/s\)[ \*\* ](#)|Packet forwarding rate \(Thousand pps\)[ \*\*\* ](#)|NIC queues[ \*\*\*\* ](#)|ENIs[ \*\*\*\*\* ](#)|Private IP address of a single ENI|
|:------------|:---|:-------------|:---------------------------|:------------------------------|:---------------------------------------------------|:------------------------|:--------------------|----------------------------------|
|ecs.se1.large|2|16.0|N/A|0.5|100|1|2|6|
|ecs.se1.xlarge|4|32.0|N/A|0.8|200|1|3|10|
|ecs.se1.2xlarge|8|64.0|N/A|1.5|400|1|4|10|
|ecs.se1.4xlarge|16|128.0|N/A|3.0|500|2|8|20|
|ecs.se1.8xlarge|32|256.0|N/A|6.0|800|3|8|20|
|ecs.se1.14xlarge|56|480.0|N/A|10.0|1,200|4|8|20|

See [other instance type families](#).

## d1ne, big data type family with enhanced network performance {#d1ne .section}

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

|Instance type|vCPU|Memory \(GiB\)|Local disks \(GiB\)[ \* ](#)|Bandwidth \(Gbit/s\)[ \*\* ](#)|Packet forwarding rate \(Thousand pps\)[ \*\*\* ](#)|NIC queues[ \*\*\*\* ](#)|ENIs[ \*\*\*\*\* ](#)|Private IP address of a single ENI|
|:------------|:---|:-------------|:---------------------------|:------------------------------|:---------------------------------------------------|:------------------------|:--------------------|----------------------------------|
|ecs.d1ne.2xlarge|8|32.0|4 \* 5500|6.0|1,000|4|4|10|
|ecs.d1ne.4xlarge|16|64.0|8 \* 5500|12.0|1,600|4|8|20|
|ecs.d1ne.6xlarge|24|96.0|12 \* 5500|16.0|2,000|6|8|20|
|ecs.d1ne-c8d3.8xlarge|32|128.0|12 \* 5500|20.0|2,000|6|8|20|
|ecs.d1ne.8xlarge|32|128.0|16 \* 5500|20.0|2,500|8|8|20|
|ecs.d1ne-c14d3.14xlarge|56|160.0|12 \* 5500|35.0|4,500|14|8|20|
|ecs.d1ne.14xlarge|56|224.0|28 \* 5500|35.0|4,500|14|8|20|

**Note:** 

-   You cannot change configurations of d1ne instances.
-   For more information about d1ne type families, see [FAQ on d1 and d1ne](https://partners-intl.aliyun.com/help/faq-detail/52993.htm).

See [other instance type families](#).

## d1, big data type family {#d1 .section}

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

|Instance type|vCPU|Memory \(GiB\)|Local disks \(GiB\)[ \* ](#)|Bandwidth \(Gbit/s\)[ \*\* ](#)|Packet forwarding rate \(Thousand pps\)[ \*\*\* ](#)|NIC queues[ \*\*\*\* ](#)|ENIs[ \*\*\*\*\* ](#)|Private IP address of a single ENI|
|:------------|:---|:-------------|:---------------------------|:------------------------------|:---------------------------------------------------|:------------------------|:--------------------|----------------------------------|
|ecs.d1.2xlarge|8|32.0|4 \* 5500|3.0|300|1|4|10|
|ecs.d1.3xlarge|12|48.0|16 \* 5500|4.0|400|1|6|10|
|ecs.d1.4xlarge|16|64.0|8 \* 5500|6.0|600|2|8|20|
|ecs.d1.6xlarge|24|96.0|12 \* 5500|8.0|800|2|8|20|
|ecs.d1-c8d3.8xlarge|32|128.0|12 \* 5500|10.0|1,000|4|8|20|
|ecs.d1.8xlarge|32|128.0|16 \* 5500|10.0|1,000|4|8|20|
|ecs.d1-c14d3.14xlarge|56|160.0|12 \* 5500|17.0|1,800|6|8|20|
|ecs.d1.14xlarge|56|224.0|28 \* 5500|17.0|1,800|6|8|20|

**Note:** For more information about d1 type families, see [FAQ on d1 and d1ne](https://partners-intl.aliyun.com/help/faq-detail/52993.htm).

See [other instance type families](#).

## i2, type family with local SSD disks {#i2 .section}

**Features**

-   I/O-optimized
-   Supports SSD Cloud Disks and Ultra Disks
-   High-performance local NVMe SSD disks with high IOPS, high I/O throughput, and low latency.
-   Equipped with a vCPU to memory ratio of 1:8, designed for high-performance databases
-   Equipped with 2.5 GHz Intel Xeon Platinum 8163 \(Skylake\) processors
-   Supports strong network performance through sufficient computing capacity
-   Suitable for the following scenarios:
    -   OLTP and high-performance relational databases
    -   NoSQL databases, such as Cassandra and MongoDB
    -   Search applications, such as Elasticsearch

**Instance types**

|Instance type|vCPU|Memory \(GiB\)|Local disks \(GiB\)[ \* ](#)|Bandwidth \(Gbit/s\)[ \*\* ](#)|Packet forwarding rate \(Thousand pps\)[ \*\*\* ](#)|NIC queues[ \*\*\*\* ](#)|ENIs[ \*\*\*\*\* ](#)|Private IP address of a single ENI|
|:------------|:---|:-------------|:---------------------------|:------------------------------|:---------------------------------------------------|:------------------------|:--------------------|----------------------------------|
|ecs.i2.xlarge|4|32.0|1 \* 894|1.0|500|2|3|10|
|ecs.i2.2xlarge|8|64.0|1 \* 1788|2.0|1,000|2|4|10|
|ecs.i2.4xlarge|16|128.0|2 \* 1788|3.0|1,500|4|8|20|
|ecs.i2.8xlarge|32|256.0|4 \* 1788|6.0|2,000|8|8|20|
|ecs.i2.16xlarge|64|512.0|8 \* 1788|10.0|4,000|16|8|20|

See [other instance type families](#).

## i2g, type family with local SSD disks {#i2g .section}

**Features**

-   I/O-optimized
-   Supports SSD Cloud Disks and Ultra Disks
-   High-performance local NVMe SSD disks with high IOPS, high I/O throughput, and low latency.
-   Equipped with a vCPU to memory ratio of 1:4, designed for high-performance databases
-   Equipped with 2.5 GHz Intel Xeon Platinum 8163 \(Skylake\) processors
-   Supports strong network performance through sufficient computing capacity
-   Suitable for the following scenarios:
    -   OLTP and high-performance relational databases
    -   NoSQL databases, such as Cassandra and MongoDB
    -   Search applications, such as Elasticsearch

**Instance types**

|Instance type|vCPU|Memory \(GiB\)|Local disks \(GiB\)[ \* ](#)|Bandwidth \(Gbit/s\)[ \*\* ](#)|Packet forwarding rate \(Thousand pps\)[ \*\*\* ](#)|NIC queues[ \*\*\*\* ](#)|ENIs[ \*\*\*\*\* ](#)|Private IP address of a single ENI|
|:------------|:---|:-------------|:---------------------------|:------------------------------|:---------------------------------------------------|:------------------------|:--------------------|----------------------------------|
|ecs.i2g.2xlarge|8|32.0|1 \* 894|2.0|1,000|2|4|10|
|ecs.i2g.4xlarge|16|64.0|1 \* 1788|3.0|1,500|4|8|20|
|ecs.i2g.8xlarge|32|128.0|2 \* 1788|6.0|2,000|8|8|20|
|ecs.i2g.16xlarge|64|256.0|4 \* 1788|10.0|4,000|16|8|20|

See [other instance type families](#).

## i1, type family with local SSD disks {#i1 .section}

**Features**

-   I/O-optimized
-   Supports SSD Cloud Disks and Ultra Disks
-   High-performance local NVMe SSD disks with high IOPS, high I/O throughput, and low latency
-   Equipped with a vCPU to memory ratio of 1:4, designed for big data scenarios
-   Equipped with 2.5 GHz Intel Xeon E5-2682 v4 \(Broadwell\) processors
-   Supports strong network performance through sufficient computing capacity
-   Suitable for the following scenarios:
    -   OLTP and high-performance relational databases
    -   NoSQL databases, such as Cassandra and MongoDB
    -   Search applications, such as Elasticsearch

**Instance types**

|Instance type|vCPU|Memory \(GiB\)|Local disks \(GiB\)[ \* ](#)|Bandwidth \(Gbit/s\)[ \*\* ](#)|Packet forwarding rate \(Thousand pps\)[ \*\*\* ](#)|NIC queues[ \*\*\*\* ](#)|ENIs[ \*\*\*\*\* ](#)|Private IP address of a single ENI|
|:------------|:---|:-------------|:---------------------------|:------------------------------|:---------------------------------------------------|:------------------------|:--------------------|----------------------------------|
|ecs.i1.xlarge|4|16.0|2 \* 104|0.8|200|1|3|10|
|ecs.i1.2xlarge|8|32.0|2 \* 208|1.5|400|1|4|10|
|ecs.i1.3xlarge|12|48.0|2 \* 312|2.0|400|1|6|10|
|ecs.i1.4xlarge|16|64.0|2 \* 416|3.0|500|2|8|20|
|ecs.i1-c5d1.4xlarge|16|64.0|2 \* 1456|3.0|400|2|8|20|
|ecs.i1.6xlarge|24|96.0|2 \* 624|4.5|600|2|8|
|ecs.i1.8xlarge|32|128.0|2 \* 832|6.0|800|3|8|20|
|ecs.i1-c10d1.8xlarge|32|128.0|2 \* 1456|6.0|800|3|8|20|
|ecs.i1.14xlarge|56|224.0|2 \* 1456|10.0|1,200|4|8|20|

See [other instance type families](#).

## hfc5, compute optimized type family with high clock speed {#hfc5 .section}

**Features**

-   I/O-optimized
-   Supports SSD Cloud Disks and Ultra Disks
-   Stable performance
-   3.1 GHz Intel Xeon Gold 6149 \(Skylake\) processors
-   Equipped with a vCPU to memory ratio of 1:2
-   Supports strong network performance through sufficient computing capacity
-   Suitable for the following scenarios:
    -   High-performance Web front-end servers
    -   High-performance science and engineering applications
    -   Massively Multiplayer Online \(MMO\) games and video coding

**Instance types**

|Instance type|vCPU|Memory \(GiB\)|Local disks \(GiB\)[ \* ](#)|Bandwidth \(Gbit/s\)[ \*\* ](#)|Packet forwarding rate \(Thousand pps\)[ \*\*\* ](#)|NIC queues[ \*\*\*\* ](#)|ENIs[ \*\*\*\*\* ](#)|Private IP address of a single ENI|
|:------------|:---|:-------------|:---------------------------|:------------------------------|:---------------------------------------------------|:------------------------|:--------------------|----------------------------------|
|ecs.hfc5.large|2|4.0|N/A|1.0|300|2|2|6|
|ecs.hfc5.xlarge|4|8.0|N/A|1.5|500|2|3|10|
|ecs.hfc5.2xlarge|8|16.0|N/A|2.0|1,000|2|4|10|
|ecs.hfc5.3xlarge|12|24.0|N/A|2.5|1,300|4|6|10|
|ecs.hfc5.4xlarge|16|32.0|N/A|3.0|1,600|4|8|20|
|ecs.hfc5.6xlarge|24|48.0|N/A|4.5|2,000|6|8|20|
|ecs.hfc5.8xlarge|32|64.0|N/A|6.0|2,500|8|8|20|

See [other instance type families](#).

## hfg5, general-purpose type family with high clock speed {#hfg5 .section}

**Features**

-   I/O-optimized
-   Supports SSD Cloud Disks and Ultra Disks
-   Stable performance
-   3.1 GHz Intel Xeon Gold 6149 \(Skylake\) processors
-   Equipped with a vCPU to memory ratio of 1:4, except for the 56 vCPU instance type
-   Supports strong network performance through sufficient computing capacity
-   Suitable for the following scenarios:
    -   High-performance Web front-end servers
    -   High-performance science and engineering applications
    -   Massively Multiplayer Online \(MMO\) games and video coding

**Instance types**

|Instance type|vCPU|Memory \(GiB\)|Local disks \(GiB\)[ \* ](#)|Bandwidth \(Gbit/s\)[ \*\* ](#)|Packet forwarding rate \(Thousand pps\)[ \*\*\* ](#)|NIC queues[ \*\*\*\* ](#)|ENIs[ \*\*\*\*\* ](#)|Private IP address of a single ENI|
|:------------|:---|:-------------|:---------------------------|:------------------------------|:---------------------------------------------------|:------------------------|:--------------------|----------------------------------|
|ecs.hfg5.large|2|8.0|N/A|1.0|300|2|2|6|
|ecs.hfg5.xlarge|4|16.0|N/A|1.5|500|2|3|10|
|ecs.hfg5.2xlarge|8|32.0|N/A|2.0|1,000|2|4.|10|
|ecs.hfg5.3xlarge|12|48.0|N/A|2.5|1,300|4|6|10|
|ecs.hfg5.4xlarge|16|64.0|N/A|3.0|1,600|4|8|20|
|ecs.hfg5.6xlarge|24|96.0|N/A|4.5|2,000|6|8|20|
|ecs.hfg5.8xlarge|32|128.0|N/A|6.0|2,500|8|8|20|
|ecs.hfg5.14xlarge|56|160.0|N/A|10.0|4,000|14|8|20|

See [other instance type families](#).

## vgn5i, light-weight compute optimized type family with GPU {#vgn5i .section}

**Features**

-   I/O-optimized
-   Supports SSD Cloud Disks and Ultra Disks
-   Use an NVIDIA P4 GPU computation accelerator
-   Contains a virtual GPU \(which is the result of partitioned virtualization\)
    -   Supports the 1/8, 1/4, 1/2, and 1:1 computing capacity of NVIDIA Tesla P4 GPUs
    -   Supports 1, 2, 4, and 8 GB of GPU memory
-   Equipped with a vCPU to memory ratio of 1:3
-   Equipped with 2.5 GHz Intel Xeon E5-2682 v4 \(Broadwell\) processors
-   Supports strong network performance through sufficient computing capacity
-   Suitable for the following scenarios:
    -   Real-time online rendering required for cloud gaming and AR/VR applications
    -   AI reasoning \(including deep and machine learning\), used in the elastic deployment of Internet services that use AI reasoning and computing
    -   Educational and modeling experiment environments that use deep learning

**Instance types**

|Instance type|vCPU|Memory \(GiB\)|Local disks \(GiB\)[ \* ](#)|GPU|GPU memory \(GB\)|Bandwidth \(Gbit/s\)[ \*\* ](#)|Packet forwarding rate \(thousand pps\)[ \*\*\* ](#)|NIC queues[ \*\*\*\* ](#)|ENIs[ \*\*\*\*\* ](#)|
|:------------|:---|:-------------|:---------------------------|:--|:----------------|:------------------------------|:---------------------------------------------------|:------------------------|:--------------------|
|ecs.vgn5i-m1.large|2|6|N/A|P4\*1/8|1|1|300|2|2|
|ecs.vgn5i-m2.xlarge|4|12|N/A|P4\*1/4|2|2|500|2|3|
|ecs.vgn5i-m4.2xlarge|8|24|N/A|P4\*1/2|4|3|800|2|4|
|ecs.vgn5i-m8.4xlarge|16|48|N/A|P4\*1|8|5|1,000|4|5|

**Note:** For more information, see [Create a compute optimized instance with GPUs](reseller.en-US/Instances/Instance type families/Compute optimized type family with GPU/Create a compute optimized instance with GPU.md#).

See [other instance type families](#).

## gn6i, compute optimized type family with GPUs {#gn6i .section}

**Features**

-   I/O-optimized
-   Equipped with a vCPU to memory ratio of 1:4
-   Equipped with 2.5 GHz Intel Xeon Platinum 8163 \(Skylake\) processors
-   Supports ESSD Cloud Disks \(million-level IOPS\), SSD Cloud Disks, and Ultra Disks
-   Achieves better performance with the X-Dragon new-generation compute architecture
-   Uses NVIDIA T4 GPU processors:
    -   Based on the new NVIDIA Turing architecture
    -   Up to 320 Turing Tensor Cores
    -   Up to 2,560 CUDA Cores
    -   Mixed-precision Tensor Cores support 65 TFlops FP16, 130 INT8 TOPS, and 260 INT4 TOPS
    -   16 GB GPU memory capacity \(320 GB/s bandwidth\)
-   Supports strong network performance through sufficient computing capacity
-   Suitable for the following scenarios:
    -   AI \(deep learning and machine learning\) inference, computer vision, voice recognition, voice synthesization, natural language processing, machine translation, and reference systems
    -   Real-time online rendering required for cloud gaming and AR/VR applications
    -   Heavy-load graphic computing or graphic workstations
    -   GPU-accelerated databases
    -   High-performance computing

**Instance types**

|Instance types|vCPU|Memory \(GiB\)|Local disks \(GiB\)[ \* ](#)|GPU|GPU memory \(GB\)|Bandwidth \(Gbit/s\)[ \*\* ](#)|Packet forwarding rate \(Thousand pps\)[ \*\*\* ](#)|NIC queues[ \*\*\*\* ](#)|ENIs[ \*\*\*\*\* ](#)|
|:-------------|:---|:-------------|:---------------------------|:--|:----------------|-------------------------------|:---------------------------------------------------|:------------------------|:--------------------|
|ecs.gn6i-c4g1.xlarge|4|15|N/A|T4\*1|16|4|500|2|2|
|ecs.gn6i-c8g1.2xlarge|8|31|N/A|T4\*1|16|5|800|2|2|
|ecs.gn6i-c16g1.4xlarge|16|62|N/A|T4\*1|16|6|1,000|4|3|
|ecs.gn6i-c24g1.6xlarge|24|93|N/A|T4\*1|16|7.5|1,200|6|4|
|ecs.gn6i-c24g1.12xlarge|48|186|N/A|T4\*2|32|15|2,400|12|6|
|ecs.gn6i-c24g1.24xlarge|96|372|N/A|T4\*4|64|30|4,800|24|8|
|ecs.gn6i-c32g1.8xlarge|32|124|N/A|T4\*1|16|10|1,600|8|6|
|ecs.gn6i-c48g1.12xlarge|48|186|N/A|T4\*1|16|12|2,400|12|6|
|ecs.gn6i-c72g1.18xlarge|72|279|N/A|T4\*1|16|21.5|3,600|18|8|

**Note:** For more information, see [Create a compute optimized instance with GPUs](../../../../dita-oss-bucket/SP_2/DNA0011894323/reseller.en-US/Instances/Instance type families/Compute optimized type family with GPU/Create a compute optimized instance with GPU.md#).

See [other instance type families](#).

## gn6v, compute optimized type family with GPUs {#section_uqb_h4z_3hb .section}

**Features**

-   I/O-optimized
-   Supports SSD Cloud Disks and Ultra Disks
-   Uses NVIDIA V100 GPU processors
-   Equipped with a vCPU to memory ratio of 1:4
-   Equipped with 2.5 GHz Intel Xeon Platinum 8163 \(Skylake\) processors
-   Uses NVIDIA V100 GPU processors \(with the SXM2 module\):
    -   Based on the new NVIDIA Volta architecture
    -   16 GB HBM2 GPU memory capacity \(900 GB/s bandwidth\)
    -   Up to 5,120 CUDA Cores
    -   Up to 640 Tensor Cores
    -   Supports up to six NVLink connections and total bandwidth of 300 GB/s \(25 GB/s per connection\)
-   Supports strong network performance through sufficient computing capacity
-   Suitable for the following scenarios:
    -   Deep learning, autonomous vehicles, voice recognition, and other AI applications
    -   Scientific computing, computational finance, genomics, and environmental analysis

**Instance types**

|Instance types|vCPU|Memory \(GiB\)|Local disks \(GiB\)[ \* ](#)|GPU|GPU memory \(GB\)|Bandwidth \(Gbit/s\)[ \*\* ](#)|Packet forwarding rate \(Thousand pps\)[ \*\*\* ](#)|NIC queues[ \*\*\*\* ](#)|ENIs[ \*\*\*\*\* ](#)|Private IP address of a single ENI|
|:-------------|:---|:-------------|:---------------------------|:--|:----------------|:------------------------------|:---------------------------------------------------|:------------------------|:--------------------|----------------------------------|
|ecs.gn6v-c8g1.2xlarge|8|32.0|N/A|1 \* NVIDIA V100|1 \* 16|2.5|800|4|4|10|
|ecs.gn6v-c8g1.8xlarge|32|128.0|N/A|4 \* NVIDIA V100|4 \* 16|10.0|2,000|8|8|20|
|ecs.gn6v-c8g1.16xlarge|64|256.0|N/A|8 \* NVIDIA V100|8 \* 16|20.0|2,500|16|8|20|

**Note:** For more information, see [Create a compute optimized instance with GPUs](../../../../dita-oss-bucket/SP_2/DNA0011894323/reseller.en-US/Instances/Instance type families/Compute optimized type family with GPU/Create a compute optimized instance with GPU.md#).

See [other instance type families](#).

## gn5, compute optimized type family with GPU {#gn5 .section}

**Features**

-   I/O-optimized
-   Supports SSD Cloud Disks and Ultra Disks
-   Uses NVIDIA P100 GPU processors
-   No fixed ratio of vCPU to memory
-   High-performance local NVMe SSD disks
-   Equipped with 2.5 GHz Intel Xeon E5-2682 v4 \(Broadwell\) processors
-   Supports strong network performance through sufficient computing capacity
-   Suitable for the following scenarios:
    -   Deep learning
    -   Scientific computing, such as computational fluid dynamics, computational finance, genomics, and environmental analysis
    -   High-performance computing, rendering, multi-media coding and decoding, and other server-side GPU compute workloads

**Instance types**

|Instance type|vCPU|Memory \(GiB\)|Local disks \(GiB\)[ \* ](#)|GPU|GPU memory \(GB\)|Bandwidth \(Gbit/s\)[ \*\* ](#)|Packet forwarding rate \(Thousand pps\)[ \*\*\* ](#)|NIC queues[ \*\*\*\* ](#)|ENIs[ \*\*\*\*\* ](#)|Private IP address of a single ENI|
|:------------|:---|:-------------|:---------------------------|:--|:----------------|:------------------------------|:---------------------------------------------------|:------------------------|:--------------------|----------------------------------|
|ecs.gn5-c4g1.xlarge|4|30.0|440|1 \* NVIDIA P100|1 \* 16|3.0|300|1|3|10|
|ecs.gn5-c8g1.2xlarge|8|60.0|440|1 \* NVIDIA P100|1 \* 16|3.0|400|1|4|10|
|ecs.gn5-c4g1.2xlarge|8|60.0|880|2 \* NVIDIA P100|2 \* 16|5.0|1,000|2|4|10|
|ecs.gn5-c8g1.4xlarge|16|120.0|880|2 \* NVIDIA P100|2 \* 16|5.0|1,000|4|8|20|
|ecs.gn5-c28g1.7xlarge|28|112.0|440|1 \* NVIDIA P100|1 \* 16|5.0|1,000|8|8|20|
|ecs.gn5-c8g1.8xlarge|32|240.0|1760|4 \* NVIDIA P100|4 \* 16|10.0|2,000|8|8|20|
|ecs.gn5-c28g1.14xlarge|56|224.0|880|2 \* NVIDIA P100|2 \* 16|10.0|2,000|14|8|20|
|ecs.gn5-c8g1.14xlarge|54|480.0|3520|8 \* NVIDIA P100|8 \* 16|25.0|4,000|14|8|20|

**Note:** For more information, see [Create a compute optimized instance with GPUs](../../../../dita-oss-bucket/SP_2/DNA0011894323/reseller.en-US/Instances/Instance type families/Compute optimized type family with GPU/Create a compute optimized instance with GPU.md#).

See [other instance type families](#).

## gn5i, compute optimized type family with GPU {#gn5i .section}

**Features**

-   I/O-optimized
-   Supports SSD Cloud Disks and Ultra Disks
-   Uses NVIDIA P4 GPU processors
-   Equipped with a vCPU to memory ratio of 1:4
-   Equipped with 2.5 GHz Intel Xeon E5-2682 v4 \(Broadwell\) processors
-   Supports strong network performance through sufficient computing capacity
-   Suitable for the following scenarios:
    -   Deep learning
    -   Multi-media coding and decoding, and other server-side GPU compute workloads

**Instance types**

|Instance type|vCPU|Memory \(GiB\)|Local disks \(GiB\)[ \* ](#)|GPU|GPU memory \(GB\)|Bandwidth \(Gbit/s\)[ \*\* ](#)|Packet forwarding rate \(Thousand pps\)[ \*\*\* ](#)|NIC queues[ \*\*\*\* ](#)|ENIs[ \*\*\*\*\* ](#)|Private IP address of a single ENI|
|:------------|:---|:-------------|:---------------------------|:--|:----------------|:------------------------------|:---------------------------------------------------|:------------------------|:--------------------|----------------------------------|
|ecs.gn5i-c2g1.large|2|8.0|N/A|1 \* NVIDIA P4|1 \* 8|1.0|100|2|2|6|
|ecs.gn5i-c4g1.xlarge|4|16.0|N/A|1 \* NVIDIA P4|1 \* 8|1.5|200|2|3|10|
|ecs.gn5i-c8g1.2xlarge|8|32.0|N/A|1 \* NVIDIA P4|1 \* 8|2.0|400|4|4|10|
|ecs.gn5i-c16g1.4xlarge|16|64.0|N/A|1 \* NVIDIA P4|1 \* 8|3.0|800|4|8|10|
|ecs.gn5i-c16g1.8xlarge|32|128.0|N/A|2 \* NVIDIA P4|2 \* 8|6.0|1,200|8|8|20|
|ecs.gn5i-c28g1.14xlarge|56|224.0|N/A|2 \* NVIDIA P4|2 \* 8|10.0|2,000|14|8|20|

**Note:** For more information, see [Create a compute optimized instance with GPUs](../../../../dita-oss-bucket/SP_2/DNA0011894323/reseller.en-US/Instances/Instance type families/Compute optimized type family with GPU/Create a compute optimized instance with GPU.md#).

See [other instance type families](#).

## gn4, compute optimized type family with GPU {#gn4 .section}

**Features**

-   I/O-optimized
-   Supports SSD Cloud Disks and Ultra Disks
-   Uses NVIDIA M40 GPU processors
-   No fixed ratio of CPU to memory
-   Equipped with 2.5 GHz Intel Xeon E5-2682 v4 \(Broadwell\) processors
-   Supports strong network performance through sufficient computing capacity
-   Suitable for the following scenarios:
    -   Deep learning
    -   Scientific computing, such as computational fluid dynamics, computational finance, genomics, and environmental analysis
    -   High-performance computing, rendering, multi-media coding and decoding, and other server-side GPU compute workloads

**Instance types**

|Instance type|vCPU|Memory \(GiB\)|Local disks \(GiB\)[ \* ](#)|GPU|GPU memory \(GB\)|Bandwidth \(Gbit/s\)[ \*\* ](#)|Packet forwarding rate \(Thousand pps\)[ \*\*\* ](#)|NIC queues[ \*\*\*\* ](#)|ENIs[ \*\*\*\*\* ](#)|Private IP address of a single ENI|
|:------------|:---|:-------------|:---------------------------|:--|:----------------|:------------------------------|:---------------------------------------------------|:------------------------|:--------------------|----------------------------------|
|ecs.gn4-c4g1.xlarge|4|30.0|N/A|1 \* NVIDIA M40|1 \* 12|3.0|300|1|3|10|
|ecs.gn4-c8g1.2xlarge|8|30.0|N/A|1 \* NVIDIA M40|1 \* 12|3.0|400|1|4|10|
|ecs.gn4.8xlarge|32|48.0|N/A|1 \* NVIDIA M40|1 \* 12|6.0|800|3|8|20|
|ecs.gn4-c4g1.2xlarge|8|60.0|N/A|2 \* NVIDIA M40|2 \* 12|5.0|500|1|4|10|
|ecs.gn4-c8g1.4xlarge|16|60.0|N/A|2 \* NVIDIA M40|2 \* 12|5.0|500|1|8|20|
|ecs.gn4.14xlarge|56|96.0|N/A|2 \* NVIDIA M40|2 \* 12|10.0|1,200|4|8|20|

**Note:** For more information, see [Create a compute optimized instance with GPUs](../../../../dita-oss-bucket/SP_2/DNA0011894323/reseller.en-US/Instances/Instance type families/Compute optimized type family with GPU/Create a compute optimized instance with GPU.md#).

See [other instance type families](#).

## ga1, visualization compute type family with GPU {#ga1 .section}

**Features**

-   I/O-optimized
-   Supports SSD Cloud Disks and Ultra Disks
-   AMD S7150 GPU processors
-   Equipped with a vCPU to memory ratio of 1:2.5
-   Equipped with 2.5 GHz Intel Xeon E5-2682 v4 \(Broadwell\) processors
-   High-performance local NVMe SSD disks
-   Supports strong network performance through sufficient computing capacity
-   Suitable for the following scenarios:
    -   Rendering, multimedia coding and decoding
    -   Machine learning, high-performance computing, and high-performance databases
    -   Other server-end business scenarios that require powerful concurrent floating-point compute capabilities

**Instance types**

|Instance type|vCPU|Memory \(GiB\)|Local disks \(GiB\)[ \* ](#)|GPU|GPU memory \(GB\)|Bandwidth \(Gbit/s\)**[ \*\* ](#)**|Packet forwarding rate \(Thousand pps\)[ \*\*\* ](#)|NIC queues[ \*\*\*\* ](#)|ENIs[ \*\*\*\*\* ](#)|Private IP address of a single ENI|
|:------------|:---|:-------------|:---------------------------|:--|:----------------|:----------------------------------|:---------------------------------------------------|:------------------------|:--------------------|----------------------------------|
|ecs.ga1.xlarge|4|10.0|1 \* 87|0.25 \* AMD S7150|2|1.0|200|1|3|10|
|ecs.ga1.2xlarge|8|20.0|1 \* 175|0.5 \* AMD S7150|4|1.5|300|1|4|10|
|ecs.ga1.4xlarge|16|40.0|1 \* 350|1 \* AMD S7150|8|3.0|500|2|8|20|
|ecs.ga1.8xlarge|32|80.0|1 \* 700|2 \* AMD S7150|2 \* 8|6.0|800|3|8|20|
|ecs.ga1.14xlarge|56|160.0|1 \* 1400|4 \* AMD S7150|4 \* 8|10.0|1,200|4|8|20|

**Note:** For more information, see [Create an instance of ga1](../../../../reseller.en-US/Instances/Instance type families/Visualization compute type family with GPU/Create a ga1 instance.md#).

See [other instance type families](#).

## f1, compute optimized type family with FPGA {#f1 .section}

**Features**

-   I/O-optimized
-   Supports SSD Cloud Disks and Ultra Disks
-   Intel ARRIA 10 GX 1150 FPGA
-   Equipped with a vCPU to memory ratio of 1:7.5
-   Equipped with 2.5 GHz Intel Xeon E5-2682 v4 \(Broadwell\) processors
-   Supports strong network performance through sufficient computing capacity
-   Suitable for the following scenarios:
    -   Deep learning and reasoning
    -   Genomics research
    -   Financial analysis
    -   Picture transcoding
    -   Computational workloads, such as real-time video processing and security

**Instance types**

|Instance type|vCPU|Memory \(GiB\)|Local disks \(GiB\)[ \* ](#)|FPGA|Bandwidth \(Gbit/s\)[ \*\* ](#)|Packet forwarding rate \(Thousand pps\)[ \*\*\* ](#)|NIC queues[ \*\*\*\* ](#)|ENIs[ \*\*\*\*\* ](#)|Private IP address of a single ENI|
|:------------|:---|:-------------|:---------------------------|:---|:------------------------------|:---------------------------------------------------|:------------------------|:--------------------|----------------------------------|
|ecs.f1-c8f1.2xlarge|8|60.0|N/A|Intel ARRIA 10 GX 1150|3.0|400|4|4|10|
|ecs.f1-c8f1.4xlarge|16|120.0|N/A|2 \* Intel ARRIA 10 GX 1150|5.0|1,000|4|8|20|
|ecs.f1-c28f1.7xlarge|28|112.0|N/A|Intel ARRIA 10 GX 1150|5.0|2,000|8|8|20|
|ecs.f1-c28f1.14xlarge|56|224.0|N/A|2 \* Intel ARRIA 10 GX 1150|10.0|2,000|14|8|20|

See [other instance type families](#).

## f3, compute optimized type family with FPGA {#f3 .section}

**Features**

-   I/O-optimized
-   Supports SSD Cloud Disks and Ultra Disks
-   Xilinx 16nm Virtex UltraScale + VU9P
-   Equipped with a vCPU to memory ratio of 1:4
-   Equipped with 2.5 GHz Intel Xeon Platinum 8163 \(Skylake\) processors
-   Supports strong network performance through sufficient computing capacity
-   Suitable for the following scenarios:
    -   Deep learning and reasoning
    -   Genomics research
    -   Speeding up database access
    -   Picture transcoding, such as converting JPEG to WebP
    -   Real-time video processing, such as H.265 video compression

**Instance types**

|Instance type|vCPU|Memory \(GiB\)|Local disks \(GiB\)[ \* ](#)|FPGA|Bandwidth \(Gbit/s\)[ \*\* ](#)|Packet forwarding rate \(Thousand pps\)[ \*\*\* ](#)|NIC queues[ \*\*\*\* ](#)|ENIs[ \*\*\*\*\* ](#)|Private IP address of a single ENI|
|:------------|:---|:-------------|:---------------------------|:---|:------------------------------|:---------------------------------------------------|:------------------------|:--------------------|----------------------------------|
|ecs.f3-c4f1.xlarge|4|16.0|N/A|1 \* Xilinx VU9P|1.5|300|2|3|10|
|ecs.f3-c8f1.2xlarge|8|32.0|N/A|1 \* Xilinx VU9P|2.5|500|4|4|10|
|ecs.f3-c16f1.4xlarge|16|64.0|N/A|1 \* Xilinx VU9P|5.0|1,000|4|8|20|
|ecs.f3-c16f1.8xlarge|32|128.0|N/A|2 \* Xilinx VU9P|10.0|2,000|8|8|20|
|ecs.f3-c16f1.16xlarge|64|256.0|N/A|4 \* Xilinx VU9P|20.0|2,500|16|8|20|

See [other instance type families](#).

## ebmhfg5, ECS Bare Metal Instance type family with high clock speed {#ebmhfg5 .section}

**Features**

-   I/O-optimized
-   Supports SSD Cloud Disks and Ultra Disks
-   Equipped with a vCPU to memory ratio of 1:4
-   3.7 GHz Intel Xeon E3-1240v6 \(Skylake\) processors, 8-core vCPU, up to 4.1 GHz Turbo Boot
-   High network performance: 2 million pps packet forwarding rate
-   Supports VPC network only
-   Provides dedicated hardware resources and physical isolation
-   Supports Intel SGX
-   Suitable for the following scenarios:
    -   Workloads that require direct access to physical resources, or scenarios where binding a license to the hardware is required
    -   Gaming or financial applications featuring high performance
    -   High-performance Web servers
    -   Enterprise-level applications, such as high-performance databases

**Instance types**

|Instance type|vCPU|Memory \(GiB\)|Local disks \(GiB\)[ \* ](#)|Bandwidth \(Gbit/s\)[ \*\* ](#)|Packet forwarding rate \(Thousand pps\)[ \*\*\* ](#)|NIC queues[ \*\*\*\* ](#)|ENIs[ \*\*\*\*\* ](#)|Private IP address of a single ENI|
|:------------|:---|:-------------|:---------------------------|:------------------------------|:---------------------------------------------------|:------------------------|:--------------------|----------------------------------|
|ecs.ebmhfg5.2xlarge|8|32.0|N/A|6.0|2,000|8|6|8|

**Note:** For more information about ECS Bare Metal Instance, see [EBM Instance overview](reseller.en-US/Instances/Instance type families/ECS bare metal instance type family/EBM Instance overview.md#).

See [other instance type families](#).

## ebmc4, computing ECS Bare Metal Instance type family {#ebmc4 .section}

**Features**

-   I/O-optimized
-   Supports SSD Cloud Disks and Ultra Disks
-   Equipped with a vCPU to memory ratio of 1:2
-   Equipped with 2.5 GHz Intel Xeon E5-2682 v4 \(Broadwell\) processors, up to 2.9 GHz Turbo Boot
-   High network performance: 4 million pps packet forwarding rate
-   Supports VPC network only
-   Provides dedicated hardware resources and physical isolation
-   Suitable for the following scenarios:
    -   Scenarios where a large volume of packets are received and transmitted, such as the re-transmission of telecommunication information
    -   Third-party virtualization \(includes but is not limited to Xen and KVM\), and AnyStack \(includes but is not limited to OpenStack and ZStack\)
    -   Containers \(includes but is not limited to Docker, Clear Container, and Pouch\)
    -   Enterprise-level applications, such as medium and large databases
    -   Video coding

**Instance types**

|Instance type|vCPU|Memory \(GiB\)|Local disks \(GiB\)[ \* ](#)|Bandwidth \(Gbit/s\)[ \*\* ](#)|Packet forwarding rate \(Thousand pps\)[ \*\*\* ](#)|NIC queues[ \*\*\*\* ](#)|ENIs[ \*\*\*\*\* ](#)|Private IP address of a single ENI|
|:------------|:---|:-------------|:---------------------------|:------------------------------|:---------------------------------------------------|:------------------------|:--------------------|----------------------------------|
|ecs.ebmc4.8xlarge|32|64.0|N/A|10.0|4,000|8|12|10|

**Note:** For more information about ECS Bare Metal Instance, see [EBM Instance overview](reseller.en-US/Instances/Instance type families/ECS bare metal instance type family/EBM Instance overview.md#).

See [other instance type families](#).

## ebmg5, general-purpose ECS Bare Metal Instance type family {#ebmg5 .section}

**Features**

-   I/O-optimized
-   Supports SSD Cloud Disks and Ultra Disks
-   Equipped with a vCPU to memory ratio of 1:4
-   Equipped with 2.5 GHz Intel Xeon Platinum 8163 \(Skylake\) processors, 96-core vCPU, up to 2.7 GHz Turbo Boot
-   High network performance: 4 million pps packet forwarding rate
-   Supports VPC network only
-   Provides dedicated hardware resources and physical isolation
-   Suitable for the following scenarios:
    -   Workloads that require direct access to physical resources, or scenarios where binding a license to the hardware is required
    -   Third-party virtualization \(includes but is not limited to Xen and KVM\), and AnyStack \(includes but is not limited to OpenStack and ZStack\)
    -   Containers \(includes but is not limited to Docker, Clear Container, and Pouch\)
    -   Enterprise-level applications, such as medium and large databases
    -   Video encoding

**Instance types**

|Instance type|vCPU|Memory \(GiB\)|Local disks \(GiB\)[ \* ](#)|Bandwidth \(Gbit/s\)[ \*\* ](#)|Packet forwarding rate \(Thousand pps\)[ \*\*\* ](#)|NIC queues[ \*\*\*\* ](#)|ENIs[ \*\*\*\*\* ](#)|Private IP address of a single ENI|
|:------------|:---|:-------------|:---------------------------|:------------------------------|:---------------------------------------------------|:------------------------|:--------------------|----------------------------------|
|ecs.ebmg5.24xlarge|96|384.0|N/A|10.0|4,000|8|32|10|

**Note:** For more information about ECS Bare Metal Instance, see [EBM Instance overview](reseller.en-US/Instances/Instance type families/ECS bare metal instance type family/EBM Instance overview.md#).

See [other instance type families](#).

## scch5, Super Computing Cluster \(SCC\) instance type family with high clock speed {#scch5 .section}

**Features**

-   I/O-optimized
-   Supports SSD Cloud Disks and Ultra Disks
-   Supports both RoCE and VPC networks, of which RoCE is dedicated to RDMA communication
-   With all features of ECS Bare Metal Instance
-   3.1 GHz Intel Xeon Gold 6149 \(Skylake\) processors
-   Equipped with a vCPU to memory ratio of 1:3
-   Suitable for the following scenarios:
    -   Large-scale machine learning applications
    -   Large-scale high-performance scientific and engineering applications
    -   Large-scale data analysis, batch computing, video encoding

**Instance types**

|Instance type|vCPU|Physical core|Memory \(GiB\)|GPU|Bandwidth \(Gbit/s\)[ \*\* ](#)|Packet forwarding rate \(Thousand pps\)[ \*\*\* ](#)|RoCE \(Inbound/Outbound\) \(Gbit/s\)|NIC queues[ \*\*\*\* ](#)|ENIs[ \*\*\*\*\* ](#)|Private IP address of a single ENI|
|:------------|:---|-------------|:-------------|:--|:------------------------------|:---------------------------------------------------|:-----------------------------------|:------------------------|:--------------------|----------------------------------|
|ecs.scch5.16xlarge|64|32|192.0|N/A|10.0|4,500|46|8|32|10|

**Note:** The ecs.scch5.16xlarge instance type provides 64 logical processors on 32 physical cores. For more information about SCC, see [Super Computing Clusters](reseller.en-US/Instances/Instance type families/Super Computing Cluster instance type family/Super Computing Clusters.md#).

See [other instance type families](#).

## sccg5, general-purpose Super Computing Cluster \(SCC\) instance type family {#sccg5 .section}

**Features**

-   I/O-optimized
-   Supports SSD Cloud Disks and Ultra Disks
-   Supports both RoCE and VPC networks, of which RoCE is dedicated to RDMA communication
-   With all features of ECS Bare Metal Instance
-   Equipped with 2.5 GHz Intel Xeon Platinum 8163 \(Skylake\) processors
-   Equipped with a vCPU to memory ratio of 1:4
-   Suitable for the following scenarios:
    -   Large-scale machine learning applications
    -   Large-scale high-performance scientific and engineering applications
    -   Large-scale data analysis, batch computing, video encoding

**Instance types**

|Instance type|vCPU|Physical core|Memory \(GiB\)|GPU|Bandwidth \(Gbit/s\)[ \*\* ](#)|Packet forwarding rate \(Thousand pps\)[ \*\*\* ](#)|RoCE \(Inbound/Outbound\) \(Gbit/s\)|NIC queues[ \*\*\*\* ](#)|ENIs[ \*\*\*\*\* ](#)|Private IP address of a single ENI|
|:------------|:---|-------------|:-------------|:--|:------------------------------|:---------------------------------------------------|:-----------------------------------|:------------------------|:--------------------|----------------------------------|
|ecs.sccg5.24xlarge|96|48|384.0|N/A|10.0|4,500|46|8|32|10|

**Note:** The ecs.sccg5.24xlarge instance type provides 96 logical processors on 48 physical cores. For more information about SCC, see [Super Computing Clusters](reseller.en-US/Instances/Instance type families/Super Computing Cluster instance type family/Super Computing Clusters.md#).

See [other instance type families](#).

## sccgn6, compute optimized Super Computing Cluster \(SCC\) instance type family with GPUs {#sccgn6 .section}

**Features**

-   I/O-optimized
-   Equipped with a vCPU to memory ratio of 1:4
-   Equipped with 2.5 GHz Intel Xeon Platinum 8163 \(Skylake\) processors
-   With all features of ECS Bare Metal Instances
-   Storage:
    -   Supports ESSD Cloud Disks \(million-level IOPS\), SSD Cloud Disks, and Ultra Disks
    -   Supports high-performance Cloud Parallel File System \(CPFS\)
-   Networking:
    -   Supports VPC networks equipped with two 25Gbps ports
    -   Supports RoCE v2 networks, which is dedicated to RDMA communication
-   Uses NVIDIA V100 GPU processors \(with the SXM2 module\):
    -   Based on the new NVIDIA Volta architecture
    -   Up to 640 Tensor Cores
    -   Up to 5,120 CUDA Cores
    -   16 GB HBM2 GPU memory capacity \(900 GB/s bandwidth\)
    -   Supports up to six NVLink connections and total bandwidth of 300 GB/s \(25 GB/s per connection\)
-   Suitable for the following scenarios:
    -   Ultra-large-scale machine learning applications
    -   Large-scale high-performance scientific and emulation applications
    -   Large-scale data analysis, batch computing, video encoding

**Instance types**

|Instance types|vCPU|Memory \(GiB\)|Local disks \(GiB\)[ \* ](#)|GPU|Bandwidth \(Gbit/s\)[ \*\* ](#)|Packet forwarding rate \(Thousand pps\)[ \*\*\* ](#)|RoCE \(Inbound/Outbound\) \(Gbit/s\)|NIC queues[ \*\*\*\* ](#)|ENIs[ \*\*\*\*\* ](#)|Private IP address of a single ENI|
|:-------------|:---|:-------------|:---------------------------|:--|:------------------------------|:---------------------------------------------------|------------------------------------|:------------------------|:--------------------|----------------------------------|
|ecs.sccgn6.24xlarge|96|384|N/A|V100\*8|30|4,500|25\*2|8|32|10|

See [other instance type families](#).

## t5, burstable instances {#t5 .section}

**Features**

-   Equipped with 2.5 GHz Intel Xeon processors
-   The latest DDR4 memory
-   No fixed ratio of vCPU to memory
-   Baseline CPU performance, burstable, but restricted by accumulated CPU credits
-   Resource balance among compute, memory, and networks
-   Supports VPC network only
-   Suitable for the following scenarios:
    -   Web application servers
    -   Lightweight web servers
    -   Development and testing environments

**Instance types**

|Instance types|vCPU|Memory \(GiB\)|Avg baseline CPU performance|CPU credits/hour|Max CPU credit balance|Local disks \(GiB\)[ \* ](#)|Bandwidth \(Gbit/s\)[ \*\* ](#)|Packet forwarding rate \(Thousand pps\)[ \*\*\* ](#)|NIC queues[ \*\*\*\* ](#)|ENIs[ \*\*\*\* ](#)|Private IP address of a single ENI|
|:-------------|:---|--------------|:---------------------------|:---------------|:---------------------|----------------------------|-------------------------------|----------------------------------------------------|-------------------------|:------------------|----------------------------------|
|ecs.t5-lc2m1.nano|1|0.5|10%|6|144|N/A|0.1|40|1|1|2|
|ecs.t5-lc1m1.small|1|1.0|10%|6|144|N/A|0.2|60|1|1|2|
|ecs.t5-lc1m2.small|1|2.0|10%|6|144|N/A|0.2|60|1|1|2|
|ecs.t5-lc1m2.large|2|4.0|10%|12|288|N/A|0.4|100|1|1|2|
|ecs.t5-lc1m4.large|2|8.0|10%|12|288|N/A|0.4|100|1|1|2|
|ecs.t5-c1m1.large|2|2.0|15%|18|432|N/A|0.5|100|1|1|2|
|ecs.t5-c1m2.large|2|4.0|15%|18|432|N/A|0.5|100|1|1|2|
|ecs.t5-c1m4.large|2|8.0|15%|18|432|N/A|0.5|100|1|1|2|
|ecs.t5-c1m1.xlarge|4|4.0|15%|36|864|N/A|0.8|200|1|2|6|
|ecs.t5-c1m2.xlarge|4|8.0|15%|36|864|N/A|0.8|200|1|2|6|
|ecs.t5-c1m4.xlarge|4|16.0|15%|36|864|N/A|0.8|200|1|2|6|
|ecs.t5-c1m1.2xlarge|8|8.0|15%|72|1728|N/A|1.2|400|1|2|6|
|ecs.t5-c1m2.2xlarge|8|16.0|15%|72|1728|N/A|1.2|400|1|2|6|
|ecs.t5-c1m4.2xlarge|8|32.0|15%|72|1728|N/A|1.2|400|1|2|6|
|ecs.t5-c1m1.4xlarge|16|16.0|15%|144|3456|N/A|1.2|600|1|2|6|
|ecs.t5-c1m2.4xlarge|16|32.0|15%|144|3456|N/A|1.2|600|1|2|6|

**Note:** For more information about t5, see [Overview](reseller.en-US/Instances/Instance type families/Burstable performance instances/Overview.md#).

See [other instance type families](#).

## xn4/n4/mn4/e4, type families of previous generations for entry-level users, computing on the x86-architecture {#xn4-n4-mn4-e4 .section}

**Features**

-   Equipped with 2.5 GHz Intel Xeon E5-2682 v4 \(Broadwell\) processors
-   The latest DDR4 memory
-   No fixed ratio of CPU to memory

|Type family|Features|vCPU to memory ratio|Ideal for|
|:----------|:-------|:-------------------|:--------|
|xn4|Compact entry-level instances|1:1| -   Front ends of Web applications
-   Light load applications and microservices
-   Applications for development or testing environments

 |
|n4|General entry-level instances|1:2| -   Websites and Web applications
-   Development environment, building servers, code repositories, microservices, and testing and staging environment
-   Lightweight enterprise applications

 |
|mn4|Balanced entry-level instances|1:4| -   Websites and Web applications
-   Lightweight databases and caches
-   Integrated applications and lightweight enterprise services

 |
|e4|Memory entry-level instances|1:8| -   Applications that require large volume of memory
-   Lightweight databases and cache

 |

**xn4**

|Instance type|vCPU|Memory \(GiB\)|Local disks \(GiB\)[ \* ](#)|Bandwidth \(Gbit/s\)[ \*\* ](#)|Packet forwarding rate \(Thousand pps\)[ \*\*\* ](#)|NIC queues[ \*\*\*\* ](#)|ENIs[ \*\*\*\*\* ](#)|Private IP address of a single ENI|
|:------------|:---|:-------------|:---------------------------|:------------------------------|:---------------------------------------------------|:------------------------|:--------------------|----------------------------------|
|ecs.xn4.small|1|1.0|N/A|0.5|50|1|1|2|

**n4**

|Instance type|vCPU|Memory \(GiB\)|Local disks \(GiB\)[ \* ](#)|Bandwidth \(Gbit/s\)[ \*\* ](#)|Packet forwarding rate \(Thousand pps\)[ \*\*\* ](#)|NIC queues[ \*\*\*\* ](#)|ENIs[ \*\*\*\*\* ](#)|Private IP address of a single ENI|
|:------------|:---|:-------------|:---------------------------|:------------------------------|:---------------------------------------------------|:------------------------|:--------------------|----------------------------------|
|ecs.n4.small|1|2.0|N/A|0.5|50|1|1|2|
|ecs.n4.large|2|4.0|N/A|0.5|100|1|1|2|
|ecs.n4.xlarge|4|8.0|N/A|0.8|150|1|2|6|
|ecs.n4.2xlarge|8|16.0|N/A|1.2|300|1|2|6|
|ecs.n4.4xlarge|16|32.0|N/A|2.5|400|1|2|6|
|ecs.n4.8xlarge|32|64.0|N/A|5.0|500|1|2|6|

**mn4**

|Instance type|vCPU|Memory \(GiB\)|Local disks \(GiB\)[ \* ](#)|Bandwidth \(Gbit/s\)[ \*\* ](#)|Packet forwarding rate \(Thousand pps\)[ \*\*\* ](#)|NIC queues[ \*\*\*\* ](#)|ENIs[ \*\*\*\*\* ](#)|Private IP address of a single ENI|
|:------------|:---|:-------------|:---------------------------|:------------------------------|:---------------------------------------------------|:------------------------|:--------------------|----------------------------------|
|ecs.mn4.small|1|4.0|N/A|0.5|50|1|1|2|
|ecs.mn4.large|2|8.0|N/A|0.5|100|1|1|2|
|ecs.mn4.xlarge|4|16.0|N/A|0.8|150|1|2|6|
|ecs.mn4.2xlarge|8|32.0|N/A|1.2|300|1|2|6|
|ecs.mn4.4xlarge|16|64.0|N/A|2.5|400|1|2|6|
|ecs.mn4.8xlarge|32|128.0|N/A|5|500|2|8|6|

**e4**

|Instance type|vCPU|Memory \(GiB\)|Local disks \(GiB\)[ \* ](#)|Bandwidth \(Gbit/s\)[ \*\* ](#)|Packet forwarding rate \(Thousand pps\)[ \*\*\* ](#)|NIC queues[ \*\*\*\* ](#)|ENIs[ \*\*\*\*\* ](#)|Private IP address of a single ENI|
|:------------|:---|:-------------|:---------------------------|:------------------------------|:---------------------------------------------------|:------------------------|:--------------------|----------------------------------|
|ecs.e4.small|1|8.0|N/A|0.5|50|1|1|2|
|ecs.ce4.xlarge|2|16.0|N/A|0.5|100|1|1|2|
|ecs.ce4.xlarge|4|32.0|N/A|0.8|150|1|2|6|
|ecs.e4.2xlarge|8|64.0|N/A|1.2|300|1|3|6|
|ecs.ce4.xlarge|16|128.0|N/A|2.5|400|1|8|6|

See [other instance type families](#).

 \* Cache disks, or Local disks, are the disks located on the physical servers \(host machines\) that ECS instances are hosted on. They provide temporary block level storage for instances. Block storage capacity is measured in binary units. In some cases, such as when the computing resources of an instance, including CPU and memory, are released, or an instance is inactive while migration occurs, data on the local disks is erased. For more information, see [Local disks](../../../../reseller.en-US/Block Storage/Local disks.md#).

 \*\* The maximum sum of inbound and outbound bandwidth.

 \*\*\* The maximum sum of inbound and outbound packet forwarding rates. For more information about packet forwarding rate testing, see [Test network performance](https://partners-intl.aliyun.com/help/faq-detail/55757.htm).

 \*\*\*\* The maximum number of NIC queues that an instance type supports. If your instance is running CentOS 7.3, the maximum number of NIC queues is used by default.

 \*\*\*\*\* An enterprise-level instance with two or more vCPU cores supports elastic network interfaces. An entry-level instance with four or more vCPU cores supports elastic network interfaces. For more information, see [ENI overview](../../../../reseller.en-US/Network/Elastic Network Interfaces/ENI overview.md#).

