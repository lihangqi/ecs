# Change configurations of Pay-As-You-Go instances {#concept_fzw_gbf_5db .concept}

This topic describes how to change configurations of Pay-As-You-Go instances, including the number of vCPUs and memory size.

**Note:** Changing instance configurations requires stopping your instance, which disrupts services. Exercise caution when performing this action. We recommend that you perform this operation during off-peak hours.

## Limits {#section_hxl_fc2_xdb .section}

-   You can change the configurations of an instance multiple times, but the interval between two change operations must be at least five minutes.

-   You cannot change the configurations of instances within or between such instance type families: d1, d1ne, i1, i2, ga1, gn5, f1, f2, f3, ebmc4, ebmg5, sccg5, and scch5. For more information, see [instance type families that support upgrading instance types](reseller.en-US/Instances/Change configurations/Instance type families that support instance type upgrades.md#).


## Prerequisites {#section_jyl_fc2_xdb .section}

The instance has been stopped.

## Procedure {#section_kyl_fc2_xdb .section}

To change configurations of an instance, follow these steps:

1.  Find the target instance. In the **Actions** column, click **Change Instance Type**.
2.  On the Instance Type page, select the desired instance type and click **Confirm**.

    **Note:** You can also call the [DescribeResourcesModification](../reseller.en-US/API Reference/Regions/DescribeResourcesModification.md#) API action to query the instance types that can be changed.


The new configuration takes effect immediately after the change is complete. You can view the instance type information in the **Basic Information** area of the Instance Details page, as shown in the following figure.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9644/15667877415424_en-US.png)

