# **Super Computing Clusters** {#concept_ptr_t5z_wgb .concept}

This topic describes the features of three Super Computing Cluster \(SCC\) instance type families: scch5, sccg5, and sccgn6. The instance type family scch5 features high clock speed, sccg5 is for general use scenarios, and sccgn6 is compute optimized. Their specific instance types are also provided.

## Overview {#section_zw1_ng4_1fb .section}

SCCs are based on ECS Bare Metal \(EBM\) Instances. Given the high-speed interconnects of Remote Direct Memory Access \(RDMA\) technology, SCCs greatly improve network performance and the acceleration ratio of large-scale clusters. Therefore, SCCs have all the benefits of EBM Instances and offer high-quality network performance featuring high bandwidth and low latency.

SCCs are released by Alibaba Cloud to meet the demands of applications such as high performance computing, artificial intelligence, machine learning, scientific or engineering computing, data analysis, and audio and video processing. In the clusters, nodes are connected by RDMA networks featuring high bandwidth and low latency, which guarantee the parallel efficiency demanded by applications that require high-performance computing. The RDMA over Convergent Ethernet \(RoCE\) rivals an Infiniband network in terms of connection speed and supports more extensive Ethernet-based applications.

The combination of SCCs and other Alibaba Cloud computing products such as ECS and GPU instances provides the Alibaba Cloud elastic high-performance computing \(E-HPC\) platform with the ultimate high performance parallel computing resources, making supercomputing on the cloud a reality.

## Comparison of SCCs to physical and virtual servers {#section_efq_x55_ydb .section}

The following table compares SCC, physical servers, and virtual servers.

|Metric|Feature|SCC|Physical server|Virtual server|
|:-----|:------|:--|:--------------|:-------------|
|Automated O&M|Delivery in minutes|Yes|No|Yes|
|Computing|Zero performance loss|Yes|Yes|No|
|Zero feature loss|Yes|Yes|No|
|Zero resource competition|Yes|Yes|No|
|Storage|Fully compatible with ECS cloud disks|Yes|No|Yes|
|Start from cloud disks \(system disks\)|Yes|No|Yes|
|System disk can be quickly reset|Yes|No|Yes|
|Uses ECS images|Yes|No|Yes|
|Supports cold migration between physical and virtual servers|Yes|No|Yes|
|Requires no installation of operating system|Yes|No|Yes|
|Discards local RAID, and provides stronger protection of data on cloud disks|Yes|No|Yes|
|Network|Fully compatible with ECS VPCs|Yes|No|Yes|
|Fully compatible with the ECS classic network|Yes|No|Yes|
|Free of bottlenecks for communications between physical and virtual server clusters in a VPC|Yes|No|Yes|
|Management|Fully compatible with the existing ECS management system|Yes|No|Yes|
|Consistent user experience with virtual servers regarding VNC and other features|Yes|No|Yes|
|Guaranteed out of band network security|Yes|No|No|

## scch5, Super Computing Cluster \(SCC\) instance type family with high clock speed {#section_azk_dj2_xgb .section}

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

|Instance type|vCPU|Physical core|Memory \(GiB\)|GPU|Bandwidth \(Gbit/s\)[ \*\* ](reseller.en-US/Instances/Instance type families.md#)|Packet forwarding rate \(Thousand pps\)[ \*\*\* ](reseller.en-US/Instances/Instance type families.md#)|RoCE \(Inbound/Outbound\) \(Gbit/s\)|NIC queues[ \*\*\*\* ](reseller.en-US/Instances/Instance type families.md#)|ENIs[ \*\*\*\*\* ](reseller.en-US/Instances/Instance type families.md#)|
|:------------|:---|-------------|:-------------|:--|:----------------------------------------------|:-------------------------------------------------------------------|:-----------------------------------|:----------------------------------------|:------------------------------------|
|ecs.scch5.16xlarge|64|32|192.0|N/A|10.0|4,500|46|8|32|

**Note:** The ecs.scch5.16xlarge instance type provides 64 logical processors on 32 physical cores. For more information about SCC, see [Super Computing Clusters](reseller.en-US/Instances/Instance type families/Super Computing Cluster instance type family/Super Computing Clusters.md#).

See [other instance type families](reseller.en-US/Instances/Instance type families.md#).

## sccg5, geneneral-purpose Super Computing Cluster \(SCC\) instance type family {#section_mxg_2j2_xgb .section}

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

|Instance type|vCPU|Physical core|Memory \(GiB\)|GPU|Bandwidth \(Gbit/s\)[ \*\* ](reseller.en-US/Instances/Instance type families.md#)|Packet forwarding rate \(Thousand pps\)[ \*\*\* ](reseller.en-US/Instances/Instance type families.md#)|RoCE \(Inbound/Outbound\) \(Gbit/s\)|NIC queues[ \*\*\*\* ](reseller.en-US/Instances/Instance type families.md#)|ENIs[ \*\*\*\*\* ](reseller.en-US/Instances/Instance type families.md#)|
|:------------|:---|-------------|:-------------|:--|:----------------------------------------------|:-------------------------------------------------------------------|:-----------------------------------|:----------------------------------------|:------------------------------------|
|ecs.sccg5.24xlarge|96|48|384.0|N/A|10.0|4,500|46|8|32|

**Note:** The ecs.sccg5.24xlarge instance type provides 96 logical processors on 48 physical cores. For more information about SCC, see [Super Computing Clusters](reseller.en-US/Instances/Instance type families/Super Computing Cluster instance type family/Super Computing Clusters.md#).

See [other instance type families](reseller.en-US/Instances/Instance type families.md#).

## sccgn6, compute optimized Super Computing Cluster \(SCC\) instance type family with GPUs {#section_bf2_3ml_jhb .section}

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
    -   16 GB HBM2 memory capacity \(900 GB/s bandwidth\)
    -   Supports up to six NVLink connections and total bandwidth of 300 GB/s \(25 GB/s per connection\)
-   Suitable for the following scenarios:
    -   Ultra-large-scale machine learning applications
    -   Large-scale high-performance scientific and emulation applications
    -   Large-scale data analysis, batch computing, video encoding

**Instance types**

|Instance types|vCPU|Memory \(GiB\)|Local disks \(GiB\)[ \* ](reseller.en-US/Instances/Instance type families.md#)|GPU|Bandwidth \(Gbit/s\)[ \*\* ](reseller.en-US/Instances/Instance type families.md#)|Packet forwarding rate \(Thousand pps\)[ \*\*\* ](reseller.en-US/Instances/Instance type families.md#)|RoCE \(Inbound/Outbound\) \(Gbit/s\)|IPv6-ready?|NIC queues[ \*\*\*\* ](reseller.en-US/Instances/Instance type families.md#)|ENIs[ \*\*\*\*\* ](reseller.en-US/Instances/Instance type families.md#)|
|:-------------|:---|:-------------|:-------------------------------------------|:--|:----------------------------------------------|:-------------------------------------------------------------------|------------------------------------|:----------|:----------------------------------------|:------------------------------------|
|ecs.sccgn6.24xlarge|96|384|N/A|V100\*8|30|4,500|25\*2|Yes|8|32|

See [other instance type families](reseller.en-US/Instances/Instance type families.md#).

## Billing methods {#section_wfq_x55_ydb .section}

SCC instances support the Subscription billing method. For more information about billing methods, see [Billing method comparison.](../../../../reseller.en-US/Pricing/Billing method comparison.md#)

## Related documents {#section_xfq_x55_ydb .section}

For more information, see [SCC FAQ](https://partners-intl.aliyun.com/help/faq-detail/89878.htm).

