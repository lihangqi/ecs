# Attach an ENI {#concept_twf_4jj_zdb .concept}

This topic describes how to attach an Elastic Network Interface \(ENI\). Specifically, you either attach an ENI when you create an ECS instance, or you can alternatively create an ENI separately and then attach it to an ECS instance. Attaching an ENI allows you to build clusters with higher availability, perform failovers with lower costs, and manage your network with finer granularity.

## Attach an ENI when you create an ECS instance {#section_zwv_4ps_lgb .section}

**Limits**

If you attach a secondary ENI, as opposed to a primary ENI, to an ECS instance and do not detach it from the ECS instance, the secondary ENI will be released when you release the ECS instance. For more information, see [Detach an ENI from an instance](reseller.en-US/Network/Elastic Network Interfaces/Detach an ENI from an instance.md).

**Procedure**

Before you begin, make sure that you have created an ECS instance. For the specific procedure, see [Step 2: Create an instance](../../../../../reseller.en-US/Quick Start for Entry-Level Users/Step 2. Create an instance.md#).

When you attach an ENI to an ECS instance during the process of creating an ECS instance, configure the following parameters:

1.  Basic configurations
    -   Region: ENIs are supported in all regions.
    -   Instance type: Select an I/O-optimized instance type that supports ENIs. For more information, see [Instance type families](../../../../../reseller.en-US/Instances/Instance type families/Instance type families.md#).
    -   Image: The following image types support ENIs without any manual configuration required:

        -   CentOS 7.3 64-bit
        -   CentOS 6.8 64-bit
        -   Windows Server 2016 Datacenter Edition 64-bit
        -   Windows Server 2012 R2 Datacenter Edition 64-bit
        **Note:** 

        For other image types, after you create an ECS instance, you must configure the ENI to enable the instance to support ENIs.

2.  Networking
    -   Network: Select **VPC**, and then select a VPC and VSwitch that you created.
    -   ENI: Click **Add ENI** to attach the target ENI. The ENI and the instance must belong to the same VSwitch.

        **Note:** When you create an instance in the ECS console, you can attach up to two ENIs to the instance. One is the primary ENI, and the other is the secondary ENI. You can attach more secondary ENIs to the instance by using one of the following two methods:

        -   [Create an ENI](reseller.en-US/Network/Elastic Network Interfaces/Create an ENI.md) in the ECS console, and then [attach the ENI](reseller.en-US//Attach an ENI to an instance.md) to the instance.
        -   Call the API [AttachNetworkInterface](../../../../../reseller.en-US/API Reference/Elastic network interfaces/AttachNetworkInterface .md) to attach more ENIs to the instance.

## Attach an ENI to an existing ECS instance {#section_bwf_mqs_lgb .section}

**Limits**

-   The ENI can only be attached to the existing ECS instance as a secondary ENI, rather than a primary ENI.
-   The ENI must be in the **Available** state.
-   The ECS instance must be in the **Stopped** or **Running** state.
-   The ENI can only be attached to a VPC ECS instance. The ENI and the instance must be in the same VPC.
-   The VSwitch to which the ENI belongs must be in the same zone as the ECS instance to which the ENI is attached.
-   The ENI can only be attached to an I/O-optimized instance.
-   One ENI can be attached to only one VPC ECS instance, but one instance can be attached with multiple ENIs. For more information, see [Instance type families](../../../../../reseller.en-US/Instances/Instance type families/Instance type families.md).

**Prerequisites**

-   An ENI is created. For more information, see [Create an ENI](reseller.en-US/Network/Elastic Network Interfaces/Create an ENI.md).
-   The ENI is in the **Available** state.
-   The instance can be attached with secondary ENIs and is in the **Stopped** or **Running** state. For more information, see [Instance type families](../../../../../reseller.en-US/Instances/Instance type families/Instance type families.md).

**Procedure**

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, choose **Networks and Security** \> **ENI**.
3.  Select the target region.
4.  Locate an available ENI, and then click **Bind to Instance**.
5.  In the displayed dialog box, select the target instance, and then click **OK**.

Refresh the list. When the ENI is in the **Bound** state, the ENI is attached to the instance.

**Note:** If the last time your instance was started or restarted is earlier than April 1, 2018, then you must use the ECS console or call the API [RebootInstance](../../../../../reseller.en-US/API Reference/Instances/RebootInstance.md#) to [Restart the instance](reseller.en-US/Instances/Manage instances/Restart an instance.md#), as opposed to logging on to the instance to restart it. Otherwise, the ENI cannot be attached to the instance.

## What to do next {#section_gj1_sjk_zdb .section}

After you attach an ENI to an ECS instance, you can perform the following operations:

-   [Detach the ENI from the instance](reseller.en-US/Network/Elastic Network Interfaces/Detach an ENI from an instance.md) or [Delete the ENI](reseller.en-US/Network/Elastic Network Interfaces/Delete an ENI.md).
-   [Configure the ENI](reseller.en-US/Network/Elastic Network Interfaces/Configure an ENI.md) if the image cannot identify the ENI.

