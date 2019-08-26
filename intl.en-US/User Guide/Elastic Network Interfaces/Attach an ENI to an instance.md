# Attach an ENI to an instance {#concept_ax5_pjk_zdb .concept}

You can attach an ENI to an instance.

This topic describes how to attach an ENI to an instance in the ECS console.

## Limits {#section_z31_sjk_zdb .section}

To attach an ENI to an instance, you have the following limits:

-   You can only attach a secondary ENI to an instance.
-   The ENI must be in the **Available** status.
-   The instance must be in the **Stopped** or **Running** status.
-   You can only attach an ENI to a VPC-Connected ECS instance, and they must be in the same VPC.
-   The VSwitches of the ENI and the instance can be different, but they must be in the same zone.
-   An ENI can be attached to an I/O optimized ECS instance only.
-   An ENI can only be attached to one VPC-Connected ECS instance at a time. However, a VPC-Connected ECS instance can be associated with multiple ENIs. For more information about the maximum number of ENIs that can be attached to one instance, see [instance type families](../../../../reseller.en-US/Product Introduction/Instance type families.md).

## Prerequisites {#section_bj1_sjk_zdb .section}

Before you attach an ENI to an instance, finish the following operations:

-   [Create an ENI](reseller.en-US/User Guide/Elastic Network Interfaces/Create an ENI.md).
-   Make sure the ENI is in the **Available** status.
-   Make sure your instance can be associated with secondary ENIs, and the instance is in the **Stopped** or **Running** status. For the number of ENIs that can be attached to each instance type, see the [instance type families](../../../../reseller.en-US/Product Introduction/Instance type families.md).

## Procedure {#section_dj1_sjk_zdb .section}

To attach an ENI to an instance, follow these steps:

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, select **Networks and Security** \> **ENI**.
3.  Select a region.
4.  Find an available ENI, and in the **Actions** column, click **Bind to Instance**.
5.  In the Bind to Instance dialog box, after selecting an instance, click **OK**.

In the Network Interfaces page, refresh the table. When the selected ENI is in the **Bound** status, it is successfully attached to the instance.

## What to do next {#section_gj1_sjk_zdb .section}

After an ENI is attached to an instance, you can:

-   [Detach the ENI from an instance](reseller.en-US/User Guide/Elastic Network Interfaces/Detach an ENI from an instance.md), and then [delete the ENI](reseller.en-US/User Guide/Elastic Network Interfaces/Delete an ENI.md).
-   [Modify attributes of the ENI](reseller.en-US/User Guide/Elastic Network Interfaces/Modify attributes of an ENI.md).
-   [Configure the ENI](reseller.en-US/User Guide/Elastic Network Interfaces/Configure an ENI.md), if the ENI cannot be automatically recognized by the operating system of your instance.

