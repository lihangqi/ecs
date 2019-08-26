# EBM Instance overview {#concept_lnh_hv2_5db .concept}

This topic describes ECS Bare Metal \(EBM\) Instances and the instance type families that provide EBM Instance types \(specifically, high-clock speed type family ebmhfg5, compute type family ebmc4, and general-purpose type family ebmg5\).

## Background information {#section_mh2_uj0_w3p .section}

Alibaba Cloud EBM Instances use next-generation virtualization technology that supports multiple virtual cloud servers and nested virtualization while also maintaining excellent resource elasticity and a seamless user experience.

Compared with other available instance types, EBM Instances offer the following advantages:

-   **Exclusive computing resources** 

    EBM Instances provide better performance and isolation than standard physical servers and enable exclusive computing resources without virtualization performance overheads or feature loss. EBM Instances support 8, 32, and 96 CPU cores and ultra high frequencies. For example, an EBM Instance with 8 cores supports a frequency of up to 3.7 to 4.1 GHz.

-   **Chip-level security** 

    EBM Instances implement Intel® SGX, which allows EBM Instances to compute only encrypted data in a safe and trusted environment, providing advanced security for your data in the cloud. For more information, see [Install SGX](reseller.en-US/Instances/Instance type families/ECS bare metal instance type family/Install SGX.md#).

-   **Compatible with multiple private clouds** 

    EBM Instances supports re-virtualization. As a result, private cloud users can seamlessly migrate to Alibaba Cloud without experiencing performance overhead issues that typically occur in standard nested virtualization methods.

-   **Support for heterogeneous instruction set processors** 

    EBM Instances are based on proprietary virtualization 2.0 technology developed by Alibaba Cloud, which support ARM and other instruction set processors without incurring additional costs.


When you use EBM Instances, note the following:

-   The specifications of EBM Instances cannot be upgraded or downgraded.
-   If a hardware fault occurs to an EBM Instance, a failover occurs and data is stored in the cloud disks of the EBM Instance.

## Comparison of EBM Instances, physical machines, and virtual machines {#section_efq_x55_ydb .section}

The following table compares EBM Instance, physical servers, and virtual servers. In this table, Y means supported, N means not supported, and N/A means not applicable.

|Feature type|Feature|EBM Instance|Physical server|Virtual server|
|:-----------|:------|:-----------|:--------------|:-------------|
|Automated O&M|Delivery in minutes|Y|N|Y|
|Computing|Zero performance loss|Y|Y|N|
|Zero feature loss|Y|Y|N|
|Zero resource preemption|Y|Y|N|
|Storage|Compatible with ECS cloud disks|Y|N|Y|
|Started from cloud disks \(system disks\)|Y|N|Y|
|Quick resetting of the system disk|Y|N|Y|
|Compatible with ECS images|Y|N|Y|
|Cold migration between physical and virtual servers|Y|N|Y|
|Free of OS installation|Y|N|Y|
|Free of local RAID, and stronger protection of data in cloud disks|Y|N|Y|
|Network|Compatible with the ECS VPC networks|Y|N|Y|
|Compatible with the ECS classic networks|Y|N|Y|
|Free of communication bottlenecks between physical and virtual server clusters in the VPC|Y|N|Y|
|Management|Compatible with the existing ECS management system|Y|N|Y|
|Consistent user experience on VNC and other features with that of virtual servers|Y|N|Y|
|Out-of-band \(OOB\) network security|Y|N|N/A|

## ebmhfg5, ECS Bare Metal Instance type family with high clock speed {#section_cyd_dnh_grf .section}

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

|Instance type|vCPU|Memory \(GiB\)|Local disks \(GiB\)[ \* ](reseller.en-US/Instances/Instance type families.md#)|Bandwidth \(Gbit/s\)[ \*\* ](reseller.en-US/Instances/Instance type families.md#)|Packet forwarding rate \(Thousand pps\)[ \*\*\* ](reseller.en-US/Instances/Instance type families.md#)|NIC queues[ \*\*\*\* ](reseller.en-US/Instances/Instance type families.md#)|ENIs[ \*\*\*\*\* ](reseller.en-US/Instances/Instance type families.md#)|Private IP address of a single ENI|
|:------------|:---|:-------------|:-------------------------------------------|:----------------------------------------------|:-------------------------------------------------------------------|:----------------------------------------|:------------------------------------|----------------------------------|
|ecs.ebmhfg5.2xlarge|8|32.0|N/A|6.0|2,000|8|6|8|

**Note:** For more information about ECS Bare Metal Instance, see [EBM Instance overview](reseller.en-US/Instances/Instance type families/ECS bare metal instance type family/EBM Instance overview.md#).

See [other instance type families](reseller.en-US/Instances/Instance type families.md#).

## ebmc4, computing ECS Bare Metal Instance type family {#section_9nb_7d3_ni3 .section}

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

|Instance type|vCPU|Memory \(GiB\)|Local disks \(GiB\)[ \* ](reseller.en-US/Instances/Instance type families.md#)|Bandwidth \(Gbit/s\)[ \*\* ](reseller.en-US/Instances/Instance type families.md#)|Packet forwarding rate \(Thousand pps\)[ \*\*\* ](reseller.en-US/Instances/Instance type families.md#)|NIC queues[ \*\*\*\* ](reseller.en-US/Instances/Instance type families.md#)|ENIs[ \*\*\*\*\* ](reseller.en-US/Instances/Instance type families.md#)|Private IP address of a single ENI|
|:------------|:---|:-------------|:-------------------------------------------|:----------------------------------------------|:-------------------------------------------------------------------|:----------------------------------------|:------------------------------------|----------------------------------|
|ecs.ebmc4.8xlarge|32|64.0|N/A|10.0|4,000|8|12|10|

**Note:** For more information about ECS Bare Metal Instance, see [EBM Instance overview](reseller.en-US/Instances/Instance type families/ECS bare metal instance type family/EBM Instance overview.md#).

See [other instance type families](reseller.en-US/Instances/Instance type families.md#).

## ebmg5, general-purpose ECS Bare Metal Instance type family {#section_xim_xnu_sqe .section}

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

|Instance type|vCPU|Memory \(GiB\)|Local disks \(GiB\)[ \* ](reseller.en-US/Instances/Instance type families.md#)|Bandwidth \(Gbit/s\)[ \*\* ](reseller.en-US/Instances/Instance type families.md#)|Packet forwarding rate \(Thousand pps\)[ \*\*\* ](reseller.en-US/Instances/Instance type families.md#)|NIC queues[ \*\*\*\* ](reseller.en-US/Instances/Instance type families.md#)|ENIs[ \*\*\*\*\* ](reseller.en-US/Instances/Instance type families.md#)|Private IP address of a single ENI|
|:------------|:---|:-------------|:-------------------------------------------|:----------------------------------------------|:-------------------------------------------------------------------|:----------------------------------------|:------------------------------------|----------------------------------|
|ecs.ebmg5.24xlarge|96|384.0|N/A|10.0|4,000|8|32|10|

**Note:** For more information about ECS Bare Metal Instance, see [EBM Instance overview](reseller.en-US/Instances/Instance type families/ECS bare metal instance type family/EBM Instance overview.md#).

See [other instance type families](reseller.en-US/Instances/Instance type families.md#).

## Billing methods {#section_wfq_x55_ydb .section}

EBM Instances support Subscription and Pay-As-You-Go billing methods. For more information, see [Billing method comparison](../../../../reseller.en-US/Pricing/Billing method comparison.md#).

## Related document {#section_ady_2mb_8m5 .section}

For more information, see [EBM Instance FAQ](https://partners-intl.aliyun.com/help/faq-detail/66558.htm).

