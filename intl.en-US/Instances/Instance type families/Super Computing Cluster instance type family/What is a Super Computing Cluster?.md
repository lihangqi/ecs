# What is a Super Computing Cluster? {#concept_ptr_t5z_wgb .concept}

This topic describes Super Computing Clusters \(SCCs\) and the following SCC instance families and their instance types: scch5 instance family with high clock speed, sccg5 general purpose instance family, and sccgn6 compute optimized GPU instance family.

## Overview {#section_zw1_ng4_1fb .section}

SCCs are based on ECS Bare Metal Instances. With the high-speed interconnects of Remote Direct Memory Access \(RDMA\) technology, SCCs greatly improve network performance and the acceleration ratio of large-scale clusters. Therefore, SCCs have all the benefits of ECS Bare Metal Instances and offer high-quality network performance featuring high bandwidth and low latency.

SCCs are released by Alibaba Cloud to meet the demands of applications such as high performance computing, artificial intelligence, machine learning, scientific and engineering computing, data analysis, and audio and video processing. In the clusters, nodes are connected over RDMA networks featuring high bandwidth and low latency, which guarantee the parallel efficiency demanded by applications that require high performance computing. The RDMA over Convergent Ethernet \(RoCE\) rivals an InfiniBand network in terms of connection speed and supports more extensive Ethernet-based applications.

The combination of SCCs and other Alibaba Cloud computing products such as ECS and GPU instances provides Elastic HPC with the ultimate high performance parallel computing resources, making supercomputing on the cloud a reality.

## Comparison of SCCs, physical machines, and virtual machines {#section_efq_x55_ydb .section}

The following table shows a comparison of features. In this table, Y means supported, N means not supported, and N/A means not applicable.

|Feature type|Feature|SCC|Physical machine|Virtual machine|
|:-----------|:------|:--|:---------------|:--------------|
|Automated O&M|Delivery in minutes|Y|N|Y|
|Computing|Zero performance loss|Y|Y|N|
|Zero feature loss|Y|Y|N|
|Zero resource preemption|Y|Y|N|
|Storage|Compatible with ECS disks|Y|N|Y|
|Startup from disks \(system disks\)|Y|N|Y|
|Quick reset of system disks|Y|N|Y|
|Compatible with ECS images|Y|N|Y|
|Cold migration between physical and virtual machines|Y|N|Y|
|Free of OS installation|Y|N|Y|
|Free of local RAID, and stronger protection of data in disks|Y|N|Y|
|Network|Compatible with ECS VPC networks|Y|N|Y|
|Compatible with ECS classic networks|Y|N|Y|
|Free of communication bottlenecks between physical and virtual machine clusters in VPC|Y|N|Y|
|Management|Compatible with existing ECS management systems|Y|N|Y|
|Consistent user experiences on VNC and other features with that of virtual machines|Y|N|Y|
|Out-of-band \(OOB\) network security|Y|N|N/A|

## scch5, SCC instance type family with high clock speed {#section_o3g_ifk_1fs .section}

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

## sccg5, general purpose SCC instance family {#section_rcg_pie_45u .section}

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

## sccgn6, compute optimized SCC GPU instance family {#section_u4r_jvq_5b1 .section}

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

## Billing methods {#section_wfq_x55_ydb .section}

SCC supports monthly and yearly subscription billing methods. For more information, see [Billing method comparison](../../../../reseller.en-US/Pricing/Billing method comparison.md#).

