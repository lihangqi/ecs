# Plan networks {#concept_mnh_443_wdb .concept}

We recommend Virtual Private Clouds \(VPCs\), which are logically isolated from each other. VPCs have the following characteristics:

-   Isolated network environment
-   Controllable network configurations

## Determine the number of VPCs {#section_ecn_kdj_wdb .section}

-   We recommend that you use multiple VPCs if any of the following requirements is involved:

    -   The system is deployed in multiple regions.

        VPCs are region-specific resources, which cannot be deployed across regions. To deploy a system across regions, you must use multiple VPCs. The [Express Connect](../../../../intl.en-US/Product Introduction/What is Express Connect?.md#) product built on the Alibaba backbone network can easily achieve communication between VPCs across regions or countries.

    -   Multiple business systems are isolated from each other.

        To strictly isolate multiple business systems within the same region by using VPCs, such as strict isolation between the production environment and the test environment, you must use multiple VPCs.

-   Use a single VPC.

    A single VPC is recommended if you do not have to deploy a system in multiple regions or isolate systems from each other by using VPCs. Now, up to 10,000 cloud product instances can run in a single VPC. Such a capacity can meet basic requirements.


## Determine the number of VSwitches {#section_a21_c2j_wdb .section}

We recommend that you use at least two VSwitches even if you use only one VPC. In addition, deploy the two VSwitches in two different zones to achieve cross-zone disaster tolerance.

The network communication latency between different zones in the same region is low, but the time is still needed for business system adaptation and verification. A latency higher than expected may be introduced due to complicated system calls, system processing, and cross-zone calls. We recommend that you optimize and adapt the system to balance between high availability and low latency.

The number of VSwitches used is related to the system size and planning. If the front-end systems can access Internet or can be accessed by Internet, you can deploy different front-end systems under different VSwitches to achieve disaster tolerance, and deploy backend systems under other switches.

## Select network blocks {#section_tjr_c2j_wdb .section}

You can use the standard private CIDR blocks listed in the following table and their subnets as the private IP address ranges of VPCs.

|CIDR blocks|Number of available IP addresses|Remarks|
|:----------|:-------------------------------|:------|
|192.168.0.0/16|65532|Addresses occupied by systems are excluded.|
|172.16.0.0/12|1048572|Addresses occupied by systems are excluded.|
|10.0.0.0/8|16777212|Addresses occupied by systems are excluded.|

**Note:** 

-   After a VPC is created, you cannot modify its CIDR blocks.
-   If you have requirements for other special CIDR blocks, [open a ticket](https://workorder-intl.console.aliyun.com/#/ticket/createIndex) or contact your customer manager to activate the CIDR blocks.
-   If multiple VPCs exist, or you have to build a hybrid cloud composed of VPCs and offline IDCs, we recommend that you use subnets of the preceding standard CIDR blocks and that the netmask length does not exceed 16.
-   If only one VPC is on the cloud and the VPC does not have to communicate with offline IDCs, you can select any of the preceding CIDR blocks or their subnets.
-   You must also consider whether the class network is used. If you are using a classic a classic network on the cloud and plan to connect ECS instances of the classic network to a VPC by using the [ClassicLink](../../../../intl.en-US/User Guide/Network connection/ClassicLink/ClassicLink overview.md#) feature, we recommend that you use a CIDR block other than 10.0.0.0/8 for the VPC, because the CIDR block of a classic network is 10.0.0.0/8.

For more information, see [plan and design VPC](../../../../intl.en-US/Best practices/Plan and design VPC.md#).

