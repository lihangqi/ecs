# Compute-intensive instance type families {#concept_w3g_z1z_wgb .concept}

This topic describes specific compute instance type families, and lists the specific instance types within each of the instance type families. Specifically, the instance type families to be described are: compute-intensive instance type family ic5, compute-optimized instance type family with enhanced network performance sn1ne, and compute instance type family c5.

## ic5, intensive compute instance type family {#section_ij5_rzd_xgb .section}

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

|Instance type |Vcpu|Memory \(GiB\) |Local disks \(GiB\)[\*](reseller.en-US/Instances/Instance type families/Instance type families.md#)|Bandwidth \(Gbit/s\)[\*\*](reseller.en-US/Instances/Instance type families/Instance type families.md#) |Packet forwarding rate \(Thousand pps\)[\*\*\*](reseller.en-US/Instances/Instance type families/Instance type families.md#)|NIC queues[\*\*\*\*](reseller.en-US/Instances/Instance type families/Instance type families.md#)|ENIs[\*\*\*\*\*](reseller.en-US/Instances/Instance type families/Instance type families.md#)|
|:-------------|:---|:--------------|:-----------------------------------------|:---------------------------------------------|:-----------------------------------------------------------------|:--------------------------------------|:----------------------------------|
|ecs.ic5.large|2|2.0|N/A|1.0|300|2|2|
|ecs.ic5.xlarge|4|4.0|N/A|1.5|500|2|3|
|ecs.ic5.2xlarge|8|8.0|N/A|2.5|800|2|4|
|ecs.ic5.3xlarge|12|12.0|N/A|4.0|900|4|6|
|ecs.ic5.4xlarge|16|16.0|N/A|5.0|1,000|4|8|

See [other instance type families](reseller.en-US/Instances/Instance type families/Instance type families.md#).

## c5, compute instance type family {#section_m25_szd_xgb .section}

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

|Instance type |vCPU|Memory \(GiB\) |Local disks \(GiB\)[\*](reseller.en-US/Instances/Instance type families/Instance type families.md#)|Bandwidth \(Gbit/s\)[\*\*](reseller.en-US/Instances/Instance type families/Instance type families.md#)|Packet forwarding rate \(Thousand pps\)[\*\*\*](reseller.en-US/Instances/Instance type families/Instance type families.md#)|NIC queues[\*\*\*\*](reseller.en-US/Instances/Instance type families/Instance type families.md#)|ENIs[\*\*\*\*\*](reseller.en-US/Instances/Instance type families/Instance type families.md#)|
|:-------------|:---|:--------------|:-----------------------------------------|:--------------------------------------------|:-----------------------------------------------------------------|:--------------------------------------|:----------------------------------|
|ecs.c5.large|2|4.0|N/A|1.0|300|2|2|
|ecs.c5.xlarge|4|8.0|N/A|1.5|500|2|3|
|ecs.c5.2xlarge|8|16.0|N/A|2.5|800|2|4|
|ecs.c5.3xlarge|12|24.0|N/A|4.0|900|4|6|
|ecs.c5.4xlarge|16|32.0|N/A|5.0|1,000|4|8|
|ecs.c5.6xlarge|24|48.0|N/A|7.5|1,500|6|8|
|ecs.c5.8xlarge|32|64.0|N/A|10.0|2,000|8|8|
|ecs.c5.16xlarge|64|128.0|N/A|20.0|4,000|16|8|

See [other instance type families](reseller.en-US/Instances/Instance type families/Instance type families.md#).

## sn1ne, compute optimized type family with enhanced network performance {#section_hjs_tzd_xgb .section}

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

|Instance type |vCPU|Memory \(GiB\) |Local disks \(GiB\)[\*](reseller.en-US/Instances/Instance type families/Instance type families.md#)|Bandwidth \(Gbit/s\)[\*\*](reseller.en-US/Instances/Instance type families/Instance type families.md#) |Packet forwarding rate \(Thousand pps\)[\*\*\*](reseller.en-US/Instances/Instance type families/Instance type families.md#)|NIC queues[\*\*\*\*](reseller.en-US/Instances/Instance type families/Instance type families.md#)|ENIs[\*\*\*\*\*](reseller.en-US/Instances/Instance type families/Instance type families.md#)|
|:-------------|:---|:--------------|:-----------------------------------------|:---------------------------------------------|:-----------------------------------------------------------------|:--------------------------------------|:----------------------------------|
|ecs.sn1ne.large|2|4.0|N/A|1.0|300|2|2|
|ecs.sn1ne.xlarge|4|8.0|N/A|1.5|500|2|3|
|ecs.sn1ne.2xlarge|8|16.0|N/A|2.0|1,000|4|4|
|ecs.sn1ne.3xlarge|12|24.0|N/A|2.5|1,300|4|6|
|ecs.sn1ne.4xlarge|16|32.0|N/A|3.0|1,600|4|8|
|ecs.sn1ne.6xlarge|24|48.0|N/A|4.5|2,000|6|8|
|ecs.sn1ne.8xlarge|32|64.0|N/A|6.0|2,500|8|8|

See [other instance type families](reseller.en-US/Instances/Instance type families/Instance type families.md#).

