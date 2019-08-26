# General-purpose instance type families {#concept_kmv_f1z_wgb .concept}

This topic describes the general-purpose instance type families g5 and sn2ne, and lists specific instance types.

## g5, general-purpose type family {#section_mzt_mzd_xgb .section}

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

|Instance type|vCPU|Memory \(GiB\)|Local disks \(GiB\)[ \* ](reseller.en-US/Instances/Instance type families.md#)|Bandwidth \(Gbit/s\)[ \*\* ](reseller.en-US/Instances/Instance type families.md#)|Packet forwarding rate \(Thousand pps\)[ \*\*\* ](reseller.en-US/Instances/Instance type families.md#)|NIC queues[ \*\*\*\* ](reseller.en-US/Instances/Instance type families.md#)|ENIs[ \*\*\*\*\* ](reseller.en-US/Instances/Instance type families.md#)|
|:------------|:---|:-------------|:-------------------------------------------|:----------------------------------------------|:-------------------------------------------------------------------|:----------------------------------------|:------------------------------------|
|ecs.g5.large|2|8.0|N/A|1.0|300|2|2|
|ecs.g5.xlarge|4|16.0|N/A|1.5|500|2|3|
|ecs.g5.2xlarge|8|32.0|N/A|2.5|800|2|4|
|ecs.g5.3xlarge|12|48.0|N/A|4.0|900|4|6|
|ecs.g5.4xlarge|16|64.0|N/A|5.0|1,000|4|8|
|ecs.g5.6xlarge|24|96.0|N/A|7.5|1,500|6|8|
|ecs.g5.8xlarge|32|128.0|N/A|10.0|2,000|8|8|
|ecs.g5.16xlarge|64|256.0|N/A|20.0|4,000|16|8|

See [other instance type families](reseller.en-US/Instances/Instance type families.md#).

## sn2ne, general-purpose type family with enhanced network performance { .section}

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

|Instance type|vCPU|Memory \(GiB\)|Local disks \(GiB\)[ \* ](reseller.en-US/Instances/Instance type families.md#)|Bandwidth \(Gbit/s\)[ \*\* ](reseller.en-US/Instances/Instance type families.md#)|Packet forwarding rate \(Thousand pps\)[ \*\*\* ](reseller.en-US/Instances/Instance type families.md#)|NIC queues[ \*\*\*\* ](reseller.en-US/Instances/Instance type families.md#)|ENIs[ \*\*\*\*\* ](reseller.en-US/Instances/Instance type families.md#)|
|:------------|:---|:-------------|:-------------------------------------------|:----------------------------------------------|:-------------------------------------------------------------------|:----------------------------------------|:------------------------------------|
|ecs.sn2ne.large|2|8.0|N/A|1.0|300|2|2|
|ecs.sn2ne.xlarge|4|16.0|N/A|1.5|500|2|3|
|ecs.sn2ne.2xlarge|8|32.0|N/A|2.0|1,000|4|4|
|ecs.sn2ne.3xlarge|12|48.0|N/A|2.5|1,300|4|6|
|ecs.sn2ne.4xlarge|16|64.0|N/A|3.0|1,600|4|8|
|ecs.sn2ne.6xlarge|24|96.0|N/A|4.5|2,000|6|8|
|ecs.sn2ne.8xlarge|32|128.0|N/A|6.0|2,500|8|8|
|ecs.sn2ne.14xlarge|56|224.0|N/A|10.0|4,500|14|8|

See [other instance type families](reseller.en-US/Instances/Instance type families.md#).

