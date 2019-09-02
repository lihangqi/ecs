# What is an ECS Bare Metal Instance? {#concept_lnh_hv2_5db .concept}

This topic describes ECS Bare Metal Instances and the following instance families and their instance types: ebmc5s compute optimized instance family with enhanced network performance, ebmg5s general purpose instance family with enhanced network performance, ebmr5s memory optimized instance family with enhanced network performance, ebmhfg5 instance family with high clock speed, ebmc4 compute optimized instance family, and ebmg5 general purpose instance family.

## ECS Bare Metal Instance overview {#section_onk_y55_ydb .section}

ECS Bare Metal Instances are a computing service that combines the elasticity of virtual machines and the performance and features of physical machines. ECS Bare Metal Instances are designed based on the state-of-the-art virtualization 2.0 technology developed by Alibaba Cloud. The virtualization used by ECS Bare Metal Instances is optimized to support common ECS instances and nested virtualization, maintaining the elastic performance and user experience of physical machines.

ECS Bare Metal Instances combine the strengths of both physical machines and ECS instances to deliver powerful and robust computing capabilities. With the virtualization 2.0 technology, ECS Bare Metal Instances provide your business applications with direct access to the processor and memory resources of the underlying servers without virtualization overheads. ECS Bare Metal Instances keep the hardware feature sets \(such as Intel® VT-x\) and resource isolation capabilities of physical machines, ideal for applications that need to run in non-virtualization environments.

By virtue of the independently developed chips and hypervisor system software and the redefined server hardware architecture, ECS Bare Metal Instances deeply integrate features from both physical and virtual machines. ECS Bare Metal Instances can seamlessly connect with other Alibaba Cloud products for storage, networking, and database tasks. ECS Bare Metal Instances are fully compatible with ECS instance images. These properties allow you to build resources to suit your business requirements.

ECS Bare Metal Instances provide the following benefits through technological innovation:

-   Exclusive computing resources

    ECS Bare Metal Instances provide better performance and resource isolation than standard physical machines and can ensure the exclusivity of computing resources without virtualization overhead or feature loss. ECS Bare Metal Instances support ultrahigh-frequency instances and can contain 8, 32, or 96 vCPUs. An ECS Bare Metal Instance with eight vCPUs can provide a core frequency of 3.7 to 4.1 GHz for better performance and faster response for gaming and finance businesses than peer services.

-   Chip-level security

    ECS Bare Metal Instances implement Intel ® SGX, which allows ECS Bare Metal Instances to compute only encrypted data in a safe and trusted environment, to provide advanced security for cloud data. For more information, see [Install SGX](reseller.en-US/Instances/Instance type families/ECS bare metal instance type family/Install SGX.md#).

-   Compatible with multiple private clouds

    ECS Bare Metal Instances can address the needs of high-performance computing and help you build new hybrid clouds. Thanks to the flexibility, elasticity, and other strengths inherited from the mix of physical and virtual machines, ECS Bare Metal Instances can implement re-virtualization. Offline private clouds can be seamlessly migrated to Alibaba Cloud without the performance overheads that may arise from nested virtualization, giving you a new method to move businesses onto the cloud.

-   Support for heterogeneous instruction set processors

    The virtualization 2.0 technology used by ECS Bare Metal Instances is developed independently by Alibaba Cloud, and supports ARM and other instruction set processors at no additional cost.


When you use ECS Bare Metal Instances, note the following items:

-   ECS Bare Metal Instances cannot be upgraded or downgraded.
-   If a hardware fault occurs to an ECS Bare Metal Instance, a failover occurs and data is stored in the disks of the ECS Bare Metal Instance.

## Comparison of ECS Bare Metal Instances, physical machines, and virtual machines {#section_efq_x55_ydb .section}

The following table shows a comparison of features. In this table, Y means supported, N means not supported, and N/A means not applicable.

|Feature type|Feature|ECS Bare Metal Instance|Physical machine|Virtual machine|
|:-----------|:------|:----------------------|:---------------|:--------------|
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

**Note:** 

-   您可以前往[ECS实例可购买地域](https://ecs-buy4service.aliyun.com/instanceTypes/#/instanceTypeByRegion)，查看本实例的可购情况。
-   For more information about these specifications, see [EN-US\_TP\_9548.md\#section\_e9r\_xkf\_z15](reseller.en-US/Instances/Instance type families.md#section_e9r_xkf_z15).

## ebmc5s, compute optimized ECS Bare Metal Instance family with enhanced network performance {#section_pnq_v2c_u07 .section}

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

-   您可以前往[ECS实例可购买地域](https://ecs-buy4service.aliyun.com/instanceTypes/#/instanceTypeByRegion)，查看本实例的可购情况。
-   For more information about these specifications, see [EN-US\_TP\_9548.md\#section\_e9r\_xkf\_z15](reseller.en-US/Instances/Instance type families.md#section_e9r_xkf_z15).

## ebmg5s, general purpose ECS Bare Metal Instance family with enhanced network performance {#section_qiz_xda_sce .section}

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

-   您可以前往[ECS实例可购买地域](https://ecs-buy4service.aliyun.com/instanceTypes/#/instanceTypeByRegion)，查看本实例的可购情况。
-   For more information about these specifications, see [EN-US\_TP\_9548.md\#section\_e9r\_xkf\_z15](reseller.en-US/Instances/Instance type families.md#section_e9r_xkf_z15).

## ebmr5s, memory optimized ECS Bare Metal Instance family with enhanced network performance {#section_v7p_ot4_f4n .section}

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

-   您可以前往[ECS实例可购买地域](https://ecs-buy4service.aliyun.com/instanceTypes/#/instanceTypeByRegion)，查看本实例的可购情况。
-   For more information about these specifications, see [EN-US\_TP\_9548.md\#section\_e9r\_xkf\_z15](reseller.en-US/Instances/Instance type families.md#section_e9r_xkf_z15).

## ebmhfg5, ECS Bare Metal Instance family with high clock speed {#section_69a_h1f_n9m .section}

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

-   您可以前往[ECS实例可购买地域](https://ecs-buy4service.aliyun.com/instanceTypes/#/instanceTypeByRegion)，查看本实例的可购情况。
-   For more information about these specifications, see [EN-US\_TP\_9548.md\#section\_e9r\_xkf\_z15](reseller.en-US/Instances/Instance type families.md#section_e9r_xkf_z15)v.

## ebmc4, compute optimized ECS Bare Metal Instance family {#section_8xi_1ce_45q .section}

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

-   您可以前往[ECS实例可购买地域](https://ecs-buy4service.aliyun.com/instanceTypes/#/instanceTypeByRegion)，查看本实例的可购情况。
-   For more information about these specifications, see [EN-US\_TP\_9548.md\#section\_e9r\_xkf\_z15](reseller.en-US/Instances/Instance type families.md#section_e9r_xkf_z15).

## ebmg5, general purpose ECS Bare Metal Instance family {#section_nii_o5k_4t2 .section}

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

-   您可以前往[ECS实例可购买地域](https://ecs-buy4service.aliyun.com/instanceTypes/#/instanceTypeByRegion)，查看本实例的可购情况。
-   For more information about these specifications, see [EN-US\_TP\_9548.md\#section\_e9r\_xkf\_z15](reseller.en-US/Instances/Instance type families.md#section_e9r_xkf_z15).

## Billing methods {#section_wfq_x55_ydb .section}

ECS Bare Metal Instances support pay-as-you-go and subscription billing methods. For more information, see [Billing method comparison](../../../../reseller.en-US/Pricing/Billing method comparison.md#).

