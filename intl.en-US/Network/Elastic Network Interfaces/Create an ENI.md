# Create an ENI {#concept_gjc_4lj_zdb .concept}

This topic describes how to create an elastic network interface \(ENI\) in the ECS console. You can use an ENI to deploy a high-availability cluster, and perform low-cost failover and fine-grained network management.

## Background information {#section_sv4_dhv_hdg .section}

You can create an ENI by using either of the following two methods:

-   Attach an ENI when you create an instance. For more information, see [Attach an ENI](reseller.en-US/Network/Elastic Network Interfaces/Attach an ENI.md#). You can attach a maximum of two ENIs. One is the primary ENI and the other is the secondary ENI. A secondary ENI created in this way will be released with the instance if it is not detached from the instance. For information about how to detach an ENI, see [EN-US\_TP\_9736.md\#](reseller.en-US/Network/Elastic Network Interfaces/Detach an ENI from an instance.md#).
-   Create a separate ENI. The created ENI can be attached to an instance. For information about how to attach an ENI, see [Attach an ENI](reseller.en-US/Network/Elastic Network Interfaces/Attach an ENI.md#). An ENI created in this way can only be used as a secondary ENI.

## Limits {#section_nhd_3tk_zdb .section}

Before you create an ENI, note the following limits:

-   Each ENI must be in a VSwitch of a VPC.
-   Each ENI must belong to at least one security group.

## Prerequisites {#section_phd_3tk_zdb .section}

-   You have created a VPC and a VSwitch in the VPC .
-   You have created a security group in the same VPC.

## Procedure {#section_rhd_3tk_zdb .section}

To create an ENI, follow these steps:

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the navigation pane on the left, choose **Networks and Security** \> **ENI**.
3.  Select the target region.
4.  Click **Create ENI**.
5.  In the Create ENI dialog box, complete the following configurations:
    1.  **Network Interface Name**: Enter a name for the ENI.
    2.  **VPC**: Select a VPC. When you attach an ENI to an instance, they must be in the same VPC.

        **Note:** After an ENI is created, you cannot change the VPC.

    3.  **VSwitch**: Select a VSwitch. When you attach an ENI to an instance, they must be in the same zone, but they do not have to be in the same VSwitch.

        **Note:** After an ENI is created, you cannot change the VSwitch.

    4.  **Primary Private IP**: Specify an IPv4 address as the private IP address of the ENI. The IPv4 address must be available in the CIDR block of the specified VSwitch. If you do not specify one, a private IP address is automatically assigned to your ENI after the ENI is created.
    5.  **Security Group**: Select a security group in the selected VPC.
    6.  **Description**: Optional. Enter a description for the ENI.
    7.  Click **OK**.

On the Network Interfaces page, refresh the table. When the new ENI is in the **Available** status, it is created successfully.

## What to do next {#section_whd_3tk_zdb .section}

After you create an ENI, you can:

-   [Attach an ENI to an instance](reseller.en-US//Attach an ENI to an instance.md).
-   [Modify attributes of the ENI](reseller.en-US/Network/Elastic Network Interfaces/Modify attributes of an ENI.md).
-   [Delete the ENI](reseller.en-US/Network/Elastic Network Interfaces/Delete an ENI.md).

