# **Entry-level instance type families** {#concept_ycf_pzy_wgb .concept}

This topic describes the entry-level instance type families xn4, n4, mn4, and e4, and lists the specific instance types within each of these instance type families.

## xn4/n4/mn4/e4, type families of previous generations for entry-level users, computing on the x86-architecture {#section_ppq_f32_xgb .section}

**Features**

-   Equipped with 2.5 GHz Intel Xeon E5-2682 v4 \(Broadwell\) processors
-   The latest DDR4 memory
-   No fixed ratio of CPU to memory

|Type family |Features|vCPU to memory ratio |Ideal for|
|:-----------|:-------|:--------------------|:--------|
|xn4|Compact entry-level instances|1:1| -   Front ends of Web applications
-   Light load applications and microservices
-   Applications for development or testing environments

 |
|n4|General entry-level instances |1:2| -   Websites and Web applications
-   Development environment, building servers, code repositories, microservices, and testing and staging environment
-   Lightweight enterprise applications

 |
|mn4|Balanced entry-level instances|1:4| -   Websites and Web applications
-   Lightweight databases and caches
-   Integrated applications and lightweight enterprise services

 |
|e4|Memory entry-level instances |1:8| -   Applications that require large volume of memory
-   Lightweight databases and cache

 |

**xn4**

|Instance type |vCPU|Memory \(GiB\) |Local disks \(GiB\)[\*](reseller.en-US/Instances/Instance type families/Instance type families.md#)|Bandwidth \(Gbit/s\)[\*\*](reseller.en-US/Instances/Instance type families/Instance type families.md#) |Packet forwarding rate \(Thousand pps\)[\*\*\*](reseller.en-US/Instances/Instance type families/Instance type families.md#)|NIC queues[\*\*\*\*](reseller.en-US/Instances/Instance type families/Instance type families.md#)|ENIs[\*\*\*\*\*](reseller.en-US/Instances/Instance type families/Instance type families.md#)|
|:-------------|:---|:--------------|:-----------------------------------------|:---------------------------------------------|:-----------------------------------------------------------------|:--------------------------------------|:----------------------------------|
|ecs.xn4.small|1|1.0|N/A|0.5|50|1|1|

**n4**

|Instance type |vCPU|Memory \(GiB\) |Local disks \(GiB\)[\*](reseller.en-US/Instances/Instance type families/Instance type families.md#)|Bandwidth \(Gbit/s\)[\*\*](reseller.en-US/Instances/Instance type families/Instance type families.md#) |Packet forwarding rate \(Thousand pps\)[\*\*\*](reseller.en-US/Instances/Instance type families/Instance type families.md#)|NIC queues[\*\*\*\*](reseller.en-US/Instances/Instance type families/Instance type families.md#)|ENIs[\*\*\*\*\*](reseller.en-US/Instances/Instance type families/Instance type families.md#)|
|:-------------|:---|:--------------|:-----------------------------------------|:---------------------------------------------|:-----------------------------------------------------------------|:--------------------------------------|:----------------------------------|
|ecs.n4.small|1|2.0|N/A|0.5|50|1|1|
|ecs.n4.large|2|4.0|N/A|0.5|100|1|1|
|ecs.n4.xlarge|4|8.0|N/A|0.8|150|1|2|
|ecs.n4.2xlarge|8|16.0|N/A|1.2|300|1|2|
|ecs.n4.4xlarge|16|32.0|N/A|2.5|400|1|2|
|ecs.n4.8xlarge|32|64.0|N/A|5.0|500|1|2|

**mn4**

|Instance type |vCPU|Memory \(GiB\) |Local disks \(GiB\)[\*](reseller.en-US/Instances/Instance type families/Instance type families.md#)|Bandwidth \(Gbit/s\)[\*\*](reseller.en-US/Instances/Instance type families/Instance type families.md#) |Packet forwarding rate \(Thousand pps\)[\*\*\*](reseller.en-US/Instances/Instance type families/Instance type families.md#)|NIC queues[\*\*\*\*](reseller.en-US/Instances/Instance type families/Instance type families.md#)|ENIs[\*\*\*\*\*](reseller.en-US/Instances/Instance type families/Instance type families.md#)|
|:-------------|:---|:--------------|:-----------------------------------------|:---------------------------------------------|:-----------------------------------------------------------------|:--------------------------------------|:----------------------------------|
|ecs.mn4.small|1|4.0|N/A|0.5|50|1|1|
|ecs.mn4.large|2|8.0|N/A|0.5|100|1|1|
|ecs.mn4.xlarge|4|16.0|N/A|0.8|150|1|2|
|ecs.mn4.2xlarge|8|32.0|N/A|1.2|300|1|2|
|ecs.mn4.4xlarge|16|64.0|N/A|2.5|400|1|2|
|ecs.mn4.8xlarge|32|128.0|N/A|5|500|2|8|

**e4**

|Instance type |vCPU|Memory \(GiB\) |Local disks \(GiB\)[\*](reseller.en-US/Instances/Instance type families/Instance type families.md#)|Bandwidth \(Gbit/s\)[\*\*](reseller.en-US/Instances/Instance type families/Instance type families.md#) |Packet forwarding rate \(Thousand pps\)[\*\*\*](reseller.en-US/Instances/Instance type families/Instance type families.md#)|NIC queues[\*\*\*\*](reseller.en-US/Instances/Instance type families/Instance type families.md#)|ENIs[\*\*\*\*\*](reseller.en-US/Instances/Instance type families/Instance type families.md#)|
|:-------------|:---|:--------------|:-----------------------------------------|:---------------------------------------------|:-----------------------------------------------------------------|:--------------------------------------|:----------------------------------|
|ecs.e4.small|1|8.0|N/A|0.5|50|1|1|
|ecs.ce4.xlarge|2|16.0|N/A|0.5|100|1|1|
|ecs.ce4.xlarge|4|32.0|N/A|0.8|150|1|2|
|ecs.e4.2xlarge|8|64.0|N/A|1.2|300|1|3|
|ecs.ce4.xlarge|16|128.0|N/A|2.5|400|1|8|

See [other instance type families](reseller.en-US/Instances/Instance type families/Instance type families.md#).

\* Cache disks, or Local disks, are the disks located on the physical servers \(host machines\) that ECS instances are hosted on. They provide temporary block level storage for instances. Block storage capacity is measured in binary units. In some cases, such as when the computing resources of an instance, including CPU and memory, are released, or an instance is inactive while migration occurs, data on the local disks is erased. For more information, see [EN-US\_TP\_9561.md\#](reseller.en-US/Block storage/Local disks.md#).

\*\* The maximum bandwidth of inbound and outbound traffic.

\*\*\* The maximum packet forwarding rate of inbound and outbound traffic. For more information about packet forwarding rate testing, see [Test network performance](https://partners-intl.aliyun.com/help/faq-detail/55757.htm).

\*\*\*\* The maximum number of NIC queues that an instance type supports. If your instance is running CentOS 7.3, the maximum number of NIC queues is used by default.

\*\*\*\*\* An enterprise-level instance with two or more vCPU cores supports elastic network interfaces. An entry-level instance with four or more vCPU cores supports elastic network interfaces. For more information about elastic network interfaces, see [EN-US\_TP\_9568.md\#](reseller.en-US/Network/Elastic Network Interfaces/Elastic network interfaces.md#).

