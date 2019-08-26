# Step 5. Release an instance {#concept_aj2_fxn_s2b .concept}

This topic describes how to release an ECS instance. If you no longer need an instance, you can release it so it does not continue to incur fees.

For VPC-Connected instances, if you do not enable the **No fees for stopped instances \(VPC-Connected\)** feature, the instance continues to incur fees even after it is stopped. For instances in classic networks, the instance constantly incurs fees throughput its lifecycle. If you no longer need an instance, you can release it to prevent any possible fees. For more information, see [Stop an instance](../intl.en-US/Instances/Manage instances/Start or stop an instance.md#section_fdq_nsl_xdb) and [Release an instance](../intl.en-US/Instances/Manage instances/Release an instance.md#).

This topic describes how to release a Pay-As-You-Go instance in the ECS console. Subscription instances are released automatically after the billing cycle ends.

**Note:** If there is data on the instance, we recommend that you [create a snapshot](../intl.en-US/Snapshots/Use snapshots/Create a snapshot.md#) to back up the data before releasing it.

## Procedure {#section_t4p_zxn_s2b .section}

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).
2.  In the left-side navigation pane, choose **Instances & Images** \> **Instances**.
3.  In the upper-left corner, select the target region.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/123261/156229798550161_en-US.png)

4.  In the list of instances, locate the instance ecs-01 to release. In the **Actions** column, choose **More** \> **Instance Status** \> **Release**.
5.  In the displayed dialog box, select **Release Now**, then click **Next**.
6.  Confirm that you want to release the instance, then click **OK**.

The released instance is then no longer displayed on the Instances page.

