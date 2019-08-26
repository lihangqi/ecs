# Compute optimized and GPU-equipped instance type families {#concept_fgq_sdz_wgb .concept}

This topic describes specific compute optimized instance type families with GPUs, and lists the specific instance types within each of the instance type families. Specifically, the instance type families to be described are as follows: vgn5i, gn6i, gn6v, gn5, gn5i, and gn4.

## vgn5i, light-weight compute optimized type family with GPU {#section_dbr_ndk_dhb .section}

**Features**

-   I/O-optimized
-   Supports SSD Cloud Disks and Ultra Disks
-   Use an NVIDIA P4 GPU computation accelerator
-   Contains a virtual GPU \(which is the result of partitioned virtualization\)
    -   Supports the 1/8, 1/4, 1/2, and 1:1 computing capacity of NVIDIA Tesla P4 GPUs
    -   Supports 1, 2, 4, and 8 GiB of video memory
-   Equipped with a vCPU to memory ratio of 1:3
-   Equipped with 2.5 GHz Intel Xeon E5-2682 v4 \(Broadwell\) processors
-   Supports strong network performance through sufficient computing capacity
-   Suitable for the following scenarios:
    -   Real-time online rendering required for cloud gaming and AR/VR applications
    -   AI reasoning \(including deep and machine learning\), used in the elastic deployment of Internet services that use AI reasoning and computing
    -   Educational and modeling experiment environments that use deep learning

**Instance types**

|Instance type|vCPU|Memory \(GiB\)|Local disks \(GiB\)[ \* ](reseller.en-US/Instances/Instance type families.md#)|GPU|GPU memory \(GiB\)|Bandwidth \(Gbit/s\)[ \*\* ](reseller.en-US/Instances/Instance type families.md#)|Packet forwarding rate \(thousand pps\)[ \*\*\* ](reseller.en-US/Instances/Instance type families.md#)|NIC queues[ \*\*\*\* ](reseller.en-US/Instances/Instance type families.md#)|ENIs[ \*\*\*\*\* ](reseller.en-US/Instances/Instance type families.md#)|
|:------------|:---|:-------------|:-------------------------------------------|:--|:-----------------|:----------------------------------------------|:-------------------------------------------------------------------|:----------------------------------------|:------------------------------------|
|ecs.vgn5i-m1.large|2|6|N/A|P4\*1/8|1|1|300|2|2|
|ecs.vgn5i-m2.xlarge|4|12|N/A|P4\*1/4|2|2|500|2|3|
|ecs.vgn5i-m4.2xlarge|8|24|N/A|P4\*1/2|4|3|800|2|4|
|ecs.vgn5i-m8.4xlarge|16|48|N/A|P4\*1|8|5|1,000|4|5|

**Note:** For more information, see [Create a compute optimized instance with GPUs](reseller.en-US/Instances/Instance type families/Compute optimized type family with GPU/Create a compute optimized instance with GPU.md#).

See [other instance type families](reseller.en-US/Instances/Instance type families.md#).

## gn6i, compute optimized type family with GPUs {#section_zr2_vkl_jhb .section}

**Features**

-   I/O-optimized
-   Supports IPv6
-   Equipped with a vCPU to memory ratio of 1:4
-   Equipped with 2.5 GHz Intel Xeon Platinum 8163 \(Skylake\) processors
-   Supports ESSD Cloud Disks \(million-level IOPS\), SSD Cloud Disks, and Ultra Disks
-   Achieves better performance with the X-Dragon new-generation compute architecture
-   Uses NVIDIA T4 GPU processors:
    -   Based on the new NVIDIA Turing architecture
    -   Up to 320 Turing Tensor Cores
    -   Up to 2,560 CUDA Cores
    -   Mixed-precision Tensor Cores support 65 TFlops FP16, 130 INT8 TOPS, and 260 INT4 TOPS
    -   16 GB memory capacity \(320 GB/s bandwidth\)
-   Supports strong network performance through sufficient computing capacity
-   Suitable for the following scenarios:
    -   AI \(deep learning and machine learning\) inference, computer vision, voice recognition, voice synthesization, natural language processing, machine translation, and reference systems
    -   Real-time online rendering required for cloud gaming and AR/VR applications
    -   Heavy-load graphic computing or graphic workstations
    -   GPU-accelerated databases
    -   High-performance computing

**Instance types**

|Instance types|vCPU|Memory \(GiB\)|Local disks \(GiB\)[ \* ](reseller.en-US/Instances/Instance type families.md#)|GPU|GPU memory \(GiB\)|Bandwidth \(Gbit/s\)[ \*\* ](reseller.en-US/Instances/Instance type families.md#)|Packet forwarding rate \(Thousand pps\)[ \*\*\* ](reseller.en-US/Instances/Instance type families.md#)|IPv6-ready?|NIC queues[ \*\*\*\* ](reseller.en-US/Instances/Instance type families.md#)|ENIs[ \*\*\*\*\* ](reseller.en-US/Instances/Instance type families.md#)|
|:-------------|:---|:-------------|:-------------------------------------------|:--|:-----------------|-----------------------------------------------|:-------------------------------------------------------------------|:----------|:----------------------------------------|:------------------------------------|
|ecs.gn6i-c4g1.xlarge|4|15|N/A|T4\*1|16|4|500|Yes|2|2|
|ecs.gn6i-c8g1.2xlarge|8|31|N/A|T4\*1|16|5|800|Yes|2|2|
|ecs.gn6i-c16g1.4xlarge|16|62|N/A|T4\*1|16|6|1,000|Yes|4|3|
|ecs.gn6i-c24g1.6xlarge|24|93|N/A|T4\*1|16|7.5|1,200|Yes|6|4|
|ecs.gn6i-c24g1.12xlarge|48|186|N/A|T4\*2|32|15|2,400|Yes|12|6|
|ecs.gn6i-c24g1.24xlarge|96|372|N/A|T4\*4|64|30|4,800|Yes|24|8|
|ecs.gn6i-c32g1.8xlarge|32|124|N/A|T4\*1|16|10|1,600|Yes|8|6|
|ecs.gn6i-c48g1.12xlarge|48|186|N/A|T4\*1|16|12|2,400|Yes|12|6|
|ecs.gn6i-c72g1.18xlarge|72|279|N/A|T4\*1|16|21.5|3,600|Yes|18|8|

**Note:** For more information, see [Create a compute optimized instance with GPUs](../../../../dita-oss-bucket/SP_2/DNA0011894323/reseller.en-US/Instances/Instance type families/Compute optimized type family with GPU/Create a compute optimized instance with GPU.md#).

See [other instance type families](reseller.en-US/Instances/Instance type families.md#).

## gn6v, compute optimized type family with GPUs {#section_mgy_332_xgb .section}

**Features**

-   I/O-optimized
-   Supports SSD Cloud Disks and Ultra Disks
-   Uses NVIDIA V100 GPU processors
-   Equipped with a vCPU to memory ratio of 1:4
-   Equipped with 2.5 GHz Intel Xeon Platinum 8163 \(Skylake\) processors
-   Supports strong network performance through sufficient computing capacity
-   Suitable for the following scenarios:
    -   Deep learning, autonomous vehicles, voice recognition, and other AI applications
    -   Scientific computing, computational finance, genomics, and environmental analysis

**Instance types**

|Instance types|vCPU|Memory \(GiB\)|Local disks \(GiB\)[ \* ](reseller.en-US/Instances/Instance type families.md#)|GPU|GPU memory \(GiB\)|Bandwidth \(Gbit/s\)[ \*\* ](reseller.en-US/Instances/Instance type families.md#)|Packet forwarding rate \(Thousand pps\)[ \*\*\* ](reseller.en-US/Instances/Instance type families.md#)|NIC queues[ \*\*\*\* ](reseller.en-US/Instances/Instance type families.md#)|ENIs[ \*\*\*\*\* ](reseller.en-US/Instances/Instance type families.md#)|
|:-------------|:---|:-------------|:-------------------------------------------|:--|:-----------------|:----------------------------------------------|:-------------------------------------------------------------------|:----------------------------------------|:------------------------------------|
|ecs.gn6v-c8g1.2xlarge|8|32.0|N/A|1 \* NVIDIA V100|1 \* 16|2.5|800|4|4|
|ecs.gn6v-c8g1.8xlarge|32|128.0|N/A|4 \* NVIDIA V100|4 \* 16|10.0|2,000|8|8|
|ecs.gn6v-c8g1.16xlarge|64|256.0|N/A|8 \* NVIDIA V100|8 \* 16|20.0|2,500|16|8|

**Note:** For more information, see [Create a compute optimized instance with GPUs](../../../../dita-oss-bucket/SP_2/DNA0011894323/reseller.en-US/Instances/Instance type families/Compute optimized type family with GPU/Create a compute optimized instance with GPU.md#).

See [other instance type families](reseller.en-US/Instances/Instance type families.md#).

## gn5, compute optimized type family with GPU {#section_qtz_j32_xgb .section}

**Features**

-   I/O-optimized
-   Supports SSD Cloud Disks and Ultra Disks
-   Uses NVIDIA P100 GPU processors
-   No fixed ratio of vCPU to memory
-   High-performance local NVMe SSD disks
-   Equipped with 2.5 GHz Intel Xeon E5-2682 v4 \(Broadwell\) processors
-   Supports strong network performance through sufficient computing capacity
-   Suitable for the following scenarios:
    -   Deep learning
    -   Scientific computing, such as computational fluid dynamics, computational finance, genomics, and environmental analysis
    -   High-performance computing, rendering, multi-media coding and decoding, and other server-side GPU compute workloads

**Instance types**

|Instance type|vCPU|Memory \(GiB\)|Local disks \(GiB\)[ \* ](reseller.en-US/Instances/Instance type families.md#)|GPU|GPU memory \(GiB\)|Bandwidth \(Gbit/s\)[ \*\* ](reseller.en-US/Instances/Instance type families.md#)|Packet forwarding rate \(Thousand pps\)[ \*\*\* ](reseller.en-US/Instances/Instance type families.md#)|NIC queues[ \*\*\*\* ](reseller.en-US/Instances/Instance type families.md#)|ENIs[ \*\*\*\*\* ](reseller.en-US/Instances/Instance type families.md#)|
|:------------|:---|:-------------|:-------------------------------------------|:--|:-----------------|:----------------------------------------------|:-------------------------------------------------------------------|:----------------------------------------|:------------------------------------|
|ecs.gn5-c4g1.xlarge|4|30.0|440|1 \* NVIDIA P100|1 \* 16|3.0|300|1|3|
|ecs.gn5-c8g1.2xlarge|8|60.0|440|1 \* NVIDIA P100|1 \* 16|3.0|400|1|4|
|ecs.gn5-c4g1.2xlarge|8|60.0|880|2 \* NVIDIA P100|2 \* 16|5.0|1,000|2|4|
|ecs.gn5-c8g1.4xlarge|16|120.0|880|2 \* NVIDIA P100|2 \* 16|5.0|1,000|4|8|
|ecs.gn5-c28g1.7xlarge|28|112.0|440|1 \* NVIDIA P100|1 \* 16|5.0|1,000|8|8|
|ecs.gn5-c8g1.8xlarge|32|240.0|1760|4 \* NVIDIA P100|4 \* 16|10.0|2,000|8|8|
|ecs.gn5-c28g1.14xlarge|56|224.0|880|2 \* NVIDIA P100|2 \* 16|10.0|2,000|14|8|
|ecs.gn5-c8g1.14xlarge|54|480.0|3520|8 \* NVIDIA P100|8 \* 16|25.0|4,000|14|8|

**Note:** For more information, see [Create a compute optimized instance with GPUs](../../../../dita-oss-bucket/SP_2/DNA0011894323/reseller.en-US/Instances/Instance type families/Compute optimized type family with GPU/Create a compute optimized instance with GPU.md#).

See [other instance type families](reseller.en-US/Instances/Instance type families.md#).

## gn5i, compute optimized type family with GPU {#section_u3b_l32_xgb .section}

**Features**

-   I/O-optimized
-   Supports SSD Cloud Disks and Ultra Disks
-   Uses NVIDIA P4 GPU processors
-   Equipped with a vCPU to memory ratio of 1:4
-   Equipped with 2.5 GHz Intel Xeon E5-2682 v4 \(Broadwell\) processors
-   Supports strong network performance through sufficient computing capacity
-   Suitable for the following scenarios:
    -   Deep learning
    -   Multi-media coding and decoding, and other server-side GPU compute workloads

**Instance types**

|Instance type|vCPU|Memory \(GiB\)|Local disks \(GiB\)[ \* ](reseller.en-US/Instances/Instance type families.md#)|GPU|GPU memory \(GiB\)|Bandwidth \(Gbit/s\)[ \*\* ](reseller.en-US/Instances/Instance type families.md#)|Packet forwarding rate \(Thousand pps\)[ \*\*\* ](reseller.en-US/Instances/Instance type families.md#)|NIC queues[ \*\*\*\* ](reseller.en-US/Instances/Instance type families.md#)|ENIs[ \*\*\*\*\* ](reseller.en-US/Instances/Instance type families.md#)|
|:------------|:---|:-------------|:-------------------------------------------|:--|:-----------------|:----------------------------------------------|:-------------------------------------------------------------------|:----------------------------------------|:------------------------------------|
|ecs.gn5i-c2g1.large|2|8.0|N/A|1 \* NVIDIA P4|1 \* 8|1.0|100|2|2|
|ecs.gn5i-c4g1.xlarge|4|16.0|N/A|1 \* NVIDIA P4|1 \* 8|1.5|200|2|3|
|ecs.gn5i-c8g1.2xlarge|8|32.0|N/A|1 \* NVIDIA P4|1 \* 8|2.0|400|4|4|
|ecs.gn5i-c16g1.4xlarge|16|64.0|N/A|1 \* NVIDIA P4|1 \* 8|3.0|800|4|8|
|ecs.gn5i-c16g1.8xlarge|32|128.0|N/A|2 \* NVIDIA P4|2 \* 8|6.0|1,200|8|8|
|ecs.gn5i-c28g1.14xlarge|56|224.0|N/A|2 \* NVIDIA P4|2 \* 8|10.0|2,000|14|8|

**Note:** For more information, see [Create a compute optimized instance with GPUs](../../../../dita-oss-bucket/SP_2/DNA0011894323/reseller.en-US/Instances/Instance type families/Compute optimized type family with GPU/Create a compute optimized instance with GPU.md#).

See [other instance type families](reseller.en-US/Instances/Instance type families.md#).

## gn4, compute optimized type family with GPU {#section_cts_l32_xgb .section}

**Features**

-   I/O-optimized
-   Supports SSD Cloud Disks and Ultra Disks
-   Uses NVIDIA M40 GPU processors
-   No fixed ratio of CPU to memory
-   Equipped with 2.5 GHz Intel Xeon E5-2682 v4 \(Broadwell\) processors
-   Supports strong network performance through sufficient computing capacity
-   Suitable for the following scenarios:
    -   Deep learning
    -   Scientific computing, such as computational fluid dynamics, computational finance, genomics, and environmental analysis
    -   High-performance computing, rendering, multi-media coding and decoding, and other server-side GPU compute workloads

**Instance types**

|Instance type|vCPU|Memory \(GiB\)|Local disks \(GiB\)[ \* ](reseller.en-US/Instances/Instance type families.md#)|GPU|GPU memory \(GiB\)|Bandwidth \(Gbit/s\)[ \*\* ](reseller.en-US/Instances/Instance type families.md#)|Packet forwarding rate \(Thousand pps\)[ \*\*\* ](reseller.en-US/Instances/Instance type families.md#)|NIC queues[ \*\*\*\* ](reseller.en-US/Instances/Instance type families.md#)|ENIs[ \*\*\*\*\* ](reseller.en-US/Instances/Instance type families.md#)|
|:------------|:---|:-------------|:-------------------------------------------|:--|:-----------------|:----------------------------------------------|:-------------------------------------------------------------------|:----------------------------------------|:------------------------------------|
|ecs.gn4-c4g1.xlarge|4|30.0|N/A|1 \* NVIDIA M40|1 \* 12|3.0|300|1|3|
|ecs.gn4-c8g1.2xlarge|8|30.0|N/A|1 \* NVIDIA M40|1 \* 12|3.0|400|1|4|
|ecs.gn4.8xlarge|32|48.0|N/A|1 \* NVIDIA M40|1 \* 12|6.0|800|3|8|
|ecs.gn4-c4g1.2xlarge|8|60.0|N/A|2 \* NVIDIA M40|2 \* 12|5.0|500|1|4|
|ecs.gn4-c8g1.4xlarge|16|60.0|N/A|2 \* NVIDIA M40|2 \* 12|5.0|500|1|8|
|ecs.gn4.14xlarge|56|96.0|N/A|2 \* NVIDIA M40|2 \* 12|10.0|1,200|4|8|

**Note:** For more information, see [Create a compute optimized instance with GPUs](../../../../dita-oss-bucket/SP_2/DNA0011894323/reseller.en-US/Instances/Instance type families/Compute optimized type family with GPU/Create a compute optimized instance with GPU.md#).

See [other instance type families](reseller.en-US/Instances/Instance type families.md#).

