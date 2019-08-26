# Phased-out instance types {#concept_t1v_lxw_wgb .concept}

This article lists all the phased out instance types.

## sn2, general purpose type family {#section_e1p_ttg_4gb .section}

**Features**

-   vCPU : Memory = 1:4
-   2.5 GHz Intel Xeon, E5-2682 v4 \(Broadwell\), or E5-2680 v3 \(Haswell\) processors
-   The network performance of an instance matching the computing type \(the more advanced the computing type, the more powerful the network performance\)
-   Ideal for:
    -   Enterprise-class applications of various types and sizes
    -   Medium and small database systems, cache, and search clusters
    -   Data analysis and computing
    -   Computing clusters, and data processing depending on memory

**Instance types**

|Instance type|vCPU\*|Memory \(GiB\)|Local disks \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(Thousand pps\)\*\*|NIC queues\*\*\*|ENIs \(Including 1 primary ENI\)|
|-------------|------|--------------|-------------------|--------------------|-------------------------------------------|----------------|--------------------------------|
|ecs.sn2.medium|2|8.0|N/A|0.5|100|1|2|
|ecs.sn2.large|4|16.0|N/A|0.8|200|1|3|
|ecs.sn2.xlarge|8|32.0|N/A|1.5|400|1|4|
|ecs.sn2.3xlarge|16|64.0|N/A|3.0|500|2|8|
|ecs.sn2.7xlarge|32|128.0|N/A|6.0|800|3|8|
|ecs.sn2.13xlarge|56|224.0|N/A|10.0|1,200|4|8|

\* An enterprise-level instance with 2 or more vCPU cores supports elastic network interfaces. For more information, see [Elastic network interfaces](../../../../reseller.en-US/Network/Elastic Network Interfaces/ENI overview.md#).

\*\* The maximum packet forwarding rate of inbound or outbound traffic. For more information about packet forwarding rate testing, see [Test network performance](https://partners-intl.aliyun.com/help/faq-detail/55757.htm).

\*\*\* The maximum number of NIC queues that an instance type supports. If your instance is running CentOS 7.3, the maximum number of NIC queues is used by default. For more information about NIC multi-queue, see [Multi-queue for NICs](../../../../reseller.en-US/Network/Multiqueue for NICs.md#).

**Note:** You can change the configurations of an instance between any two type families of sn2, [sn2ne](reseller.en-US/Instances/Instance type families.md#sn2ne000), sn1, [sn1ne](reseller.en-US/Instances/Instance type families.md#sn1ne), [se1](reseller.en-US/Instances/Instance type families.md#se1), and [se1ne](reseller.en-US/Instances/Instance type families.md#se1ne), and within the same instance type family.

## sn1, compute optimized type family {#section_d3f_11h_4gb .section}

**Features**

-   vCPU : Memory = 1:2
-   2.5 GHz Intel Xeon, E5-2682 v4 \(Broadwell\), or E5-2680 v3 \(Haswell\) processors
-   The network performance of an instance matching the computing type \(the more advanced the computing type, the more powerful the network performance\)
-   Ideal for:
    -   Web front-end servers
    -   Front ends of Massively Multiplayer Online \(MMO\) games
    -   Data analysis, batch compute, and video coding
    -   High performance science and engineering applications

**Instance types**

|Instance type|vCPU\*|Memory \(GiB\)|Local disks \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(Thousand pps\)\*\*|NIC queues\*\*\*|ENIs \(Including 1 primary ENI\)|
|-------------|------|--------------|-------------------|--------------------|-------------------------------------------|----------------|--------------------------------|
|ecs.sn1.medium|2|4.0|N/A|0.5|100|1|2|
|ecs.sn1.large|4|8.0|N/A|0.8|200|1|3|
|ecs.sn1.xlarge|8|16.0|N/A|1.5|400|1|4|
|ecs.sn1.3xlarge|16|32.0|N/A|3.0|500|2|8|
|ecs.sn1.7xlarge|32|64.0|N/A|6.0|800|3|8|

\* An enterprise-level instance with 2 or more vCPU cores supports elastic network interfaces. For more information, see [Elastic network interfaces](../../../../reseller.en-US/Network/Elastic Network Interfaces/ENI overview.md#).

\*\* The maximum packet forwarding rate of inbound or outbound traffic. For more information about packet forwarding rate testing, see [Test network performance](https://partners-intl.aliyun.com/help/faq-detail/55757.htm).

\*\*\* The maximum number of NIC queues that an instance type supports. If your instance is running CentOS 7.3, the maximum number of NIC queues is used by default. For more information about NIC multi-queue, see [Multi-queue for NICs](../../../../reseller.en-US/Network/Multiqueue for NICs.md#).

**Note:** You can change the configurations of an instance between any two type families of sn2, [sn2ne](reseller.en-US/Instances/Instance type families.md#sn2ne000), sn1, [sn1ne](reseller.en-US/Instances/Instance type families.md#sn1ne), [se1](reseller.en-US/Instances/Instance type families.md#se1), and [se1ne](reseller.en-US/Instances/Instance type families.md#se1ne), and within the same instance type family.

## **c4/ce4/cm4, compute optimized type families with high clock speed** {#section_gpl_n1h_4gb .section}

**Features**

-   I/O-optimized
-   Supports SSD Cloud Disks and Ultra Cloud Disks
-   Stable performance
-   3.2 GHz Intel Xeon E5-2667 v4 \(Broadwell\) processors
-   Higher computing specifications matching higher network performance
-   Ideal for:
    -   High performance Web front-end servers
    -   High performance science and engineering applications
    -   Massively Multiplayer Online \(MMO\) games and video coding

**c4**

|Instance type|vCPU\*|Memory \(GiB\)|Local disks \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(Thousand pps\)\*\*|NIC queues\*\*\*|ENIs|
|-------------|------|--------------|-------------------|--------------------|-------------------------------------------|----------------|----|
|ecs.c4.xlarge|4|8.0|N/A|1.5|200|1|3|
|ecs.c4.2xlarge|8|16.0|N/A|3.0|400|1|4|
|ecs.c4.3xlarge|12|24.0|N/A|4.5|600|2|6|
|ecs.c4.4xlarge|16|32.0|N/A|6.0|800|2|8|

**ce4**

|Instance type|vCPU\*|Memory \(GiB\)|Local disks \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(Thousand pps\)\*\*|NIC queues\*\*\*|ENIs|
|-------------|------|--------------|-------------------|--------------------|-------------------------------------------|----------------|----|
|ecs.ce4.xlarge|4|32.0|N/A|1.5|200|1|3|
|ecs.ce4.2xlarge|8|64.0|N/A|3.0|400|1|3|

**cm4**

|Instance type|vCPU\*|Memory \(GiB\)|Local disks \(GiB\)|Bandwidth \(Gbit/s\)|Packet forwarding rate \(Thousand pps\)\*\*|NIC queues\*\*\*|ENIs|
|-------------|------|--------------|-------------------|--------------------|-------------------------------------------|----------------|----|
|ecs.cm4.xlarge|4|16.0|N/A|1.5|200|1|3|
|ecs.cm4.2xlarge|8|32.0|N/A|3.0|400|1|4|
|ecs.cm4.3xlarge|12|48.0|N/A|4.5|600|2|6|
|ecs.cm4.4xlarge|16|64.0|N/A|6.0|800|2|8|
|ecs.cm4.6xlarge|24|96.0|N/A|10.0|1,200|4|8|

\* An enterprise-level instance with 2 or more vCPU cores supports elastic network interfaces. For more information, see [Elastic network interfaces](../../../../reseller.en-US/Network/Elastic Network Interfaces/ENI overview.md#).

\*\* The maximum packet forwarding rate of inbound or outbound traffic. For more information about packet forwarding rate testing, see [Test network performance](https://partners-intl.aliyun.com/help/faq-detail/55757.htm).

\*\*\* The maximum number of NIC queues that an instance type supports. If your instance is running CentOS 7.3, the maximum number of NIC queues is used by default. For more information about NIC multi-queue, see [Multi-queue for NICs](../../../../reseller.en-US/Network/Multiqueue for NICs.md#).

## n1/n2/e3, Entry-level instance type families {#section_z2t_5ch_4gb .section}

**Features**

-   2.5 GHz Intel Xeon E5-2680 v3 \(Haswell\) processors
-   Higher computing specifications matching higher network performance
-   I/O-optimized
-   Supporting the following disk types:
    -   SSD Cloud Disks
    -   Ultra Cloud Disks

|Type family|Features|vCPU : Memory|Idea for|
|-----------|--------|-------------|--------|
|n1|General entry-level instances|1:2| -   Small and medium-sized web servers
-   Batch processing
-   Distributed analysis
-   Advertisement services

 |
|n2|Balanced entry-level instances|1:4| -   Medium-sized Web servers
-   Batch processing
-   Distributed analysis
-   Advertisement services
-   Hadoop clusters

 |
|e3|Memory entry-level instances|1:8| -   Cache, Redis
-   Search
-   Memory databases
-   Databases with high I/O. For example, Oracle and MongoDB
-   Hadoop clusters
-   Computing scenarios that involve massive data processing

 |

**n1**

|Instance type|vCPU\*|Memory \(GiB\)|Local disks \(GiB\)|ENIs \(Including 1 primary ENI\)|
|-------------|------|--------------|-------------------|--------------------------------|
|ecs.n1.tiny|1|1.0|N/A|1|
|ecs.n1.small|1|2.0|N/A|1|
|ecs.n1.medium|2|4.0|N/A|1|
|ecs.n1.large|4|8.0|N/A|2|
|ecs.n1.xlarge|8|16.0|N/A|2|
|ecs.n1.3xlarge|16|32.0|N/A|2|
|ecs.n1.7xlarge|32|64.0|N/A|2|

\* An enterprise-level instance with 4 or more vCPU cores supports elastic network interfaces. For more information, see [Elastic network interfaces](../../../../reseller.en-US/Network/Elastic Network Interfaces/ENI overview.md#).

**n2**

|Instance type|vCPU\*|Memory \(GiB\)|Local disks \(GiB\)|ENIs \(Including 1 primary ENI\)|
|-------------|------|--------------|-------------------|--------------------------------|
|ecs.n2.small|1|4.0|N/A|1|
|ecs.n2.medium|2|8.0|N/A|1|
|ecs.n2.large|4|16.0|N/A|2|
|ecs.n2.xlarge|8|32.0|N/A|2|
|ecs.n2.3xlarge|16|64.0|N/A|2|
|ecs.n2.7xlarge|32|128.0|N/A|2|

\* An enterprise-level instance with 4 or more vCPU cores supports elastic network interfaces. For more information, see [Elastic network interfaces](../../../../reseller.en-US/Network/Elastic Network Interfaces/ENI overview.md#).

**e3**

|Instance type|vCPU\*|Memory \(GiB\)|Local disks \(GiB\)|ENIs \(Including 1 primary ENI\)|
|-------------|------|--------------|-------------------|--------------------------------|
|ecs.e3.small|1|8.0|N/A|1|
|ecs.e3.medium|2|16.0|N/A|1|
|ecs.e3.large|4|32.0|N/A|2|
|ecs.e3.xlarge|8|64.0|N/A|2|
|ecs.e3.3xlarge|16|128.0|N/A|2|

\* An enterprise-level instance with 4 or more vCPU cores supports elastic network interfaces. For more information, see [Elastic network interfaces](../../../../reseller.en-US/Network/Elastic Network Interfaces/ENI overview.md#).

**Note:** You can change the configurations among the three entry-level instance type families, including n1, n2, and e3, and within the same instance type family.

## Instance types of Generation I {#section_ilt_c3h_4gb .section}

Instance types of Generation I include t1, s1, s2, s3, m1, m2, c1, and c2. All these instance types are legacy shared instance types. They are still categorized by the number of cores \(1, 2, 4, 8, and 16 cores\) and are not sensitive to type families.

**Note:** For information about intance type families of Generation II and Generation III, see [Instance type families](reseller.en-US/Instances/Instance type families.md#).

**Features**

-   1.9 GHz Intel Xeon E5-2420 processors or higher
-   The latest DDR3 memory
-   [I/O-optimized](#) and [non I/O-optimized](#) at your choice

**I/O-optimized instance types**

I/O-optimized instances support two types of disks:

-   SSD cloud disk
-   Ultra cloud disk

|Specification types|Type code|vCPU|Memory \(GiB\)|
|-------------------|---------|----|--------------|
|Standard|ecs.s2.large|2|4|
|ecs.s2.xlarge|2|8|
|ecs.s2.2xlarge|2|16|
|ecs.s3.medium|4|4|
|ecs.s3.large|4|8|
|High Memory|ecs.m1.medium|4|16|
|ecs.m2.medium|4|32|
|ecs.m1.xlarge|8|32|
|High CPU|ecs.c1.small|8|8|
|ecs.c1.large|8|16|
|ecs.c2.medium|16|16|
|ecs.c2.large|16|32|
|ecs.c2.xlarge|16|64|

**Non I/O-optimized instance types**

Non I/O-optimized instances only support basic cloud disks.

|Specification types|Instance type|vCPU|Memory \(GiB\)|
|-------------------|-------------|----|--------------|
|Tiny|ecs.t1.small|1|1|
|Standard|ecs.s1.small|1|2|
|ecs.s1.medium|1|4|
|ecs.s1.large|1|8|
|ecs.s2.small|2|2|
|ecs.s2.large|2|4|
|ecs.s2.xlarge|2|8|
|ecs.s2.2xlarge|2|16|
|ecs.s3.medium|4|4|
|ecs.s3.large|4|8|
|High Memory|ecs.m1.medium|4|16|
|ecs.m2.medium|4|32|
|ecs.m1.xlarge|8|32|
|High CPU|ecs.c1.small|8|8|
|ecs.c1.large|8|16|
|ecs.c2.medium|16|16|
|ecs.c2.large|16|32|
|ecs.c2.xlarge|16|64|

**Configuration change between different types**

You can change the configuration among the eight categories of shared instance types \(t1, s1, s2, s3, m1, m2, c1, and c2\), and within the same category of instance type.

