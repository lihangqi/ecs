# Modify attributes of an ENI {#concept_wn3_c3k_zdb .concept}

You can modify attributes of a secondary ENI, but not the primary ENI, of an instance. You can modify the following attributes of an ENI:

-   The name of the ENI.
-   The security group associated with the ENI. One ENI must be associated with at least one security group. However, it cannot be associated with more than five security groups.
-   Description of the ENI.

You can modify attributes of an ENI when it is in the **Available** or the **Bound** status. This document describes how to modify attributes of an ENI in the ECS console.

## Prerequisite {#section_lk2_f3k_zdb .section}

Before you modify attributes of an ENI, [create an ENI](intl.en-US/User Guide/Elastic Network Interfaces/Create an ENI.md).

## Procedure {#section_mk2_f3k_zdb .section}

To modify attributes of an ENI, follow these steps:

1.  Log on to the [ECS console](https://ecs.console.aliyun.com/?spm=a2c4g.11186623.2.9.FNEORG#/home).
2.  In the left-side navigation pane, select **Networks and Security** \> **ENI**.
3.  Select a region.
4.  Find an ENI, and in the **Actions** column, click **Modify**.
5.  In the Modify dialog box, modify the following optional configurations:
    -   **Network Interface Name**: Specify a new name for the selected ENI.
    -   **Security Group**: Select more security groups for the ENI, or remove security groups. Retain at least one security group.
    -   **Description**: Give a brief description for the ENI.

        After you finish the modification, click **OK**.


