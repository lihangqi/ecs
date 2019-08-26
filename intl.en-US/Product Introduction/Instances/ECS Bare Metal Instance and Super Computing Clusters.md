# ECS Bare Metal Instance and Super Computing Clusters {#concept_lnh_hv2_5db .concept}

ECS Bare Metal \(EBM\) Instance is a new type of computing product that features the elasticity of virtual machines and the performance and characteristics of physical machines. As a product completely and independently developed by Alibaba Cloud, EBM Instance is based on the next-generation of virtualization technology. Compared with the previous generation, not only is the common virtual cloud server supported, but also is nested virtualization. The resource elasticity of common cloud servers is retained, while nested virtualization technology creates a user experience comparable to physical machines.

Super Computing Clusters \(SCCs\) are based on EBM Instances. With the help of the high-speed interconnectivity of RDMA \(Remote Direct Memory Access\) technology, SCCs greatly enhance network performance and increase the acceleration ratio of large-scale clusters. SCCs have all the advantages of EBM Instances and offer high-quality network performance featuring high bandwidth and low latency.

## Advantages {#section_onk_y55_ydb .section}

**EBM Instances**

EBM Instances create value for customers through technological innovation. EBM Instances have the following advantages:

-   **Exclusive computing resources**

    As a cloud-based elastic computing product, the EBM Instances exceed the performance and isolation of contemporary physical machines and enable exclusive computing resources without virtualization performance overheads and feature loss. EBM Instances support 8, 32, and 96 CPU cores and ultrahigh frequency. An EBM Instance with 8 cores, for example, supports an ultrahigh frequency of up to 3.7 to 4.1 GHz, providing better performance and responsiveness for gaming and financial industries than similar products.

-   **Encrypted compute**

    For security, the EBM Instances use a chip-level trusted execution environment \(Intel® SGX\) in addition to physical server isolation. This allows the instances to compute only the encrypted data in a safe and trusted environment, and provides improved security for the customer data on the cloud. This chip-level hardware security protection provides a safe box for the data of cloud users and allows users to control all the data encryption and key protection procedures. For more information, see [Intel SGX](https://partners-intl.aliyun.com/help/faq-detail/89858.htm).

-   **Any Stack on Alibaba Cloud**

    EBM Instances combine the performance strengths and features of physical machines and [the ease-of-use and cost-effectiveness of cloud servers](reseller.en-US/Product Introduction/Benefits of ECS.md#). They can effectively meet your demands for high-performance computing and help you build new hybrid clouds. Due to their flexibility, elasticity, and other strengths, EBM Instances allow you to deploy any stack on them, such as Xen, KVM, and VMWare. As a result, offline private clouds can be seamlessly migrated to Alibaba Cloud without the performance overhead issues that may arise because of nested virtualization. This facilitates a new approach for you to move businesses onto the cloud.

-   **Heterogeneous instruction set processor support**

    The virtualization 2.0 technology used by EBM Instances is independently developed by Alibaba Cloud. It can zero-cost support ARM and other instruction set processors.


**SCC**

SCCs are based on EBM Instance, and were released by Alibaba Cloud to meet the demands of applications such as high performance computing, artificial intelligence, machine learning, scientific or engineering computing, data analysis, and audio and video processing. In the clusters, nodes are connected by Remote Direct Memory Access \(RDMA\) networks featuring high bandwidth and low latency, guaranteeing the highly parallel efficiency demanded by applications that require high-performance computing. Meanwhile, the RoCE \(RDMA over Convergent Ethernet\) rivals an Infiniband network in terms of connection speed, and supports more extensive Ethernet-based applications. The combination of SCCs built on EBM Instance and other Alibaba Cloud computing products such as ECS and GPU servers provides the Alibaba Cloud elastic high-performance computing \(E-HPC\) platform with ultimate high performance parallel computing resources, making supercomputing on the cloud a reality.

## Features {#section_efq_x55_ydb .section}

EBM Instances and SCC have the following features:

-   CPU specifications:

    -   EBM Instances: Supports 8 cores, 32 cores, and 96 cores, and supports high clock speed.
    -   SCC: Supports 64 cores and 96 cores, and provides support for high clock speed.
-   Memory specifications:

    -   EBM Instances: Supports 32 GiB to 768 GiB memory. For better computing performance, the ratio of CPU to memory is 1:2 or 1:4.
    -   SCC: The ratio of CPU to memory is 1:3 or 1:4.
-   Storage specifications: Supports starting from the virtual machine image and cloud disk to deliver instances in minutes.

-   Network configurations:

    -   Supports Virtual Private Cloud \(VPC\) networks, maintaining interoperability with ECS, GPU cloud servers, and other cloud products. Delivers performance and stability comparable to physical machine networks.
    -   \(Only for SCC\) Supports RDMA communication through high-speed RoCE networks.
-   Images: Supports images of Alibaba Cloud ECS.

-   Security settings: Maintains the same security policies and flexibility as existing cloud server ECS instances.


The following table compares EBM Instance or SCC, physical servers, and virtual servers.

|Feature type|Features|EBM Instances/SCC|Physical servers|Virtual servers|
|:-----------|:-------|:----------------|:---------------|:--------------|
|Automated O&M|Delivery in minutes|Y|N|Y|
|Computing|Zero performance loss|Y|Y|N|
|Zero feature loss|Y|Y|N|
|Zero resource competition|Y|Y|N|
|Storage|Fully compatible with ECS cloud disks|Y|N|Y|
|Start from cloud disks \(system disks\)|Y|N|Y|
|System disk can be quickly reset|Y|N|Y|
|Uses ECS images|Y|N|Y|
|Supports cold migration between physical and virtual servers|Y|N|Y|
|Requires no installation of operating system|Y|N|Y|
|Discards local RAID, and provides stronger protection of data on cloud disks|Y|N|Y|
|Network|Fully compatible with the ECS VPC networks|Y|N|Y|
|Fully compatible with the ECS classic networks|Y|N|Y|
|Free of bottlenecks for communications between physical and virtual server clusters in the VPC|Y|N|Y|
|Management|Fully compatible with the existing ECS management system|Y|N|Y|
|Consistent user experience on VNC and other features with that of virtual servers|Y|N|Y|
|Guaranteed OOB network security|Y|N|N/A|

## Instance type families {#section_ufq_x55_ydb .section}

The type families of EBM Instances include:

-   ebmg5, general purpose EBM Instance type family
-   ebmhfg5, high frequency EBM Instance type family
-   ebmc4, compute EBM Instance type family

The type families of SCC include:

-   scch5, Super Computing Cluster \(SCC\) instance type family with high clock speed
-   sccg5, geneneral-purpose Super Computing Cluster \(SCC\) instance type family

For more information, see [EBM Instance type families](reseller.en-US/Product Introduction/Instance type families.md#ebmg5) and [SCC Instance type families](reseller.en-US/Product Introduction/Instance type families.md#sccg5).

## Billing methods {#section_wfq_x55_ydb .section}

EBM Instances and SCC instances support Subscription and Pay-As-You-Go. For more information about billing methods, see [Billing method comparison](../../../../../reseller.en-US/Pricing/Billing method comparison.md#).

## Related operations {#section_xfq_x55_ydb .section}

You can [create an EBM instance](../../../../../reseller.en-US/User Guide/Instances/Create an instance/Create an EBM instance.md#) or [create an SCC server instance](../../../../../reseller.en-US/User Guide/Instances/Create an instance/Create an SCC server instance.md#) in the console.

For more information, see [FAQs about EBM Instances](https://partners-intl.aliyun.com/help/faq-detail/66558.htm) and [SCC FAQ](https://partners-intl.aliyun.com/help/faq-detail/89878.htm).

