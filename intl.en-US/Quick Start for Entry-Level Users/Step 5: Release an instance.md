# Step 5: Release an instance {#concept_aj2_fxn_s2b .concept}

If you no longer need an instance, release it so it does not continue to incur costs.

For VPC-Connected instances, if you do not enable the No fees for stopped instances \(VPC-Connected\) feature, costs are incurred after instances are stopped. For instances in classic networks, costs are always incurred after instances are stopped. If you no longer need an instance, you can release it. For more information, see [Stop an instance](../../../../reseller.en-US/User Guide/Instances/Start or stop an instance.md#section_fdq_nsl_xdb) and [Release an instance](../../../../reseller.en-US/User Guide/Instances/Release an instance.md#).

This article describes how to release a Pay-As-You-Go instance on the console. Subscription instances are released automatically after the billing cycle ends.

**Note:** If there is data on the instance, we recommend that you [create a snapshot](../../../../reseller.en-US/User Guide/Snapshots/Create snapshots.md#) to back up the data before releasing it.

## Procedure {#section_t4p_zxn_s2b .section}

1.  Log on to the [ECS Console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, click **Instances**.
3.  Select a region. In this example, select China East 1.
4.  In the list of instances, locate the instance ecs-01 to release. In the **Actions** column, click **More** \> **Instance Status** \> **Release**.
5.  Select **Release Now**, then click **Next**.
6.  Confirm that you want to release the instance, then click **OK**.

The released instance is then no longer displayed on the Instances page.

