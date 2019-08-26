# High clock speed instance type families {#concept_fv4_jdz_wgb .concept}

This topic describes the compute optimized instance type family with high clock speed hfc5 and the general-purpose instance type family with high clock speed hfg5, and lists the specific instance types within each of these two instance type families.

## hfc5, compute optimized type family with high clock speed {#section_swd_q12_xgb .section}

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

|Instance type |vCPU|Memory \(GiB\) |Local disks \(GiB\)[\*](reseller.en-US/Instances/Instance type families/Instance type families.md#)|Bandwidth \(Gbit/s\)[\*\*](reseller.en-US/Instances/Instance type families/Instance type families.md#) |Packet forwarding rate \(Thousand pps\)[\*\*\*](reseller.en-US/Instances/Instance type families/Instance type families.md#)|NIC queues[\*\*\*\*](reseller.en-US/Instances/Instance type families/Instance type families.md#)|ENIs[\*\*\*\*\*](reseller.en-US/Instances/Instance type families/Instance type families.md#)|
|:-------------|:---|:--------------|:-----------------------------------------|:---------------------------------------------|:-----------------------------------------------------------------|:--------------------------------------|:----------------------------------|
|ecs.hfc5.large|2|4.0|N/A|1.0|300|2|2|
|ecs.hfc5.xlarge|4|8.0|N/A|1.5|500|2|3|
|ecs.hfc5.2xlarge|8|16.0|N/A|2.0|1,000|2|4|
|ecs.hfc5.3xlarge|12|24.0|N/A|2.5|1,300|4|6|
|ecs.hfc5.4xlarge|16|32.0|N/A|3.0|1,600|4|8|
|ecs.hfc5.6xlarge|24|48.0|N/A|4.5|2,000|6|8|
|ecs.hfc5.8xlarge|32|64.0|N/A|6.0|2,500|8|8|

See [other instance type families](reseller.en-US/Instances/Instance type families/Instance type families.md#).

## hfg5, general-purpose type family with high clock speed {#section_nqz_q12_xgb .section}

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

|Instance type |vCPU|Memory \(GiB\) |Local disks \(GiB\)[\*](reseller.en-US/Instances/Instance type families/Instance type families.md#)|Bandwidth \(Gbit/s\)[\*\*](reseller.en-US/Instances/Instance type families/Instance type families.md#) |Packet forwarding rate \(Thousand pps\)[\*\*\*](reseller.en-US/Instances/Instance type families/Instance type families.md#)|NIC queues[\*\*\*\*](reseller.en-US/Instances/Instance type families/Instance type families.md#)|ENIs[\*\*\*\*\*](reseller.en-US/Instances/Instance type families/Instance type families.md#)|
|:-------------|:---|:--------------|:-----------------------------------------|:---------------------------------------------|:-----------------------------------------------------------------|:--------------------------------------|:----------------------------------|
|ecs.hfg5.large|2|8.0|N/A|1.0|300|2|2|
|ecs.hfg5.xlarge|4|16.0|N/A|1.5|500|2|3|
|ecs.hfg5.2xlarge|8|32.0|N/A|2.0|1,000|2|4.|
|ecs.hfg5.3xlarge|12|48.0|N/A|2.5|1,300|4|6|
|ecs.hfg5.4xlarge|16|64.0|N/A|3.0|1,600|4|8|
|ecs.hfg5.6xlarge|24|96.0|N/A|4.5|2,000|6|8|
|ecs.hfg5.8xlarge|32|128.0|N/A|6.0|2,500|8|8|
|ecs.hfg5.14xlarge|56|160.0|N/A|10.0|4,000|14|8|

See [other instance type families](reseller.en-US/Instances/Instance type families/Instance type families.md#).

