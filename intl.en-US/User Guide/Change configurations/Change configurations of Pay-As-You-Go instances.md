# Change configurations of Pay-As-You-Go instances {#concept_fzw_gbf_5db .concept}

This article describes how to change configurations of Pay-As-You-Go instances. For information about how to change configurations of \(Subscription\) instances, see [overview of configuration changes](reseller.en-US/User Guide/Instances/Change configurations/Overview of configuration changes.md#).

**Note:** Changing instance configurations requires stopping your instance, which disrupts services. Exercise caution when performing this action.

## Limits {#section_hxl_fc2_xdb .section}

-   You can upgrade an instance multiple times, but the time period between each upgrade must be at least five minutes.

-   Not supported within or between such instance type families: d1, d1ne, i1, i2, ga1, gn5, f1, f2, f3, ebmc4, ebmg5, sccg5, and scch5. For more information, see [instance type families that support upgrading instance types](reseller.en-US/User Guide/Instances/Change configurations/Instance type families that support upgrading instance types.md#).


## Prerequisite {#section_jyl_fc2_xdb .section}

The instance has been stopped.

## Procedure {#section_kyl_fc2_xdb .section}

To change instance type configurations of the instance, follow these steps:

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, click **Instances**.
3.  Select the target region.
4.  In the **Actions** column, click **Change Instance Type**.
5.  On the Instance Type page, select the desired instance type and click **Confirm**.

    **Note:** You can also enter the instance type information in the search box to filter instance types.


Once the change is complete, it takes effect immediately. You can view the instance type information in the **Basic Information** area of the Instance Details page, as shown in the following figure.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9644/15395038325424_en-US.png)

Then, restart the instance to restore your services.

You can also use the [DescribeResourcesModification](../../../../reseller.en-US/API Reference/Regions/DescribeResourcesModification.md#) API to query the instance types that can be changed.

