# Compute optimized and FPGA-equipped instance type families {#concept_ynb_ptz_wgb .concept}

This topic describes the compute optimized instance type families with FPGAs f1 and f3, and lists the specific instance types within each of these two instance type families.

## f1, compute optimized type family with FPGA {#section_ljh_qd2_xgb .section}

**Features**

-   I/O-optimized
-   Supports SSD Cloud Disks and Ultra Disks
-   Intel ARRIA 10 GX 1150 FPGA
-   Equipped with a vCPU to memory ratio of 1:7.5
-   Equipped with 2.5 GHz Intel Xeon E5-2682 v4 \(Broadwell\) processors
-   Supports strong network performance through sufficient computing capacity
-   Suitable for the following scenarios:
    -   Deep learning and reasoning
    -   Genomics research
    -   Financial analysis
    -   Picture transcoding
    -   Computational workloads, such as real-time video processing and security

**Instance types**

|Instance type |vCPU|Memory \(GiB\) |Local disks \(GiB\)[\*](reseller.en-US/Instances/Instance type families/Instance type families.md#)|FPGA|Bandwidth \(Gbit/s\)[\*\*](reseller.en-US/Instances/Instance type families/Instance type families.md#) |Packet forwarding rate \(Thousand pps\)[\*\*\*](reseller.en-US/Instances/Instance type families/Instance type families.md#)|NIC queues[\*\*\*\*](reseller.en-US/Instances/Instance type families/Instance type families.md#)|ENIs[\*\*\*\*\*](reseller.en-US/Instances/Instance type families/Instance type families.md#)|
|:-------------|:---|:--------------|:-----------------------------------------|:---|:---------------------------------------------|:-----------------------------------------------------------------|:--------------------------------------|:----------------------------------|
|ecs.f1-c8f1.2xlarge|8|60.0|N/A|Intel ARRIA 10 GX 1150|3.0|400|4|4|
|ecs.f1-c8f1.4xlarge|16|120.0|N/A|2 \* Intel ARRIA 10 GX 1150|5.0|1,000|4|8|
|ecs.f1-c28f1.7xlarge|28|112.0|N/A|Intel ARRIA 10 GX 1150|5.0|2,000|8|8|
|ecs.f1-c28f1.14xlarge|56|224.0|N/A|2 \* Intel ARRIA 10 GX 1150|10.0|2,000|14|8|

See [other instance type families](reseller.en-US/Instances/Instance type families/Instance type families.md#).

## f3, compute optimized type family with FPGA {#section_j5b_rd2_xgb .section}

**Features**

-   I/O-optimized
-   Supports SSD Cloud Disks and Ultra Disks
-   Xilinx 16nm Virtex UltraScale + VU9P
-   Equipped with a vCPU to memory ratio of 1:4
-   Equipped with 2.5 GHz Intel Xeon Platinum 8163 \(Skylake\) processors
-   Supports strong network performance through sufficient computing capacity
-   Suitable for the following scenarios:
    -   Deep learning and reasoning
    -   Genomics research
    -   Speeding up database access
    -   Picture transcoding, such as converting JPEG to WebP
    -   Real-time video processing, such as H.265 video compression

**Instance types**

|Instance type|vCPU|Memory \(GiB\)|Local disks \(GiB\)[\*](reseller.en-US/Instances/Instance type families/Instance type families.md#)|FPGA|Bandwidth \(Gbit/s\)[\*\*](reseller.en-US/Instances/Instance type families/Instance type families.md#)|Packet forwarding rate \(Thousand pps\)[\*\*\*](reseller.en-US/Instances/Instance type families/Instance type families.md#)|NIC queues[\*\*\*\*](reseller.en-US/Instances/Instance type families/Instance type families.md#)|ENIs[\*\*\*\*\*](reseller.en-US/Instances/Instance type families/Instance type families.md#)|
|:------------|:---|:-------------|:-----------------------------------------|:---|:--------------------------------------------|:-----------------------------------------------------------------|:--------------------------------------|:----------------------------------|
|ecs.f3-c4f1.xlarge|4|16.0|N/A|1 \* Xilinx VU9P|1.5|300|2|3|
|ecs.f3-c8f1.2xlarge|8|32.0|N/A|1 \* Xilinx VU9P|2.5|500|4|4|
|ecs.f3-c16f1.4xlarge|16|64.0|N/A|1 \* Xilinx VU9P|5.0|1,000|4|8|
|ecs.f3-c16f1.8xlarge|32|128.0|N/A|2 \* Xilinx VU9P|10.0|2,000|8|8|
|ecs.f3-c16f1.16xlarge|64|256.0|N/A|4 \* Xilinx VU9P|20.0|2,500|16|8|

See [other instance type families](reseller.en-US/Instances/Instance type families/Instance type families.md#).

