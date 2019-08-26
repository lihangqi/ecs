# Design VPCs {#concept_mnh_443_wdb .concept}

This topic describes how to design Virtual Private Clouds \(VPCs\), determine the number of the VPCs and VSwitches you may require for your services, and how to select private CIDR blocks. VPCs have several advantages because they run in an isolated network environment, and therefore can be useful for a number of applications.

## Determine the number of VPCs {#section_9j3_6ap_4hy .section}

When a VPC is created, it can only be used in one region. Therefore, you may need to create more than one VPC. This is especially the case if you have one or more of the following service requirements:

-   You want to deploy a business system across multiple regions.
-   You want to isolate multiple business systems. For example, you want to isolate a production environment from a test environment.

**Note:** You can run up to 15,000 cloud product instances with one VPC.

## Determine the number of VSwitches {#section_tpz_u99_l15 .section}

-   Lower quantity limit

    The minimum number of VSwitches deployed must be 2. You must deploy at least two VSwitches in different zones to allow for cross-zone disaster tolerance.

-   Network latency

    The network latency between different zones in the same region is low. However, unexpected latency increases may occur due to complicated system calls, system processing, and cross-zone calls. As such, we recommend that you optimize and adapt your business system to strike a balance between high availability and low latency.

-   System isolation

    The number of VSwitches used varies depending on the system capacity and design of the VPC. If your front-end systems can communicate with the Internet, you can deploy each front-end system under a unique VSwitch. By doing so, you can restore an application on an alternate cluster when the primary cluster fails and deploy backend systems under other Vswitches.


## Select private CIDR blocks {#section_0du_hgh_x1q .section}

-   If you use multiple VPCs or want to deploy a hybrid cloud in which your VPCs can communicate with your local Internet data center \(IDC\), we recommend that you use the subnets of standard private CIDR blocks as your VPC CIDR blocks. You may use up to 16 masks.
-   If you use only one VPC that does not communicate with your local IDC, you can select any standard private CIDR block or its subnet as your VPC CIDR block.
-   If you use both a VPC and a classic network and plan to connect the VPC with the ECS instances on the classic network by using ClassicLink, we recommend that you select a CIDR block other than 10.0.0.0/8 as your VPC CIDR block. 10.0.0.0/8 is the CIDR block for the classic network. For more information about ClassicLink, see [ClassicLink overview](../../../../reseller.en-US/User Guide/Network connection/ClassicLink/ClassicLink overview.md#).

The following table lists standard private CIDR blocks and the number of available IP addresses on each block.

**Note:** The IP addresses that are occupied by your business systems are excluded from the IP addresses available on each CIDR block.

|Private CIDR block|Number of available IP addresses|
|:-----------------|:-------------------------------|
|192.168.0.0/16|65532|
|172.16.0.0/12|1048572|
|10.0.0.0/8|16777212|

**Note:** 

-   After a VPC is created, its CIDR blocks cannot be modified.
-   If you require other special CIDR blocks, open a ticket or contact your customer manager.

For more information, see [Plan and design VPC](../../../../reseller.en-US/Best practices/Plan and design VPC.md#) in the *Virtual Private Cloud* documentation.

