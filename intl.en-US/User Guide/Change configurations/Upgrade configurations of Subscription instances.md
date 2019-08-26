# Upgrade configurations of Subscription instances {#concept_jl1_2bf_5db .concept}

You can upgrade a Subscription-billed instance type.

you can also:

-   **Convert the billing method of data disks**from Pay-As-You-Go to Subscription. The billing method of system disks cannot be changed.
-   **Change the Internet bandwidth**. This applies to the instances in a classic network and instances in a VPC that are not bound with EIPs. If you do not purchase Internet bandwidth when creating an instance, no public IP address is assigned. In this case, you can use this feature to assign a public IP address to the instance when needed.

## Fees {#section_u4k_fyd_xdb .section}

After upgrading the configuration, you must make up the difference for the rest of the current billing cycle.

## Limits {#section_v4k_fyd_xdb .section}

This feature has the following limits:

-   Only applicable to Subscription instances.

-   You can upgrade an instance multiple times, but the time period between each upgrade must be at least five minutes.

-   You must upgrade both the vCPU cores and memory size of an instance type. That is, you cannot upgrade one item separately.

-   Not supported within or between such instance type families: d1, d1ne, i1, i2, ga1, gn5, f1, f2, f3, ebmc4, ebmg5, sccg5, and scch5. For the instance type families that support this feature and the rules for upgrading instance types, see [instance type families that support upgrading instance types](reseller.en-US/User Guide/Instances/Change configurations/Instance type families that support upgrading instance types.md#).

-   This feature can be used to change the Internet bandwidth only for VPC instances bound with no EIPs and classic network instances.

-   You can change the billing method from Pay-As-You-Go to Subscription only for data disks, not for system disks.

-   In the current billing cycle, if you have already performed the [renewal for configuration downgrade](../../../../reseller.en-US/Pricing/Renew instances/Renew for configuration downgrade.md#) operation, you cannot upgrade the configuration until a new billing cycle begins.

-   After upgrading an instance type or changing the Internet bandwidth of a classic network instance from 0 Mbps to a non-zero value for the first time, you must restart the instance on the console or through the [RebootInstance](../../../../reseller.en-US/API Reference/Instances/RebootInstance.md#) API to activate the new configuration.


## Procedure {#section_gvw_myd_xdb .section}

1.  Log on to the [ECS Console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, click **Instances**.
3.  Select a region.
4.  Select the Subscription instance to upgrade and, in the **Actions** column, click **Change Configuration**.
5.  Select **Upgrade Configuration** and click **Continue**.
6.  On the Upgrade Configuration page, perform any of the following operations:
    -   Select a new **Instance Type**.

        **Note:** The page displays all the new instance types that are available for your instance.

    -   If a [Pay-As-You-Go-billed data disk is attached](reseller.en-US/User Guide/Cloud disks/Attach a cloud disk.md#) to your instance, you can convert its billing method to Subscription.
    -   If the instance is a classic network instance, or is VPC-Connected and not bound with an EIP, you can modify its Internet bandwidth.

        **Note:** If you do not purchase Internet bandwidth when creating an instance, no public IP address is assigned. In this case, you can use this feature to assign a public IP address to the instance when needed.

7.  Confirm your order details, and then click **Create Order**. Follow additional instructions as required.
8.  After upgrading an instance type or changing the Internet bandwidth of a classic network instance from 0 Mbps to a non-zero value for the first time, you must restart the instance through the console or through the [RebootInstance](../../../../reseller.en-US/API Reference/Instances/RebootInstance.md#) API to activate the new configuration.

    **Note:** You do not have to restart a VPC instance if this upgrade configuration is the first time its Internet bandwidth is increased from 0 Mbps to a non-zero value.


You can also use the [DescribeResourcesModification](../../../../reseller.en-US/API Reference/Regions/DescribeResourcesModification.md#) API to query the instance types that can be upgraded.

